# LCamHdl_CreateCamAdvanced

## Prinicple of operation

A cam disk can be created at runtime with a SIMATIC S7-1500T CPU. Segments with the profile types described in this document as well as points can be used to define a cam. Gaps between the segments and/or points are interpolated by the runtime system with the interpolation method chosen in the selected technology object cam.

A maximum number of 50 segments and 1000 points in a cam profile can be used to define a cam.
The function block `LCamHdl_CreateCamAdvanced` fills the necessary segments and points in the cam technology object starting at startSegmentIndex and startPointIndex.

The function block can be configured to delete preceding or successive cam points and cam segments. In addition it is possible to interpolate the cam disk at the end with the interpolateCam configuration bit.

The default configuration has to be changed when using the `LCamHdl_CreateCamAdvanced` function block with additional function blocks.

## Function Characteristics

See [Function Characteristics](./Function_Characteristics.md)

## Interface

### Input Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `execute` | `BOOL` | `FALSE` | Rising edge starts action once |
| `numberOfElements` | `INT` | `-1` | Number of used array elements of camProfile (-1 for whole array) |
| `startSegmentIndex` | `INT` | `1` | Start index of cam segment data (1-50) |
| `startPointIndex` | `INT` | `1` | Start index of cam point data (1-1000) |
| `config` | [`LCamHdl_typeAdvancedConfig`](../types/LCamHdl_typeAdvancedConfig.md) | - | Config for interpolating the cam disk and deleting preceding or successive cam points/segments |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `done` | `BOOL` | TRUE: Commanded action has been completed successfully |
| `busy` | `BOOL` | TRUE: FB is not finished and new output values can be expected |
| `error` | `BOOL` | TRUE: Rising edge informs that an error occurred during the execution of the FB |
| `status` | [`LCamHdl_CreateCamAdvancedStatus`](../types/StatusCodes/LCamHdl_CreateCamAdvancedStatus.md) | 16#0000 - 16#7FFF: Status of the FB, 16#8000 - 16#FFFF: Error identification |
| `nextSegmentIndex` | `INT` | Next "empty" segment index |
| `nextPointIndex` | `INT` | Next "empty" point index |
| `diagnostics` | [`LCamHdl_typeDiagnostics`](../types/LCamHdl_typeDiagnostics.md) | Diagnostics information of FB |

### In/Out Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `camProfile` | `ARRAY[*] OF` [`LCamHdl_typeAdvancedElement`](../types/LCamHdl_typeAdvancedElement.md) | Definition of the cam disk to be created |
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
| 16#8201 | `ERR_CAM_POINTS_OUT_OF_BOUNDS` | Maximum number of cam points (1000) of the technology object was exceeded |
| 16#8202 | `ERR_CAM_SEGMENTS_OUT_OF_BOUNDS` | Maximum number of cam segments (50) of the technology object was exceeded |
| 16#8203 | `ERR_FOLLOWING_POS_IN_PROFILE` | Invalid following start or end position in element no., see diagnostics.errorElementNo |
| 16#8204 | `ERR_MOD_VELO_TRAPEZOID_PARAMETER` | Invalid modified velocity trapezoid parameter C, permitted values: 0 < modVeloTrapezoidParameter<= 1 in element no., see diagnostics.errorElementNo |
| 16#8205 | `ERR_MOD_SINE_MAX_ACCEL_CA_STAR` | Invalid value modSineMaxAccelCaStar in element no., see diagnostics.errorElementNo |
| 16#8206 | `ERR_ACCELERATION_ZERO` | Invalid acceleration preset geoAccelStart/End in element no., see diagnostics.errorElementNo |
| 16#8207 | `ERR_INFLECTION_POINT` | Invalid parameter for shifting the inflection point (0< λ<1) in element no., see diagnostics.errorElementNo |
| 16#8208 | `ERR_CALCULATED_INFLECTION_POINT` | Due to the parameterization, the calculated shifting of the inflection point (λ) is outside the range (0< λ<1) in element no., see diagnostics.errorElementNo |
| 16#8209 | `ERR_LEADING_RANGE` | The difference between start and end leading value is <= 0 in element no., see diagnostics.errorElementNo |
| 16#820A | `ERR_FOLLOWING_RANGE_ZERO` | The difference between start and end following value is zero in element no., see diagnostics.errorElementNo |
| 16#820B | `ERR_INVALID_NUMBER_OF_ELEMENTS` | Invalid number of cam elements |
| 16#820C | `ERR_HARM_COMB_LEADS_TO_INVALID_CA_VALUE` | Invalid parameterization of HARMONIC_COMBINATION (const. velocity – reversal / reversal – const. velocity), characteristic value Ca becomes invalid |
| 16#820D | `ERR_INVALID_PERFORMANCE_MODE` | Invalid performance mode parameter |
| 16#820E | `ERR_ACCELERATION_SIGN_INVALID` | Invalid acceleration sign (reversal point) |
| 16#820F | `ERR_CALCULATED_PARAMETER_C` | Due to the parameterization, the calculated value for c is outside the range (0< c <=1) in element no., see diagnostics.errorElementNo |
| 16#8215 | `ERR_INVALID_PARAMETER_COMBINATION` | Parameter combination leads to invalid calculated coefficients in element no., see diagnostics.errorElementNo |
| 16#8220 | `ERR_INVALID_DELETE_OPTION` | Invalid delete option - check config |
| 16#8222 | `ERR_INVALID_START_SEGMENT_INDEX` | Invalid startSegmentIndex, 1<=startSegmentIndex <=50 |
| 16#8223 | `ERR_INVALID_START_POINT_INDEX` | Invalid startPointIndex, 1<=startPointIndex <=1000 |
| 16#8400 | `ERR_CAM_IN_USE` | Cam is in use and can't be interpolated |
| 16#8600 | `ERR_INTERPOLATE_CAM` | Error at interpolate cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8601 | `ERR_INVALID_STATE` | Internal error, invalid state |
| 16#8602 | `ERR_RESET_CAM` | Error at reset cam – see return value of system function (diagnostics.subfunctionStatus) |
