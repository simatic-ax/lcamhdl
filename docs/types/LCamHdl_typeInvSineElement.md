# LCamHdl_typeInvSineElement

| Member | Type | Default Value | Description |
|--------|------|---------------|-------------|
| `numberOfInterpolationPoints` | `INT` | `32` | Approximation - number of interpolation points |
| `leadingValueStart` | `LREAL` | `0.0` | Leading value at the beginning of the element |
| `leadingValueEnd` | `LREAL` | `0.0` | Leading value at the end of the element |
| `followingValueMin` | `LREAL` | `0.0` | Following value minimum |
| `followingValueMax` | `LREAL` | `0.0` | Following value maximum |
| `definitionRangeStart` | `LREAL` | `-0.95` | Start point in the definition range of the arcsine function that is to be used |
| `definitionRangeEnd` | `LREAL` | `0.95` | End point in the definition range of the arcsine function that is to be used |
| `mirrored` | `BOOL` | `FALSE` | Select whether or not the inverse sine is to be mirrored about the abscissa |
| `camProfileType` | `DINT` | `55` | Profile type of the cam disk element, 55: `LCAMHDL_ADD_PROFILE_INVERSE_SINE` (default) |
