# LCamHdl_CreateCam10kBasic

## Description

The function block `LCamHdl_ CreateCam10kBasic` is a copy of the function block
[LCamHdl_ CreateCamBasic](./LCamHdl_CreateCamBasic.md). The "..10k.." version enables using a cam technology object of type `TO_Cam_10k` instead of `TO_Cam`.

## Interface

### Input Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `execute` | `BOOL` | `FALSE` | Rising edge starts action once |
| `numberOfPoints` | `INT` | `-1` | Number of used points of camProfile (-1 for whole array; Maximum 51) |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `done` | `BOOL` | TRUE: Commanded action has been completed successfully |
| `busy` | `BOOL` | TRUE: FB is not finished and new output values can be expected |
| `error` | `BOOL` | TRUE: Rising edge informs that an error occurred during the execution of the FB |
| `status` | [`LCamHdl_CreateCamBasicStatus`](../types/StatusCodes/LCamHdl_CreateCamBasicStatus.md) | 16#0000 - 16#7FFF: Status of the FB, 16#8000 - 16#FFFF: Error identification |
| `diagnostics` | [`LCamHdl_typeDiagnostics`](../types/LCamHdl_typeDiagnostics.md) | Diagnostics information of FB |

### In/Out Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `camProfile` | `ARRAY[*] OF` [`LCamHdl_typeBasicPoint`](../types/LCamHdl_typeBasicPoint.md) | Definition of the cam disk to be created |
| `cam` | `TO_Cam_10k` | Technology object cam disk (10k) |

### Status Codes

#### Operation Status Codes (16#0000 - 16#7FFF)

| Code | Name | Description |
|------|------|-------------|
| 16#0000 | `STATUS_EXECUTION_FINISHED` | Execution finished without errors |
| 16#7000 | `STATUS_NO_CALL` | No call of FB |
| 16#7001 | `STATUS_FIRST_CALL` | First call of FB after enabling |
| 16#7002 | `STATUS_SUBSEQUENT_CALL` | Subsequent call of FB |

#### Error Status Codes (16#8000 - 16#FFFF)

| Code | Name | Description |
|------|------|-------------|
| 16#8200 | `ERR_NO_OF_POINTS_OUT_OF_BOUNDS` | NumberOfPoints is greater than the points in the camProfile or there is only one point in the camProfile |
| 16#8201 | `ERR_CAM_SEGMENTS_OUT_OF_BOUNDS` | Too many segments needed to define cam (Maximum 50) |
| 16#8202 | `ERR_INVALID_LEADING_VALUE` | Leading value is not valid (has to increase from one point to the next) |
| 16#8400 | `ERR_CAM_DISK_IN_USE` | Cam disk is in use and can't be interpolated |
| 16#8600 | `ERR_INTERPOLATE_CAM` | Error occurred while interpolating cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8601 | `ERR_INVALID_STATE` | Invalid state of the state machine |
| 16#8602 | `ERR_RESET_CAM` | Error at reset cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8604 | `ERR_COPY_CAM_DATA` | Error at copy cam data – see return value of system function (diagnostics.subfunctionStatus) |
