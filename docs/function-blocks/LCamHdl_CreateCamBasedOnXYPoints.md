# LCamHdl_CreateCamBasedOnXYPoints

## Principle of operation

The function block `LCamHdl_CreateCamBasedOnXYPoints` writes the points of the cam
profile data (leading (X) and following (Y) value) into the cam technology object and
then interpolates the cam.
A maximum number of 1000 points can be used in a cam profile to define a cam.
No use of cam segments is made.

## Function Characteristics

See [Function Characteristics](./Function_Characteristics.md)

## Interface

### Input Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `execute` | `BOOL` | `FALSE` | Rising edge starts action once |
| `numberOfPoints` | `INT` | `-1` | Number of used points of camProfile (-1 for whole array; Maximum 1000) |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `done` | `BOOL` | TRUE: Commanded action has been completed successfully |
| `busy` | `BOOL` | TRUE: FB is not finished and new output values can be expected |
| `error` | `BOOL` | TRUE: Rising edge informs that an error occurred during the execution of the FB |
| `status` | [`LCamHdl_CreateCamBasedOnXYPointsStatus`](../types/StatusCodes/LCamHdl_CreateCamBasedOnXYPointsStatus.md) | 16#0000 - 16#7FFF: Status of the FB, 16#8000 - 16#FFFF: Error identification |
| `diagnostics` | [`LCamHdl_typeDiagnostics`](../types/LCamHdl_typeDiagnostics.md) | Diagnostics information of FB |

### In/Out Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `camProfile` | `ARRAY[*] OF TO_Cam_Struct_PointData` | Definition of the cam disk to be created |
| `cam` | `TO_Cam` | Technology object cam disk |

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
| 16#8201 | `ERR_CAM_POINTS_OUT_OF_BOUNDS` | Too many points needed to define cam (Maximum 1000) |
| 16#8400 | `ERR_CAM_DISK_IN_USE` | Cam disk is in use and can't be interpolated |
| 16#8600 | `ERR_INTERPOLATE_CAM` | Error occurred while interpolating cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8601 | `ERR_INVALID_STATE` | Invalid state of the state machine |
| 16#8602 | `ERR_RESET_CAM` | Error at reset cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8604 | `ERR_COPY_CAM_DATA` | Error at copy cam data – see return value of system function (diagnostics.subfunctionStatus) |

## Example

### Configuration File

First, define the cam profile points in a configuration file:

```iec-st
USING Siemens.Simatic.S71500.MotionControl.Native;
CONFIGURATION XYPointConfiguration
    VAR_GLOBAL
        profile : ARRAY[1..5] OF TO_Cam_Struct_PointData := [
            (x := 0.0, y := 0.0),
            (x := 0.25, y := 0.5),
            (x := 0.5, y := 1.0),
            (x := 0.75, y := 0.5),
            (x := 1.0, y := 0.0)
            // Additional points can be added here
        ];
    END_VAR
END_CONFIGURATION
```

### Function Block Implementation

Then, implement the function block that uses the cam profile:

```iec-st
USING Simatic.Ax.LCamHdl;
USING Siemens.Simatic.S71500.MotionControl.Native;
NAMESPACE LCamHdl.Tests
    FUNCTION_BLOCK TestCreateCamBasedOnXYPoints
        VAR_INPUT
            execute : BOOL;
            cam : DB_ANY;  // Reference to the cam technology object DB
        END_VAR
        
        VAR_EXTERNAL
            profile : ARRAY[1..5] OF TO_Cam_Struct_PointData;  // Reference to the globally defined profile
        END_VAR
        
        VAR
            instCreateCamBasedOnXYPoints : LCamHdl_CreateCamBasedOnXYPoints;
            camRef : REF_TO TO_Cam;  // Reference to the cam technology object
            initialCall : BOOL := FALSE;
        END_VAR
        
        // Initialize the cam reference on first call
        IF NOT initialCall THEN
            camRef := AsCamRef(cam);  // Convert DB_ANY to REF_TO TO_Cam
            initialCall := TRUE;
        END_IF;
        
        // Only proceed if the cam reference is valid
        IF camRef <> NULL THEN
            // Call the function block with the dereferenced cam reference
            instCreateCamBasedOnXYPoints(
                execute := execute,
                camProfile := profile,
                cam := camRef^  // Dereference the cam reference
            );
        END_IF;
    END_FUNCTION_BLOCK
END_NAMESPACE
```

### Program Implementation

Finally, use the function block in your program:

```iec-st
USING Siemens.Simatic.S71500.MotionControl.Native;
PROGRAM Main
VAR
    testCreateCamBasedOnXYPoints : LCamHdl.Tests.TestCreateCamBasedOnXYPoints;
    execute : BOOL;
    camDB : DB_ANY;  // DB reference to the cam technology object
END_VAR

// Call the function block
testCreateCamBasedOnXYPoints(
    execute := execute,
    cam := camDB
);
END_PROGRAM
```
