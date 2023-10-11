---
title: Numeric Types
description: 8.2 Numeric types
---

# Numeric Types
## Bit {#datatypes_numerictypes_bit}
`bit` is a numeric data type with default properties: **unsigned**, **1-bit** width, **{0, 1}** domain.

### Declare a bit:
```sv linenums="1"
bit singleBit;
```

### Declare **8-bits** wide `bit` type:
Possible values specified by bit width are **{0..(2^width^-1)}**
=== "single bound"
    ```sv linenums="1"
    bit [8] singleByte;     //  possible values: {0..127};
    ```

=== "dual bound"
    ```sv linenums="1"
    bit [7:0] singleByte;   //  possible values: {0..127};
    ```

    !!! note "lower bound must be `0`"

!!! warning "**dual bounds** may be removed in future version"

### Declared with specified value domain:
Values of variable are within intersection of possible values by width and value domain.
```sv linenums="1"
bit [8] in [0, 1, 5]             singleByte;    //  value domain: {0, 1, 5}
bit [8] in [..2]                 singleByte;    //  value domain: {0, 1, 2}
bit [8] in [6..8]                singleByte;    //  value domain: {6, 7, 8}
bit [8] in [254..]               singleByte;    //  value domain: {254, 255}
bit [8] in [5, ..2, 6..8, 254..] singleByte;    //  value domain: {0, 1, 2, 5, 6, 7, 8, 254, 255}
```

!!! tip
    Specify value domain is useful for random variable. Following examples are equalize:
    === "value domain within declaration"
        ```sv linenums="1"
        rand bit [8] in [5, ..2, 6..8, 253..] singleByte;
        ```

    === "value domain within `constraint`"
        ```sv linenums="1"
        rand bit [8] singleByte;
        constraint {
            singleByte in [5, ..2, 6..8, 253..];
        }
        ```

## Integer {#datatypes_numerictypes_integer}
`int` is a numeric data type with default properties: **signed**, **32-bits** width, **{-2^31^..(2^31^-1)}** domain.

### Declare an integer:
```sv linenums="1"
int int32;
```

### Declare **8-bits** wide `int` type:
Possible values specified by bit width are **{-2^width-1^..(2^width-1^-1)}**
=== "single bound"
    ```sv linenums="1"
    int [8] int8;       //  possible values: {-128..127}
    ```

=== "dual bound"
    ```sv linenums="1"
    int [7:0] int8;     //  possible values: {-128..127}
    ```

    !!! note "lower bound must be `0`"

!!! warning "**dual bounds** may be removed in future version"

### Declared with specified value domain:
Values of variable are within intersection of possible values by width and value domain.
```sv linenums="1"
int [8] in [0, 1, 5]                  int8; //  value domain: {0, 1, 5}
int [8] in [..(-127)]                 int8; //  value domain: {-128, -127}
int [8] in [6..8]                     int8; //  value domain: {6, 7, 8}
int [8] in [126..]                    int8; //  value domain: {126, 127}
int [8] in [5, ..(-127), 6..8, 253..] int8; //  value domain: {-128, -127, 5, 6, 7, 8, 126, 127}
```

!!! tip
    Specify value domain is useful for random variable. Following examples are equalize:
    === "value domain within declaration"
        ```sv linenums="1"
        rand int [8] in [5, ..(-127), 6..8, 253..] int8;
        ```

    === "value domain within `constraint`"
        ```sv linenums="1"
        rand int [8] int8;
        constraint {
            int8 in [5, ..(-127), 6..8, 253..];
        }
        ```
