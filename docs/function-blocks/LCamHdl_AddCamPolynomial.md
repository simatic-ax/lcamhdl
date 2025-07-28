# LCamHdl_AddCamPolynomial

## Principle of operation

A polynomial element with or without trigonometric portion can be created at
runtime with a SIMATIC S7-1500T CPU with this type of function block. Gaps
between the segments are interpolated by the runtime system with the interpolation
method chosen in the selected technology object cam.

A maximum number of 50 segments in a cam profile can be used to define a cam.
The function block `LCamHdl_AddCamPolynomial` can be configured to delete preceding or
successive cam segments and cam points. In addition it is possible to interpolate
the cam disk at the end with the interpolateCam configuration bit.

## Function Characteristics

See [Function Characteristics](./Function_Characteristics.md)

## Interface

### Input Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `execute` | `BOOL` | `FALSE` | Rising edge starts action once |
| `numberOfElements` | `INT` | `-1` | Number of used array elements of camProfile (-1 for whole array) |
| `startSegmentIndex` | `INT` | `1` | Start index of cam segment data (1-50) |
| `config` | [`LCamHdl_typePolynomialConfig`](../types/LCamHdl_typePolynomialConfig.md) | - | Config for interpolating the cam disk and deleting preceding or successive cam points/segments |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `done` | `BOOL` | TRUE: Commanded action has been completed successfully |
| `busy` | `BOOL` | TRUE: FB is not finished and new output values can be expected |
| `error` | `BOOL` | TRUE: Rising edge informs that an error occurred during the execution of the FB |
| `status` | [`LCamHdl_AddCamPolynomialStatus`](../types/StatusCodes/LCamHdl_AddCamPolynomialStatus.md) | 16#0000 - 16#7FFF: Status of the FB, 16#8000 - 16#FFFF: Error identification |
| `nextSegmentIndex` | `INT` | Next "empty" segment index |
| `diagnostics` | [`LCamHdl_typeDiagnostics`](../types/LCamHdl_typeDiagnostics.md) | Diagnostics information of FB |

### In/Out Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `camProfile` | `ARRAY[*] OF` [`LCamHdl_typePolynomialElement`](../types/LCamHdl_typePolynomialElement.md) | Definition of the cam disk to be created |
| `cam` | `TO_Cam` | Technology object cam disk |

### Status Codes

#### Operation Status Codes (16#0000 - 16#7FFF)

| Code | Name | Description |
|------|------|-------------|
| 16#0000 | `STATUS_EXECUTION_FINISHED` | FB has created a cam successfully |
| 16#7000 | `STATUS_NO_CALL` | No call of FB |
| 16#7001 | `STATUS_FIRST_CALL` | First call of FB after enabling |
| 16#7002 | `STATUS_SUBSEQUENT_CALL` | Subsequent call of FB |

#### Error Status Codes (16#8000 - 16#FFFF)

| Code | Name | Description |
|------|------|-------------|
| 16#8200 | `ERR_INVALID_PROFILE_TYPE` | Invalid profile type in element no., see diagnostics.errorElementNo |
| 16#8202 | `ERR_CAM_SEGMENTS_OUT_OF_BOUNDS` | Maximum number of cam segments (50) of the technology object was exceeded |
| 16#8209 | `ERR_LEADING_RANGE` | The difference between start and end leading value is <= 0 in element no., see diagnostics.errorElementNo |
| 16#820B | `ERR_INVALID_NUMBER_OF_ELEMENTS` | Invalid number of cam elements |
| 16#820D | `ERR_INVALID_PERFORMANCE_MODE` | Invalid performance mode parameter |
| 16#8220 | `ERR_INVALID_DELETE_OPTION` | Invalid delete option - check config |
| 16#8222 | `ERR_INVALID_START_SEGMENT_INDEX` | Invalid startSegmentIndex, 1<=startSegmentIndex <=50 |
| 16#8225 | `ERR_MISSING_PROFILE_DATA` | No profile data available |
| 16#8240 | `ERR_INVALID_POLYNOMIAL_MODE` | Invalid polynomial mode in element no., see diagnostics.errorElementNo |
| 16#8245 | `ERR_INVALID_PHASE` | Invalid following start or end position in element no., see diagnostics.errorElementNo |
| 16#8246 | `ERR_INVALID_PERIOD_LENGTH` | Invalid period length in element no., see diagnostics.errorElementNo |
| 16#8247 | `ERR_INVALID_FREQUENCY` | Invalid frequency in element no., see diagnostics.errorElementNo |
| 16#8400 | `ERR_CAM_IN_USE` | Cam is in use and can't be interpolated |
| 16#8600 | `ERR_INTERPOLATE_CAM` | Error at interpolate cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8601 | `ERR_INVALID_STATE` | Internal error, invalid state |
| 16#8602 | `ERR_RESET_CAM` | Error at reset cam – see return value of system function (diagnostics.subfunctionStatus) |
