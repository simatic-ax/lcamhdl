# LCamHdl_ConfigConstants

## Description

The `LCamHdl_ConfigConstants` type defines constants used for configuration options in the LCamHdl library. These constants are primarily used to specify deletion options when working with cam profiles.

## Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `LCAMHDL_DELETE_NO_DATA` | 0 | Cam data delete option: No deletion |
| `LCAMHDL_DELETE_DATA_UNTIL_FIRST_INVALID_DATA_FOUND` | 1 | Cam data delete option: Delete respective data until first invalid data is found |
| `LCAMHDL_DELETE_ALL_DATA` | 2 | Cam data delete option: Delete all respective data |

## Usage

These constants are used in function blocks that modify cam profiles to specify how existing data should be handled. For example, when adding new elements to a cam profile, you can specify whether to:

- Keep all existing data (`LCAMHDL_DELETE_NO_DATA`)
- Delete data until the first invalid data is found (`LCAMHDL_DELETE_DATA_UNTIL_FIRST_INVALID_DATA_FOUND`)
- Delete all existing data (`LCAMHDL_DELETE_ALL_DATA`)
