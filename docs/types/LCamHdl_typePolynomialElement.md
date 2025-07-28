# LCamHdl_typePolynomialElement

| Member | Type | Default Value | Description |
|--------|------|---------------|-------------|
| `leadingValueStart` | `LREAL` | `0.0` | Leading value at the beginning of the element |
| `leadingValueEnd` | `LREAL` | `0.0` | Leading value at the end of the element |
| `followingValueStart` | `LREAL` | `0.0` | Following value at the beginning of the element |
| `followingValueEnd` | `LREAL` | `0.0` | Following value at the end of the element |
| `geoVeloStart` | `LREAL` | `0.0` | Velocity at the beginning of the element (real – not standardized) |
| `geoVeloEnd` | `LREAL` | `0.0` | Velocity at the end of the element (real – not standardized) |
| `geoAccelStart` | `LREAL` | `0.0` | Acceleration at the beginning of the element (real – not standardized) |
| `geoAccelEnd` | `LREAL` | `0.0` | Acceleration at the end of the element (real – not standardized) |
| `geoJerkStart` | `LREAL` | `0.0` | Jerk at the beginning of the element (real – not standardized) |
| `geoJerkEnd` | `LREAL` | `0.0` | Jerk at the end of the element (real – not standardized) |
| `inflectionPointParameter` | `LREAL` | `0.5` | Inflection point parameter (λ) – default: 0.5 standardized |
| `amplitude` | `LREAL` | `0.0` | Sine amplitude |
| `periodLength` | `LREAL` | `0.0` | Sine period length |
| `frequency` | `LREAL` | `0.0` | Sine frequency |
| `phaseStart` | `LREAL` | `0.0` | Sine phase at start |
| `phaseEnd` | `LREAL` | `0.0` | Sine phase at end |
| `camProfileType` | `DINT` | `45` | Profile type of the cam disk element, 45: `LCAMHDL_ADD_PROFILE_POLY_TRIGONOMETRIC` (default) |
| `polynomialMode` | `DINT` | `0` | Polynomial mode, 0: `LCAMHDL_POLY_MODE_BOUNDARY_VALUES_AND_POINT_OF_INFLECTION` (default) |
| `sineMode` | `DINT` | `0` | Sine mode, 0: `LCAMHDL_SINE_MODE_PHASE_START_AND_END` (default) |
