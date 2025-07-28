# LCamHdl_AdditionalConstants

## Description

The `LCamHdl_AdditionalConstants` type defines constants used to specify configuration modes for advanced mathematical profile elements in the LCamHdl library. These constants control how sine, polynomial, and other mathematical functions are parameterized when creating complex cam profiles.

## Constant Categories

### Sine Mode Constants

These constants define how sine function parameters are specified when adding sine elements to cam profiles.

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_SINE_MODE_PHASE_START_AND_END` | 0 | Sine mode: Phase at start and at end |
| `LCAMHDL_SINE_MODE_PHASE_START_AND_PERIOD_LENGTH` | 1 | Sine mode: Phase at start and period length |
| `LCAMHDL_SINE_MODE_PHASE_START_AND_FREQUENCY` | 2 | Sine mode: Phase at start and frequency |
| `LCAMHDL_SINE_MODE_PERIOD_LENGTH_AND_PHASE_END` | 3 | Sine mode: Period length and phase at end |
| `LCAMHDL_SINE_MODE_FREQUENCY_AND_PHASE_END` | 4 | Sine mode: Frequency and phase at end |

### Sine Inclination Mode Constants

These constants specify how inclined sine functions are parameterized, controlling the displacement and inclination characteristics.

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_SINE_INCL_MODE_DISPLACEMENT_START_AND_END` | 0 | Sine inclination mode: Displacement at start and end |
| `LCAMHDL_SINE_INCL_MODE_DISPLACEMENT_START_AND_INCLINATION` | 1 | Sine inclination mode: Displacement at start and inclination |
| `LCAMHDL_SINE_INCL_MODE_INCLINATION_AND_DISPLACEMENT_END` | 2 | Sine inclination mode: Inclination and displacement at end |

### Polynomial Mode Constants

These constants define how polynomial functions are specified, controlling the mathematical constraints used to define the polynomial coefficients.

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_POLY_MODE_BOUNDARY_VALUES_AND_POINT_OF_INFLECTION` | 0 | Polynomial definition by boundary values and point of inflection |
| `LCAMHDL_POLY_MODE_BOUNDARY_VALUES_AND_START_JERK` | 1 | Polynomial definition by boundary values and start jerk |
| `LCAMHDL_POLY_MODE_BOUNDARY_VALUES_AND_END_JERK` | 2 | Polynomial definition by boundary values and end jerk |

## Usage

These constants are primarily used with advanced cam element functions to specify how mathematical parameters should be interpreted:

### Sine Functions

- Used with [`LCamHdl_AddCamSine`](../function-blocks/LCamHdl_AddCamSine.md), [`LCamHdl_AddCamInvSine`](../function-blocks/LCamHdl_AddCamInvSine.md), [`LCamHdl_AddCam10kSine`](../function-blocks/LCamHdl_AddCam10kSine.md) and [`LCamHdl_AddCam10kInvSine`](../function-blocks/LCamHdl_AddCam10kInvSine.md)
- Control how phase, frequency, and period parameters are specified

### Polynomial Functions

- Used with [`LCamHdl_AddCamPolynomial`](../function-blocks/LCamHdl_AddCamPolynomial.md) / [`LCamHdl_AddCam10kPolynomial`](../function-blocks/LCamHdl_AddCam10kPolynomial.md)
- Define mathematical constraints for polynomial coefficient calculation
- Control jerk characteristics and inflection points
