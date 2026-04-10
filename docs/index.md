# LCamHdl Library for SIMATIC AX

## Overview

The LCamHdl library provides functionality for creating cam disks at runtime in SIMATIC AX applications.

## Library Structure

The library is organized into the following main components:

### Cam Creation Function Blocks

- [`CreateCamBasic`](./function-blocks/LCamHdl_CreateCamBasic.md): Creates a basic cam profile
- [`CreateCamBasedOnXYPoints`](./function-blocks/LCamHdl_CreateCamBasedOnXYPoints.md): Creates a cam profile based on XY points
- [`CreateCamAdvanced`](./function-blocks/LCamHdl_CreateCamAdvanced.md): Creates an advanced cam profile

### Cam (10k) Creation Function Blocks

- [`CreateCam10kBasic`](./function-blocks/LCamHdl_CreateCam10kBasic.md): Creates a basic 10k cam profile
- [`CreateCam10kBasedOnXYPoints`](./function-blocks/LCamHdl_CreateCam10kBasedOnXYPoints.md): Creates a 10k cam profile based on XY points
- [`CreateCam10kAdvanced`](./function-blocks/LCamHdl_CreateCam10kAdvanced.md): Creates an advanced 10k cam profile

### Explanation of the profile types

[`CreateCamAdvanced`](./function-blocks/LCamHdl_CreateCamAdvanced.md) and [`CreateCam10kAdvanced`](./function-blocks/LCamHdl_CreateCam10kAdvanced.md) use a `camProfileType` in their cam profile definition.
For a detailed overview about the different available profile types, see [Profile Types](./ProfileTypes.md).

### Additional Profiles for Advanced Cam Creation

- [`AddCamSine`](./function-blocks/LCamHdl_AddCamSine.md): Adds a sine element to a cam profile
- [`AddCamInvSine`](./function-blocks/LCamHdl_AddCamInvSine.md): Adds an inverse sine element to a cam profile
- [`AddCamDblHarmonic`](./function-blocks/LCamHdl_AddCamDblHarmonic.md): Adds a double harmonic element to a cam profile
- [`AddCamPolynomial`](./function-blocks/LCamHdl_AddCamPolynomial.md): Adds a polynomial element to a cam profile

### Additional Profiles for Advanced Cam (10k) Creation

- [`AddCam10kSine`](./function-blocks/LCamHdl_AddCam10kSine.md): Adds a sine element to a 10k cam profile
- [`AddCam10kInvSine`](./function-blocks/LCamHdl_AddCam10kInvSine.md): Adds an inverse sine element to a 10k cam profile
- [`AddCam10kDblHarmonic`](./function-blocks/LCamHdl_AddCam10kDblHarmonic.md): Adds a double harmonic element to a 10k cam profile
- [`AddCam10kPolynomial`](./function-blocks/LCamHdl_AddCam10kPolynomial.md): Adds a polynomial element to a 10k cam profile

### Additional Functions

- [`GetCamStatusWord`](./function-blocks/LCamHdl_GetCamStatusWord.md): Gets the status word of a cam profile
- [`GetCam10kStatusWord`](./function-blocks/LCamHdl_GetCam10kStatusWord.md): Gets the status word of a 10k cam profile
- [`GetCamFollowingMinMax`](./function-blocks/LCamHdl_GetCamFollowingMinMax.md): Gets the minimum and maximum following values of a cam profile
- [`GetCam10kFollowingMinMax`](./function-blocks/LCamHdl_GetCam10kFollowingMinMax.md): Gets the minimum and maximum following values of a 10k cam profile
- [`GetCamMaxSlaveDynamics`](./functions/LCamHdl_GetCamMaxSlaveDynamics.md): Gets the maximum slave dynamics of a cam profile
- [`GetCamMaxVeloMaster`](./functions/LCamHdl_GetCamMaxVeloMaster.md): Gets the maximum master velocity of a cam profile

### Data Types

- [`typeXYPoint`](./types/LCamHdl_typeXYPoint.md)
- [`typeBasicPoint`](./types/LCamHdl_typeBasicPoint.md)
- [`typeDiagnostics`](./types/LCamHdl_typeDiagnostics.md)
- [`typeAdvancedConfig`](./types/LCamHdl_typeAdvancedConfig.md)
- [`typeAdvancedElement`](./types/LCamHdl_typeAdvancedElement.md)
- [`typeSineConfig`](./types/LCamHdl_typeSineConfig.md)
- [`typeSineElement`](./types/LCamHdl_typeSineElement.md)
- [`typeInvSineConfig`](./types/LCamHdl_typeInvSineConfig.md)
- [`typeInvSineElement`](./types/LCamHdl_typeInvSineElement.md)
- [`typeDblHarmonicConfig`](./types/LCamHdl_typeDblHarmonicConfig.md)
- [`typeDblHarmonicElement`](./types/LCamHdl_typeDblHarmonicElement.md)
- [`typePolynomialConfig`](./types/LCamHdl_typePolynomialConfig.md)
- [`typePolynomialElement`](./types/LCamHdl_typePolynomialElement.md)

