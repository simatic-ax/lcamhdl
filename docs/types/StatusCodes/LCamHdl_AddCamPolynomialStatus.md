# LCamHdl_AddCamPolynomialStatus

## Overview

The named value `LCamHdl_AddCamPolynomialStatus` defines status codes for the [LCamHdl_AddCamPolynomial](../../function-blocks/LCamHdl_AddCamPolynomial.md)/[LCamHdl_AddCam10kPolynomial](../../function-blocks/LCamHdl_AddCam10kPolynomial.md) function blocks.

## Status Codes

### Operation Status Codes (16#0000 - 16#7FFF)

| Code | Name | Description |
|------|------|-------------|
| 16#0000 | `STATUS_EXECUTION_FINISHED` | FB has created a cam successfully |
| 16#7000 | `STATUS_NO_CALL` | No call of FB |
| 16#7001 | `STATUS_FIRST_CALL` | First call of FB after enabling |
| 16#7002 | `STATUS_SUBSEQUENT_CALL` | Subsequent call of FB |

### Error Status Codes (16#8000 - 16#FFFF)

| Code | Name | Description |
|------|------|-------------|
| 16#8200 | `ERR_INVALID_PROFILE_TYPE` | Invalid profile type in element no., see diagnostics.errorElementNo |
| 16#8202 | `ERR_CAM_SEGMENTS_OUT_OF_BOUNDS` | Maximum number of cam segments (50) of the technology object was exceeded |
| 16#8209 | `ERR_LEADING_RANGE` | The difference between start and end leading value is <= 0 in element no., see diagnostics.errorElementNo |
| 16#820B | `ERR_INVALID_NUMBER_OF_ELEMENTS` | Invalid number of cam elements |
| 16#820D | `ERR_INVALID_PERFORMANCE_MODE` | Invalid performance mode parameter |
| 16#8215 | `ERR_INVALID_PARAMETER_COMBINATION` | Parameter combination leads to invalid calculated coefficients in element no., see diagnostics.errorElementNo |
| 16#8220 | `ERR_INVALID_DELETE_OPTION` | Invalid delete option - check config |
| 16#8222 | `ERR_INVALID_START_SEGMENT_INDEX` | Invalid startSegmentIndex, 1<=startSegmentIndex <=50 |
| 16#8225 | `ERR_MISSING_PROFILE_DATA` | No profile data available |
| 16#8230 | `ERR_INVALID_POLYNOMIAL_MODE` | Invalid polynomial mode in element no., see diagnostics.errorElementNo |
| 16#8240 | `ERR_INVALID_SINE_MODE` | Invalid sine mode in element no., see diagnostics.errorElementNo |
| 16#8245 | `ERR_INVALID_PHASE` | Invalid following start or end position in element no., see diagnostics.errorElementNo |
| 16#8246 | `ERR_INVALID_PERIOD_LENGTH` | Invalid period length in element no., see diagnostics.errorElementNo |
| 16#8247 | `ERR_INVALID_FREQUENCY` | Invalid frequency in element no., see diagnostics.errorElementNo |
| 16#8400 | `ERR_CAM_IN_USE` | Cam is in use and can't be interpolated |
| 16#8600 | `ERR_INTERPOLATE_CAM` | Error at interpolate cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8601 | `ERR_INVALID_STATE` | Internal error, invalid state |
| 16#8602 | `ERR_RESET_CAM` | Error at reset cam – see return value of system function (diagnostics.subfunctionStatus) |