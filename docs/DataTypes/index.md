---
title: Data Types
description: PSSv2.1/7. Data types
---

# Data Types

## *Scalar* Type {#datatypes_scalar}
| Scalar Type                                                                                   | Randomizable          |
| :-------------------------------------------------------------------------------------------- | :-------------------: |
| [`bit`](IntegerTypes.md#datatypes_integertypes_bit "bit")                                     | :white_check_mark:    |
| [`int`](IntegerTypes.md#datatypes_integertypes_integer "integer")                             | :white_check_mark:    |
| `bool`                                                                                        | :white_check_mark:    |
| `enum`                                                                                        | :white_check_mark:    |
| `string`                                                                                      | :white_check_mark:    |
| `float32`<br>[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")    |                       |
| `float64`<br>[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")    |                       |
| `chandle`                                                                                     |                       |

## *Aggregate* {#datatypes_aggregate}
| Aggregate Type                        | Randomizable                                                                                                                                          |
| :------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`array`](../Array/index.md#array)    | :white_check_mark: Only for `bit`, `int`, `bool`, `enum`, `string`                                                                                    |
| [`list`](../List/index.md#list)       | :white_check_mark: Only for `bit`, `int`, `bool`, `enum`, `string`<br>[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")   |
| [`map`](../Map/index.md#map)          |                                                                                                                                                       |
| `set`                                 |                                                                                                                                                       |
| `struct`                              | :white_check_mark: Only for `bit`, `int`, `bool`, `enum`, `string`                                                                                    |

!!! Note "*Aggregate* may be nested."

## *Non-aggregate* {#datatypes_non_aggregate}
- `component`
- `action`
- `buffer`
- `stream`
- `state`
- `resource`
