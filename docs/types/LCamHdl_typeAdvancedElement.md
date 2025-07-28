# LCamHdl_typeAdvancedElement

| Member | Type | Default Value | Description |
|--------|------|---------------|-------------|
| `leadingValueStart` | `LREAL` | - | Leading value at the beginning of the element |
| `leadingValueEnd` | `LREAL` | - | Leading value at the end of the element |
| `followingValueStart` | `LREAL` | - | Following value at the beginning of the element |
| `followingValueEnd` | `LREAL` | - | Following value at the end of the element |
| `geoVeloStart` | `LREAL` | - | Velocity at the beginning of the element (real – not standardized) |
| `geoVeloEnd` | `LREAL` | - | Velocity at the end of the element (real – not standardized) |
| `geoAccelStart` | `LREAL` | - | Acceleration at the beginning of the element (real – not standardized) |
| `geoAccelEnd` | `LREAL` | - | Acceleration at the end of the element (real – not standardized) |
| `geoJerkStart` | `LREAL` | - | Jerk at the beginning of the element (real – not standardized) |
| `geoJerkEnd` | `LREAL` | - | Jerk at the end of the element (real – not standardized) |
| `inflectionPointParameter` | `LREAL` | `0.5` | Inflection point parameter (λ) – default: 0.5 standardized |
| `modVeloTrapezoidParameter` | `LREAL` | `1.0` | Element parameter (c) – sine-straight line- combination standardized |
| `modSineMaxAccelCaStar` | `LREAL` | - | Special case of modified sine – Presetting by Ca* standardized |
| `camProfileType` | `DINT` | `0` | Profile type of the cam disk element, 0: LCAMHDL_PROFILE_EMPTY (default) |
