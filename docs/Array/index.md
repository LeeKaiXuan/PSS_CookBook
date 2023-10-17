---
title: Array
description: PSSv2.1/7.9.2 Arrays
---

# Array {#array}

## Declarations
Array has 2 types of declare syntaxes: `Template`, `Square`.
=== "Template"
    ```sv linenums="1"
    array<int    , 3> intArray   ;  //  declare integer array with 3 elements
    array<bit [8], 3> byteArray  ;  //  declare byte array with 3 elements
    array<string , 3> stringArray;  //  declare string array with 3 elements
    array<array<int, 3>, 2> nestedArray;    //  declare nested array with 3x2 integer elements
    ```

=== "Square"
    ```sv linenums="1" hl_lines="4"
    int     intArray    [3];        //  declare integer array with 3 elements
    bit [8] byteArray   [3];        //  declare byte array with 3 elements
    string  stringArray [3];        //  declare string array with 3 elements
    // (1)!
    ```

    1. `square` not support for declare nested array

Declare array by `rand` keyword:
=== "Template"
    ```sv linenums="1"
    rand array<int, 3> intArray;    //  declare integer array with 3 random elements
    ```

=== "Square"
    ```sv linenums="1"
    rand int intArray [3];          //  declare integer array with 3 random elements
    ```

## Array Operators
| Operator                                                                      | Description                                                                                                                                   |
| :---------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| [`[]`](Operators.md#array_operators_index "Index operator `[]`")              | Used to access a specific element of an array.                                                                                                |
| [`=`](Operators.md#array_operators_assignment "Assignment operator `=`")      | Creates a copy of the array-type expression on the RHS and assigns it to the array on the LHS.                                                |
| [`==`](Operators.md#array_operators_equality "Equality operator `==`")        | Evaluates to *true* if all elements with corresponding indexes are equal.                                                                     |
| [`!=`](Operators.md#array_operators_inequality "Inequality operator `!=`")    | Evaluates to *true* if not all elements with corresponding indexes are equal.                                                                 |
| [`in`](Operators.md#array_operators_in "Set membership operator `in`")        | It evaluates to *true* if the element specified on the left of the operator exists in the **array** collection on the right of the operator.  |
| [`foreach`](Operators.md#array_operators_foreach "`foreach` statement")       | The foreach statement can be applied to an array to iterate over the array elements.                                                          |

## Array Methods
| Method                                                                                                                | Description                                                       |
| :-------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| [int `size()`](Methods.md#array_methods_size "function int `size()`")                                                 | Returns the number of elements in the arrays.                     |
| [int `sum()`](Methods.md#array_methods_sum "function int `sum()`")                                                    | Returns the sum of all elements currently stored in the array.    |
| [list&lt;data_type&gt; `to_list()`](Methods.md#array_methods_to_list "function list&lt;data_type&gt; `to_list()`")    | Returns all elements in a [`list`](../List/index.md#list)-type.   |
| [set&lt;data_type&gt; `to_set()`:](Methods.md#array_methods_to_set "function set&lt;data_type&gt; `to_set()`")        | Returns all elements in a `set`-type.                             |
