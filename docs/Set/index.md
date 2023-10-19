---
title: Set
description: PSSv2.1/7.9.5 Sets
---

# Set {#set}

## Properties
- Unordered.
- Non-randomizable.
- *Element* can be any [*scalar*](../DataTypes/index.md#datatypes_scalar "e.g., `bit`, `int`, `bool`, `enum`, `string`, `float32`, `float64`, `chandle`") or [*aggregate*](../DataTypes/index.md#datatypes_aggregate "e.g., `array`, `list`, `map`, `set`, `struct`") of scalars.
- *Element*s must be unique.

## Declarations
=== "Without Initialization Assignment"
    ```sv linenums="1"
    set<bit [4] > nibbleSet;    //  nibbleSet: {}
    set<int     > intSet   ;    //  intSet   : {}
    set<bool    > boolSet  ;    //  boolSet  : {}
    set<string  > stringSet;    //  stringSet: {}
    set<float32 > floatSet ;    //  floatSet : {}
    set<eSTR2NUM> enumSet  ;    //  enumSet  : {} (1)
    ```

    1. Assume defined enum type before
    ```sv linenums="1"
    enum eSTR2NUM {
        ZERO, ONE, TWO
    };
    ```

=== "With Initialization Assignment"
    ```sv linenums="1"
    set<bit [4] > nibbleSet = {4'b0001, 4'b0010};
    set<int     > intSet    = {      1, 2      };
    set<bool    > boolSet   = {  false, true   };
    set<string  > stringSet = {    "1", "2"    };
    set<float32 > floatSet  = {    1.0, 2.0    };
    set<eSTR2NUM> enumSet   = {    ONE, TWO    };   // (1)!
    ```

    1. Assume defined enum type before
    ```sv linenums="1"
    enum eSTR2NUM {
        ZERO, ONE, TWO
    };
    ```

## Set Operators
| Operator                                                                  | Description                                                                                                                                   |
| :------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| [`=`](Operators.md#set_operators_assignment "Assignment operator `=`")    | Creates a copy of the set-type expression on the RHS and assigns it to the set on the LHS.                                                    |
| [`==`](Operators.md#set_operators_equality "Equality operator `==`")      | Evaluates to *true* if all elements are equal.                                                                                                |
| [`!=`](Operators.md#set_operators_inequality "Inequality operator `!=`")  | Evaluates to *true* if not all elements are equal.                                                                                            |
| [`in`](Operators.md#set_operators_in "Set membership operator `in`")      | It evaluates to *true* if the element specified on the left of the operator exists in the **set** collection on the right of the operator.    |
| [`foreach`](Operators.md#set_operators_foreach "`foreach` statement")     | The foreach statement can be applied to a set to iterate over the set elements.                                                               |

## Set Methods
| Method                                                                                                            | Description                                                       |
| :---------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| [int `size()`](Methods.md#set_methods_size "function int `size()`")                                               | Returns the number of elements in the set.                        |
| [`clear()`](Methods.md#set_methods_clear "function void `clear()`")                                               | Removes all elements.                                             |
| [`delete(data_type element)`](Methods.md#set_methods_delete "function void `delete(data_type element)`")          | Removes the specified element.                                    |
| [`insert(data_type element)`](Methods.md#set_methods_insert "function void `insert(data_type element)`")          | Adds the specified element.                                       |
| [list&lt;data_type&gt; `to_list()`](Methods.md#set_methods_to_list "function list&lt;data_type&gt; `to_list()`")  | Returns all elements in a [`list`](../List/index.md#list)-type.   |
