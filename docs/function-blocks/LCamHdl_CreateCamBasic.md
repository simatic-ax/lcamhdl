# LCamHdl_CreateCamBasic

## Principle of operation

A cam disk can be created at runtime with a SIMATIC S7-1500T CPU. To interpolate the movement between two points of the cam profile a 5th degree polynomial is used.
The leading value of the first point defines the start of the cam disk and the leading value of the last point defines the end of the cam disk. As the indexes in the cam profile increase also the according leading values have to increase.

A maximum number of 51 points can be used in a cam profile to define a cam.
The fuction block `LCamHdl_CreateCamBasic` first fills the necessary segments in the cam
technology object and then interpolates the cam.

## Function Characteristics

See [Function Characteristics](./Function_Characteristics.md)

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
| 16#8201 | `ERR_CAM_SEGMENTS_OUT_OF_BOUNDS` | Too many segments needed to define cam (Maximum 50) |
| 16#8202 | `ERR_INVALID_LEADING_VALUE` | Leading value is not valid (has to increase from one point to the next) |
| 16#8400 | `ERR_CAM_DISK_IN_USE` | Cam disk is in use and can't be interpolated |
| 16#8600 | `ERR_INTERPOLATE_CAM` | Error occurred while interpolating cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8601 | `ERR_INVALID_STATE` | Invalid state of the state machine |
| 16#8602 | `ERR_RESET_CAM` | Error at reset cam – see return value of system function (diagnostics.subfunctionStatus) |
| 16#8604 | `ERR_COPY_CAM_DATA` | Error at copy cam data – see return value of system function (diagnostics.subfunctionStatus) |

## Example

### Configuration File

First, define the cam profile points in a configuration file:

```iec-st
USING Simatic.Ax.LCamHdl;
CONFIGURATION CamBasicConfiguration
    VAR_GLOBAL
        profileBasic : ARRAY[1..8] OF LCamHdl_typeBasicPoint := [
            (leadingValue := 100.0,
            followingValue := 0.0,
            velocityRatio := 1.0,
            accelerationRatio := 0.0),
            (leadingValue := 200.0,
            followingValue := 100.0,
            velocityRatio := 1.0,
            accelerationRatio := 0.0),
            (leadingValue := 250.0,
            followingValue := 100.0,
            velocityRatio := 0.0,
            accelerationRatio := 0.0),
            (leadingValue := 300.0,
            followingValue := 100.0,
            velocityRatio := 0.0,
            accelerationRatio := 0.0),
            (leadingValue := 350.0,
            followingValue := 100.0,
            velocityRatio := -2.0,
            accelerationRatio := 0.0),
            (leadingValue := 400.0,
            followingValue := 0.0,
            velocityRatio := -2.0,
            accelerationRatio := 0.0),
            (leadingValue := 425.0,
            followingValue := 0.0,
            velocityRatio := 0.0,
            accelerationRatio := 0.0),
            (leadingValue := 460.0,
            followingValue := 0.0,
            velocityRatio := 0.0,
            accelerationRatio := 0.0)
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
    FUNCTION_BLOCK TestCreateCamBasic
        VAR_INPUT
            execute : BOOL;
            cam : DB_ANY;  // Reference to the cam technology object DB
        END_VAR
        
        VAR_EXTERNAL
            profileBasic : ARRAY[1..8] OF LCamHdl_typeBasicPoint;  // Reference to the globally defined profile
        END_VAR
        
        VAR
            instCreateCamBasic : LCamHdl_CreateCamBasic;
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
            instCreateCamBasic(
                execute := execute,
                camProfile := profileBasic,
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
    testCreateCamBasic : LCamHdl.Tests.TestCreateCamBasic;
    execute : BOOL;
    camDB : DB_ANY;  // DB reference to the cam technology object
END_VAR

// Call the function block
testCreateCamBasic(
    execute := execute,
    cam := camDB
);
END_PROGRAM
```