### Constants

- [`ConfigConstants`](./constants/LCamHdl_ConfigConstants.md): Configuration constants
- [`ProfileConstants`](./constants/LCamHdl_ProfileConstants.md): Profile constants
- [`AdditionalConstants`](./constants/LCamHdl_AdditionalConstants.md): Additional constants

### Status Codes

- [`BasicStatus`](types/StatusCodes/LCamHdl_BasicStatus.md)
- [`AdvancedStatus`](types/StatusCodes/LCamHdl_AdvancedStatus.md)
- [`GetCamFollowingMinMaxStatus`](types/StatusCodes/LCamHdl_GetCamFollowingMinMaxStatus.md)

## Migration from TIA Portal

This library has been migrated from TIA Portal to SIMATIC AX. The functionality remains the same, but the programming model has been adapted to SIMATIC AX. Key differences include:

- Namespace: The library now uses the `Simatic.Ax.LCamHdl` namespace
- Data types: The data types have been adapted to SIMATIC AX conventions
- Error/Status handling: Error/Status handling has been adapted to use named value types

## Examples

### Creating a Basic Cam Profile

#### Configuration

```iec-st
USING Simatic.Ax.LCamHdl;
CONFIGURATION CamBasicConfiguration
    VAR_GLOBAL
        profileBasic : ARRAY[1..8] OF typeBasicPoint := [
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
            accelerationRatio := 0.0)];
    END_VAR
END_CONFIGURATION
```

#### Program

```iec-st
USING Simatic.Ax.LCamHdl;
USING Siemens.Simatic.S71500.MotionControl.Native;
PROGRAM CreateCamBasicProg
    VAR_EXTERNAL
        profileBasic : ARRAY[1..8] OF typeBasicPoint;
    END_VAR

    VAR_INPUT
        execute : BOOL;
        cam : DB_ANY;
    END_VAR

    VAR
        instCreateCamBasic : CreateCamBasic;
        camRef : REF_TO TO_Cam;
        initialCall : BOOL := FALSE;
    END_VAR
    IF NOT initialCall THEN
        camRef := AsCamRef(cam);
        initialCall := TRUE;
    END_IF;

    IF camRef <> NULL THEN
        instCreateCamBasic(
            execute := execute,
            camProfile := profileBasic,
            cam := camRef^);
    END_IF;

    // Check results
    IF createCamBasic.done THEN
        ;// Cam profile created successfully
    ELSIF createCamBasic.error THEN
        ;// Error occurred
    END_IF;
END_PROGRAM
```

### Creating a Cam Profile Based on XY Points

#### Configuration

```iec-st
USING Siemens.Simatic.S71500.MotionControl.Native;
CONFIGURATION XYPointConfiguration
    VAR_GLOBAL
        profileXY : ARRAY[1..16] OF TO_Cam_Struct_PointData := [
            (x := 0.0, y := 0.0),
            (x := 15.1351351351351, y := 0.25093172274086),
            (x := 32.7927927927928, y := 2.36276744454329),
            (x := 65.5855855855856, y := 16.2529424233088),
            (x := 76.7567567567567, y := 24.6856373693776),
            (x := 77.1171171171171, y := 24.9909075904853),
            (x := 102.342342342342, y := 51.4512818255899),
            (x := 233.153153153157, y := 274.020074851883),
            (x := 264.504504504509, y := 316.704148999998),
            (x := 314.594594594597, y := 354.074571519221),
            (x := 325.405405405408, y := 357.248162060316),
            (x := 339.459459459461, y := 359.387225922284),
            (x := 339.819819819821, y := 359.418005636778),
            (x := 340.180180180182, y := 359.447768527859),
            (x := 347.747747747749, y := 359.865226785287),
            (x := 360.0, y := 359.999999999999)
        ];
END_VAR

END_CONFIGURATION
```

#### Program

```iec-st
USING Simatic.Ax.LCamHdl;
USING Siemens.Simatic.S71500.MotionControl.Native;

PROGRAM CreateCamXYProg
    VAR_EXTERNAL
        profileXY : ARRAY[1..16] OF TO_Cam_Struct_PointData;
    END_VAR

    VAR_INPUT
        execute : BOOL;
        cam : DB_ANY;
    END_VAR

    VAR
        createCamBasedOnXYPoints : CreateCamBasedOnXYPoints;
        camRef : REF_TO TO_Cam;
        initialCall : BOOL := FALSE;
    END_VAR

    IF NOT initialCall THEN
        camRef := AsCamRef(cam);
        initialCall := TRUE;
    END_IF;

    IF camRef <> NULL THEN
        createCamBasedOnXYPoints(
            execute := execute,
            numberOfPoints := 16,
            camProfile := profileXY,
            cam := camRef^);
    END_IF;

    // Check results
    IF createCamBasedOnXYPoints.done THEN
        ;// Cam profile created successfully
    ELSIF createCamBasedOnXYPoints.error THEN
        ;// Error occurred
    END_IF;
END_PROGRAM
```
