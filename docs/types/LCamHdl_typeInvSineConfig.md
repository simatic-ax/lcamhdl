# LCamHdl_typeInvSineConfig

| Member | Type | Default Value | Description |
|--------|------|---------------|-------------|
| `deletePrecedingCamPointData` | `DINT` | `0` | Delete preceding cam point data<br/>• `0`: Delete no data<br/>• `1`: Delete until first invalid data found<br/>• `2`: Delete all data |
| `deleteSuccessiveCamPointData` | `DINT` | `1` | Delete successive cam point data<br/>• `0`: Delete no data<br/>• `1`: Delete until first invalid data found<br/>• `2`: Delete all data |
| `deleteCamSegmentData` | `DINT` | `0` | Delete cam segment data<br/>• `0`: Delete no data<br/>• `1`: Delete until first invalid data found<br/>• `2`: Delete all data |
| `interpolateCam` | `BOOL` | `TRUE` | Interpolation control<br/>• `TRUE`: Interpolate cam<br/>• `FALSE`: Do not interpolate cam |
