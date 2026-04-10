# BasicStatus

## Overview

The named value `BasicStatus` defines status codes for the following function blocks:

- [CreateCamBasic](../../function-blocks/LCamHdl_CreateCamBasic.md) / [CreateCam10kBasic](../../function-blocks/LCamHdl_CreateCam10kBasic.md)
- [CreateCamBasedOnXYPoints](../../function-blocks/LCamHdl_CreateCamBasedOnXYPoints.md) / [CreateCam10kBasedOnXYPoints](../../function-blocks/LCamHdl_CreateCam10kBasedOnXYPoints.md)

Not every status code is used by every function block. The individual function block documentation lists the applicable subset.

## Status Codes

### Operation Status Codes (16#0000 - 16#7FFF)

| Code | Name | Description |
| ---- | ---- | ----------- |
| 16#0000 | `STATUS_EXECUTION_FINISHED` | Execution finished without errors |
| 16#7000 | `STATUS_NO_CALL` | No call of FB |
| 16#7001 | `STATUS_FIRST_CALL` | First call of FB after enabling |
| 16#7002 | `STATUS_SUBSEQUENT_CALL` | Subsequent call of FB |

### Error Status Codes (16#8000 - 16#FFFF)

| Code | Name | Description |
| ---- | ---- | ----------- |
| 16#8200 | `ERR_NO_OF_POINTS_OUT_OF_BOUNDS` | NumberOfPoints is greater than the points in the camProfile or there is only one point in the camProfile |
| 16#8201 | `ERR_CAM_DATA_OUT_OF_BOUNDS` | Too many points (max 1000) or segments (max 50) needed to define cam |
| 16#8202 | `ERR_INVALID_LEADING_VALUE` | Leading value is not valid (has to increase from one point to the next) |
| 16#8400 | `ERR_CAM_DISK_IN_USE` | Cam disk is in use and can't be interpolated |
| 16#8600 | `ERR_INTERPOLATE_CAM` | Error occurred while interpolating cam - see return value of system function (diagnostics.subfunctionStatus) |
| 16#8601 | `ERR_INVALID_STATE` | Invalid state of the state machine |
| 16#8602 | `ERR_RESET_CAM` | Error at reset cam - see return value of system function (diagnostics.subfunctionStatus) |
| 16#8604 | `ERR_COPY_CAM_DATA` | Error at copy cam data - see return value of system function (diagnostics.subfunctionStatus) |
