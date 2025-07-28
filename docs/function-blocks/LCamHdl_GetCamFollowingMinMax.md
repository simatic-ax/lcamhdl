# LCamHdl_GetCamFollowingMinMax

## Principle of operation

The function block `LCamHdl_GetCamFollowingMinMax` determines the minimum and maximum following values of the cam and their first, second and third derivatives. The minimum and maximum values are determined by scanning the cam with a defined number of samples (see input `totalNumberOfSamples`).

NOTE To determine the first and second derivatives of the cam’s following values, the system function `MC_GetCamFollowingValueCyclic` is used. The third derivative is not calculated by numerical differentiation of the second derivative anymore, because `MC_GetCamFollowingValueCyclic` (V9.0) provides this value now.

NOTE The value of input `totalNumberOfSamples` defines the number of samples per complete leading value range (definition range) of the cam disk. If the minimum and maximum values are only determined in a specific subrange of the cam
(input `specificRange` = TRUE), the resulting number of samples is therefore reduced accordingly, i.e. the total runtime of the block is also reduced.

During the determination the output busy indicates the value TRUE. The error free completion is shown with done = TRUE. Status and error are output at the outputs status and error as well as diagnostics.

## Function Characteristics

See [Function Characteristics](./Function_Characteristics.md)

## Interface

### Input Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `execute` | `BOOL` | `FALSE` | Rising edge starts action once |
| `specificRange` | `BOOL` | `FALSE` | TRUE: Determine minima and maxima in a specified subrange; FALSE: Determine minima and maxima in the complete leading value range (definition range) of the cam disk |
| `startPosition` | `LREAL` | `0.0` | Start position of the specific range for determining the minima and maxima (only relevant if 'specificRange' = TRUE). Note: value must be within the leading value range (definition range) of the cam disk AND 'startPosition' < 'endPosition', otherwise the complete leading value range is used |
| `endPosition` | `LREAL` | `0.0` | End position of the specific range for determining the minima and maxima (only relevant if 'specificRange' = TRUE). Note: value must be within the leading value range (definition range) of the cam disk AND 'startPosition' < 'endPosition', otherwise the complete leading value range is used |
| `totalNumberOfSamples` | `INT` | `1000` | Total number of samples per complete leading value range (definition range) of the cam disk for MC_GetCamFollowingValue(Cyclic) functionality. Use of 721 samples is recommended for leading value range 360°, i.e. every 0.5° one sample |
| `numberOfSamplesPerCall` | `INT` | `30` | Number of samples ("MC_GetCamFollowingValue(Cyclic) calls") per block call. The higher the value, the higher the OB runtime, but less OB calls necessary |
| `masterOffset` | `LREAL` | `0.0` | Offset of the leading values of the cam. The cam technology object is not changed |
| `slaveOffset` | `LREAL` | `0.0` | Offset of the following values of the cam. The cam technology object is not changed |
| `masterScaling` | `LREAL` | `1.0` | Scaling of the leading values of the cam (value = 0.0: not permitted). The cam technology object is not changed |
| `slaveScaling` | `LREAL` | `1.0` | Scaling of the following values of the cam. The cam technology object is not changed |
| `applicationMode` | `DINT` | `3` | Determine minimum and maximum of: 0: only the following value (position), 1: the following value and first derivative (position, velocity), 2: the following value, first derivative and second derivative (position, velocity, acceleration), 3: the following value, first derivative, second derivative and third derivative (position, velocity, acceleration, jerk) |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `done` | `BOOL` | TRUE: Commanded functionality has been completed successfully |
| `busy` | `BOOL` | TRUE: FB is not finished and new output values can be expected |
| `error` | `BOOL` | TRUE: An error occurred during the execution of the FB |
| `status` | [`LCamHdl_GetCamFollowingMinMaxStatus`](../types/StatusCodes/LCamHdl_GetCamFollowingMinMaxStatus.md) | 16#0000 - 16#7FFF: Status of the FB, 16#8000 - 16#FFFF: Error identification |
| `followingValueMin` | `LREAL` | Cam following value minimum (valid when 'done' = TRUE) |
| `followingValueMax` | `LREAL` | Cam following value maximum (valid when 'done' = TRUE) |
| `firstDerivativeMin` | `LREAL` | Cam following value first derivative minimum (valid when 'done' = TRUE) |
| `firstDerivativeMax` | `LREAL` | Cam following value first derivative maximum (valid when 'done' = TRUE) |
| `secondDerivativeMin` | `LREAL` | Cam following value second derivative minimum (valid when 'done' = TRUE) |
| `secondDerivativeMax` | `LREAL` | Cam following value second derivative maximum (valid when 'done' = TRUE) |
| `thirdDerivativeMin` | `LREAL` | Cam following value third derivative minimum (valid when 'done' = TRUE) |
| `thirdDerivativeMax` | `LREAL` | Cam following value third derivative maximum (valid when 'done' = TRUE) |
| `diagnostics` | [`LCamHdl_typeDiagnostics`](../types/LCamHdl_typeDiagnostics.md) | Diagnostics information of FB |

### In/Out Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `cam` | `TO_Cam` | Reference to the cam disk |

### Status Codes

#### Operation Status Codes (16#0000 - 16#7FFF)

| Code | Name | Description |
|------|------|-------------|
| 16#0000 | `STATUS_EXECUTION_FINISHED` | Execution finished without errors |
| 16#7000 | `STATUS_NO_CALL` | No job being currently processed |
| 16#7001 | `STATUS_FIRST_CALL` | First call after incoming new job (rising edge 'execute') |
| 16#7002 | `STATUS_SUBSEQUENT_CALL` | Subsequent call during active processing without further details |

#### Error Status Codes (16#8000 - 16#FFFF)

| Code | Name | Description |
|------|------|-------------|
| 16#8210 | `ERR_TOTAL_NUMBER_OF_SAMPLES` | Invalid totalNumberOfSamples, 2<=totalNumberOfSamples |
| 16#8211 | `ERR_NUMBER_OF_SAMPLES_PER_CALL` | Invalid numberOfSamplesPerCall, 1<=numberOfSamplesPerCall |
| 16#8601 | `ERR_INVALID_STATE` | Invalid state of the state machine |
| 16#8603 | `ERR_GETCAMFOLLOWINGVALUE` | Error at MC_GetCamFollowingValue(Cyclic) - see return value of system function (diagnostics.subfunctionStatus) |
