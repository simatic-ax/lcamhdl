# LCamHdl_GetCam10kStatusWord

The function block `LCamHdl_GetCam10kStatusWord` is a copy of the function
block [LCamHdl_GetCamStatusWord](./LCamHdl_GetCamStatusWord.md). The "..10k.." version enables using a cam
technology object of type `TO_Cam_10k` instead of `TO_Cam`.

## Interface

### In/Out Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `cam` | `TO_Cam_10k` | Technology object cam disk |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `control` | `BOOL` | TRUE: Cam in use; FALSE: Cam not in use |
| `error` | `BOOL` | TRUE: Error present; FALSE: No error present |
| `restartActive` | `BOOL` | TRUE: "Restart" active. The technology object is being reinitialized; FALSE: No "Restart" active |
| `onlineStarValuesChanged` | `BOOL` | TRUE: The restart tags have been changed. For the changes to be applied, the technology object must be reinitialized; FALSE: Restart tags unchanged |
| `camDataChanged` |`BOOL` | TRUE: The definition range of the cam has changed in the technology data block; FALSE: No change |
| `interpolated` | `BOOL` | TRUE: Cam is interpolated; FALSE: Cam is not interpolated |
| `inInterpolation` | `BOOL` | TRUE: Cam is in interpolation; FALSE: Cam is not in interpolation |
| `copyCamDataActive` | `BOOL` | TRUE: A copy operation of an "MC_CopyCamData" job is active; FALSE: No copy operation of an "MC_CopyCamData" job is active |

## Migration from TIA Portal

This function block has been migrated from TIA Portal to SIMATIC AX. The functionality remains the same, but the programming model has been adapted to SIMATIC AX. Key differences include:

- Namespace: The function block now uses the `Simatic.Ax.LCamHdl` namespace
- File structure: The function block is now defined in a separate file

## See Also

- [LCamHdl_GetCamStatusWord](./LCamHdl_GetCamStatusWord.md)
- [LCamHdl_GetCam10kFollowingMinMax](./LCamHdl_GetCam10kFollowingMinMax.md)
