# LCamHdl Library for SIMATIC AX

## Overview

The LCamHdl library provides functionality for creating cam disks at runtime in SIMATIC AX applications.

Cam disks are used in motion control applications to define the relationship between a leading axis (master) and a following axis (slave). The library provides various methods to create and analyze cam profiles with different mathematical approaches.

The library is a direct conversion of the functionally identical library [LCamHdl](https://support.industry.siemens.com/cs/document/105644659) for use inside the TIA Portal

## Key Features

- Create cam profiles based on XY points
- Create basic cam profiles with polynomial segments
- Create advanced cam profiles with various mathematical functions:
  - Sine
  - Inverse sine
  - Double harmonic
  - Polynomial
- Support for both standard `TO_Cam` profiles and `TO_Cam_10k` profiles
- Analyze cam profiles for:
  - Min/max following values
  - Maximum slave dynamics
  - Maximum master velocity
  - Status information

## Requirements

- SIMATIC AX
- S7-1500T CPU with firmware version 2.9 or higher

## Installation

Install with Apax:

```cli
apax add @simatic-ax/lcamhdl
```

## Namespace

```cli
Simatic.Ax.LCamHdl;
```

## Documentation

Comprehensive documentation is available in the [docs](./docs) directory:

## Example

```iec-st
USING Simatic.Ax.LCamHdl;
USING Siemens.Simatic.S71500.MotionControl.Native;

PROGRAM Main
VAR
    camProfile : ARRAY[1..5] OF LCamHdl_typeBasicPoint;
    cam : REF_TO TO_Cam;
    createCamBasic : LCamHdl_CreateCamBasic;
    execute : BOOL;
END_VAR

// Initialize cam profile points
camProfile[1].leadingValue := 0.0;
camProfile[1].followingValue := 0.0;
camProfile[1].velocityRatio := 0.0;
camProfile[1].accelerationRatio := 0.0;

camProfile[2].leadingValue := 0.25;
camProfile[2].followingValue := 0.5;
camProfile[2].velocityRatio := 2.0;
camProfile[2].accelerationRatio := 0.0;

camProfile[3].leadingValue := 0.5;
camProfile[3].followingValue := 1.0;
camProfile[3].velocityRatio := 0.0;
camProfile[3].accelerationRatio := -8.0;

camProfile[4].leadingValue := 0.75;
camProfile[4].followingValue := 0.5;
camProfile[4].velocityRatio := -2.0;
camProfile[4].accelerationRatio := 0.0;

camProfile[5].leadingValue := 1.0;
camProfile[5].followingValue := 0.0;
camProfile[5].velocityRatio := 0.0;
camProfile[5].accelerationRatio := 0.0;

// Create cam profile
createCamBasic(
    execute := execute,
    numberOfPoints := 5,
    camProfile := camProfile,
    cam := cam^
);

// Check results
IF createCamBasic.done THEN
    // Cam profile created successfully
ELSIF createCamBasic.error THEN
    // Error occurred, check status and diagnostics
END_IF;
END_PROGRAM
```

## Contribution

Thanks for your interest in contributing. Anybody is free to report bugs, unclear documentation, and other problems regarding this repository in the Issues section

## License and Legal information

Please read the [Legal information](./LICENSE.md)
