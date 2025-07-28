# LCamHdl_GetCamStatusWord

## Principle of operation

The `LCamHdl_GetStatusWord` function block is splitting the status wordof a TO_Cam into bits.

## Interface

### In/Out Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `cam` | `TO_Cam` | Technology object cam disk |

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

## Example

```iec-st
USING Simatic.Ax.LCamHdl;
USING Siemens.Simatic.S71500.MotionControl.Native;

PROGRAM Use10kStatusProgram
    VAR_INPUT
        camDB : DB_ANY;
    END_VAR
    VAR
        camRef : REF_TO TO_Cam;
        initialCall : BOOL := FALSE;
        getCamStatus : LCamHdl_GetCam10kStatusWord;
        camInUse : BOOL;
        camError : BOOL;
        camInterpolated : BOOL;
    END_VAR

    // Initialize the cam reference on first call
    IF NOT initialCall THEN
        camRef := AsCamRef(cam);  // Convert DB_ANY to REF_TO TO_Cam
        initialCall := TRUE;
    END_IF;

    // Get cam status
    getCamStatus(cam := camRef^);

    // Check cam status
    camInUse := getCamStatus.control;
    camError := getCamStatus.error;
    camInterpolated := getCamStatus.interpolated;

    // Use status information
    IF camInUse THEN
        ;// Cam is in use, cannot be modified
    ELSIF camError THEN
        ;// Error present, handle error
    ELSIF NOT camInterpolated THEN
        ;// Cam is not interpolated, interpolate before use
    END_IF;
END_PROGRAM
```
