# LCamHdl_ProfileConstants

## Description

The `LCamHdl_ProfileConstants` type defines constants used to identify different cam profile types in the LCamHdl library.

## Profile Type Categories

### Basic Profile Types

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_PROFILE_EMPTY` | 0 | Cam profile: Empty |
| `LCAMHDL_PROFILE_POINT` | 1 | Cam profile: Single point |
| `LCAMHDL_PROFILE_DWELL` | 2 | Cam profile: Dwell |
| `LCAMHDL_PROFILE_CONST_VELO` | 3 | Cam profile: Constant velocity |

### Polynomial Profile Types

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_PROFILE_POLY_3` | 4 | Cam profile: 3rd degree polynomial |
| `LCAMHDL_PROFILE_POLY_4` | 30 | Cam profile: 4th degree polynomial |
| `LCAMHDL_PROFILE_POLY_5` | 5 | Cam profile: 5th degree polynomial |
| `LCAMHDL_PROFILE_POLY_6` | 35 | Cam profile: 6th degree polynomial |
| `LCAMHDL_PROFILE_POLY_7` | 6 | Cam profile: 7th degree polynomial - implemented using two 6th degree polynomials |

### Parabolic Profile Types

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_PROFILE_D_D_PARABOLA` | 7 | Cam profile: Dwell → dwell - quadratic parabola |
| `LCAMHDL_PROFILE_C_C_PARABOLA` | 8 | Cam profile: Constant velocity → constant velocity - quadratic parabola |

### Sine-Based Profile Types

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_PROFILE_D_D_BASIC_SINE` | 9 | Cam profile: Dwell → dwell - basic sine line |
| `LCAMHDL_PROFILE_D_D_INCLINED_SINE` | 10 | Cam profile: Dwell → dwell - inclined sine line |
| `LCAMHDL_PROFILE_D_D_MOD_SINE` | 12 | Cam profile: Dwell → dwell - modified sine line |
| `LCAMHDL_PROFILE_C_C_MOD_SINE` | 13 | Cam profile: Constant velocity → constant velocity - modified sine line |
| `LCAMHDL_PROFILE_R_R_BASIC_SINE` | 15 | Cam profile: Reversal → reversal - basic sine line |
| `LCAMHDL_PROFILE_D_C_MOD_SINE` | 16 | Cam profile: Dwell → constant velocity - modified sine line |
| `LCAMHDL_PROFILE_C_D_MOD_SINE` | 17 | Cam profile: Constant velocity → dwell - modified sine line |

### Trapezoid Profile Types

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_PROFILE_D_D_MOD_ACCEL_TRAPEZOID` | 11 | Cam profile: Dwell → dwell - modified acceleration trapezoid |
| `LCAMHDL_PROFILE_R_R_MOD_VELO_TRAPEZOID` | 14 | Cam profile: Reversal → reversal - sine-straight line - combination |
| `LCAMHDL_PROFILE_D_R_MOD_ACCEL_TRAPEZOID` | 18 | Cam profile: Dwell → reversal - modified acceleration trapezoid |
| `LCAMHDL_PROFILE_R_D_MOD_ACCEL_TRAPEZOID` | 19 | Cam profile: Reversal → dwell - modified acceleration trapezoid |

### Harmonic Combination Profile Types

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_PROFILE_D_R_HARMONIC_COMBINATION` | 20 | Cam profile: Dwell → reversal - harmonic combination |
| `LCAMHDL_PROFILE_R_D_HARMONIC_COMBINATION` | 21 | Cam profile: Reversal → dwell - harmonic combination |
| `LCAMHDL_PROFILE_C_R_HARMONIC_COMBINATION` | 22 | Cam profile: Constant velocity → reversal - harmonic combination |
| `LCAMHDL_PROFILE_R_C_HARMONIC_COMBINATION` | 23 | Cam profile: Reversal → constant velocity - harmonic combination |

### Additional Profile Types for Advanced Elements

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_ADD_PROFILE_POLY` | 44 | Cam profile for additional blocks: Polynomial |
| `LCAMHDL_ADD_PROFILE_POLY_TRIGONOMETRIC` | 45 | Cam profile for additional blocks: Polynomial with trigonometric portion |
| `LCAMHDL_ADD_PROFILE_SINE` | 51 | Cam profile for additional blocks: Sine |
| `LCAMHDL_ADD_PROFILE_INCLINED_SINE` | 52 | Cam profile for additional blocks: Inclined sine |
| `LCAMHDL_ADD_PROFILE_INVERSE_SINE` | 55 | Cam profile for additional blocks: Inverse sine |
| `LCAMHDL_ADD_PROFILE_D_R_DOUBLE_HARMONIC` | 60 | Cam profile for additional blocks: Dwell → reversal - double harmonic |
| `LCAMHDL_ADD_PROFILE_R_D_DOUBLE_HARMONIC` | 61 | Cam profile for additional blocks: Reversal → dwell - double harmonic |

## Usage

These constants are used throughout the LCamHdl library to specify the type of mathematical profile to be applied to cam segments.

### Profile Type Notation

The naming convention follows a pattern that indicates the transition characteristics:

- **D**: Dwell (zero velocity)
- **C**: Constant velocity
- **R**: Reversal (velocity direction change)

For example, `LCAMHDL_PROFILE_D_C_MOD_SINE` represents a modified sine profile that transitions from dwell to constant velocity.
