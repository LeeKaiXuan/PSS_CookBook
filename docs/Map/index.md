---
title: Map
description: PSSv2.1/7.9.4. Maps
---

# Map

## Properties
- Unordered.
- Non-randomizable.
- Elements can be added or removed within `exec` blocks.
- *Key* and *element* can be any [*scalar*](../DataTypes/index.md#datatypes_scalar "e.g., `bit`, `int`, `bool`, `enum`, `string`, `float32`, `float64`, `chandle`") or [*aggregate*](../DataTypes/index.md#datatypes_aggregate "e.g., `array`, `list`, `map`, `set`, `struct`") of scalars.
- *Key*s must be unique.

## Declarations
=== "Without Initialization Assignment"
    ```sv linenums="1"
    map<bit [4], int   > nibble2int ;   //  nibble2int : {}
    map<int    , bool  > int2bool   ;   //  int2bool   : {}
    map<bool   , string> bool2string;   //  bool2string: {}
    ```

    1. Assume defined enum type before
    ```sv linenums="1"
    enum eSTR2NUM {
        ZERO, ONE, TWO
    };
    ```

    2. Assume defined struct type before
    ```sv linenums="1"
    struct sSTR2NUM {
        string stringVal;
        int intVal;
    };
    ```


=== "With Initialization Assignment"
    ```sv linenums="1"
    map<bit [4], int   > nibble2int  = {4'b1110:3      , 4'b0110:2     };   //  nibble2int : {} -> {4'b1110:3, 4'b0110:2}
    map<int    , bool  > int2bool    = {      4:true   ,       5:false };   //  int2bool   : {} -> {4:true        , 5:false       }
    map<bool   , string> bool2string = {  false:"FALSE",    true:"TRUE"};   //  bool2string: {} -> {false:"FALSE" , true:"TRUE"   }
    ```

    1. Assume defined enum type before
    ```sv linenums="1"
    enum eSTR2NUM {
        ZERO, ONE, TWO
    };
    ```

    2. Assume defined struct type before
    ```sv linenums="1"
    struct sSTR2NUM {
        string stringVal;
        int intVal;
    };
    ```

## Map Operators
| Operator                                                                  | Description                                                                                   |
| :------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------- |
| [`[]`](Operators.md#map_operators_index "Index operator `[]`")            | Used to access a specific element of a map.                                                   |
| [`=`](Operators.md#map_operators_assignment "Assignment operator `=`")    | Creates a copy of the map-type expression on the RHS and assigns it to the map on the LHS.    |
| [`==`](Operators.md#map_operators_equality "Equality operator `==`")      | Evaluates to *true* if all elements with corresponding keys are equal.                        |
| [`!=`](Operators.md#map_operators_inequality "Inequality operator `!=`")  | Evaluates to *true* if not all elements with corresponding keys are equal.                    |
| [`foreach`](Operators.md#map_operators_foreach "`foreach` statement")     | The foreach statement can be applied to a map to iterate over the map elements.               |


## Map Methods
| Method                                                                                                        | Description                                                       |
| :------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------- |
| [int `size()`](Methods.md#map_methods_size "function int `size()`")                                           | Returns the number of elements in the map.                        |
| [`clear()`](Methods.md#map_methods_clear "function void `clear()`")                                           | Removes all elements.                                             |
| [&lt;data_type&gt; `delete(key)`](Methods.md#map_methods_delete "function &lt;data_type&gt; `delete(key)`")   | Move out element with the specified key.                          |
| [`insert(key, element)`](Methods.md#map_methods_insert "function `insert(key, element)`")                     | Add or replace element with the specified key.                    |
| [set&lt;data_type&gt; `keys()`](Methods.md#map_methods_keys "function set&lt;data_type&gt; `keys()`")         | Returns all keys in a `set`-type.                                 |
| [list&lt;data_type&gt; `values()`](Methods.md#map_methods_keys "function list&lt;data_type&gt; `values()`")   | Returns all elements in a [`list`](../List/index.md#list)-type.   |
