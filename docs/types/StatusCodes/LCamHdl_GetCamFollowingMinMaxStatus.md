# LCamHdl_GetCamFollowingMinMaxStatus

## Overview

The named value `LCamHdl_GetCamFollowingMinMaxStatus` defines status codes for the [LCamHdl_GetCamFollowingMinMax](../../function-blocks/LCamHdl_GetCamFollowingMinMax.md)/[LCamHdl_GetCam10kFollowingMinMax](../../function-blocks/LCamHdlGetCam10kFollowingMinMax.md) function blocks.

## Status Codes

### Operation Status Codes (16#0000 - 16#7FFF)

| Code | Name | Description |
|------|------|-------------|
| 16#0000 | `STATUS_EXECUTION_FINISHED` | Execution finished without errors |
| 16#7000 | `STATUS_NO_CALL` | No job being currently processed |
| 16#7001 | `STATUS_FIRST_CALL` | First call after incoming new job (rising edge 'execute') |
| 16#7002 | `STATUS_SUBSEQUENT_CALL` | Subsequent call during active processing without further details |

### Error Status Codes (16#8000 - 16#FFFF)

| Code | Name | Description |
|------|------|-------------|
| 16#8210 | `ERR_TOTAL_NUMBER_OF_SAMPLES` | Invalid totalNumberOfSamples, 2<=totalNumberOfSamples |
| 16#8211 | `ERR_NUMBER_OF_SAMPLES_PER_CALL` | Invalid numberOfSamplesPerCall, 1<=numberOfSamplesPerCall |
| 16#8601 | `ERR_INVALID_STATE` | Invalid state of the state machine |
| 16#8603 | `ERR_GETCAMFOLLOWINGVALUE` | Error at MC_GetCamFollowingValue(Cyclic) - see return value of system function (diagnostics.subfunctionStatus) |