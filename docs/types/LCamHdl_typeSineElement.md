# LCamHdl_typeSineElement

| Member | Type | Default Value | Description |
|--------|------|---------------|-------------|
| `leadingValueStart` | `LREAL` | `0.0` | Leading value at the beginning of the element |
| `leadingValueEnd` | `LREAL` | `0.0` | Leading value at the end of the element |
| `amplitude` | `LREAL` | `0.0` | Sine amplitude |
| `periodLength` | `LREAL` | `0.0` | Sine period length |
| `frequency` | `LREAL` | `0.0` | Sine frequency |
| `phaseStart` | `LREAL` | `0.0` | Phase at start |
| `phaseEnd` | `LREAL` | `0.0` | Phase at end |
| `inclination` | `LREAL` | `0.0` | Inclination of inclined sine |
| `displacementStart` | `LREAL` | `0.0` | Oscillation midpoint offset of the sine element / Displacement at start of the inclined sine |
| `displacementEnd` | `LREAL` | `0.0` | Displacement at end of the inclined sine - only inclined sine |
| `camProfileType` | `DINT` | `51` | Profile type of the cam disk element, 51: `LCAMHDL_ADD_PROFILE_SINE` (default) |
| `sineMode` | `DINT` | `0` | Profile mode, 0: `LCAMHDL_SINE_MODE_PHASE_START_AND_END` (default) |
| `inclinationMode` | `DINT` | `0` | Inclination mode, 0: `LCAMHDL_SINE_INCL_MODE_DISPLACEMENT_START_AND_END` (default) |
