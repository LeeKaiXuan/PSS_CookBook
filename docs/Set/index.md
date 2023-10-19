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
| Operator                                                      | Description                                                                                                                                   |
| :------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| [`=`](index.md#set_assignment "Assignment operator `=`")      | Creates a copy of the set-type expression on the RHS and assigns it to the set on the LHS.                                                    |
| [`==`](index.md#set_equality "Equality operator `==`")        | Evaluates to *true* if all elements are equal.                                                                                                |
| [`!=`](index.md#set_inequality "Inequality operator `!=`")    | Evaluates to *true* if not all elements are equal.                                                                                            |
| [`in`](index.md#set_in "Set membership operator `in`")        | It evaluates to *true* if the element specified on the left of the operator exists in the **set** collection on the right of the operator.    |
| [`foreach`](index.md#set_foreach "`foreach` statement")       | The foreach statement can be applied to a set to iterate over the set elements.                                                               |

## Set Methods
| Method                                                                                                    | Description                                                       |
| :-------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| [int `size()`](index.md#set_size "function int `size()`")                                                 | Returns the number of elements in the set.                        |
| [`clear()`](index.md#set_clear "function void `clear()`")                                                 | Removes all elements.                                             |
| [`delete(data_type element)`](index.md#set_delete "function void `delete(data_type element)`")            | Removes the specified element.                                    |
| [`insert(data_type element)`](index.md#set_insert "function void `insert(data_type element)`")            | Adds the specified element.                                       |
| [list&lt;data_type&gt; `to_list()`](index.md#set_to_list "function list&lt;data_type&gt; `to_list()`")    | Returns all elements in a [`list`](../List/index.md#list)-type.   |

---

## Assignment operator `=` {#set_assignment}
```sv linenums="1"
set<int> intSet;

intSet = {1, 2};    //  intSet: {}     -> {1, 2}
intSet = {3, 3, 4}; //  intSet: {1, 2} -> {3, 4} (1)
```

1. Same element will appear only once.

## Equality operator `==` {#set_equality}
```sv linenums="1"
set<int   > set_0 = { 1 ,  2      };
set<int   > set_1 = { 2 ,  1      };
set<int   > set_2 = { 1 ,  2 ,  3 };
set<string> set_3 = {"1", "2"     };

bit bitVal_0, bitVal_1, bitVal_2, bitVal_3;
if (set_0 == set_0) bitVal_0 = 1;   //  bitVal_0: 0 -> 1 (1)
if (set_0 == set_1) bitVal_1 = 1;   //  bitVal_1: 0 -> 1 (2)
if (set_0 == set_2) bitVal_2 = 1;   //  bitVal_2: 0 -> 0 (3)
if (set_0 == set_3) bitVal_3 = 1;   //  bitVal_3: 0 -> 0 (4)
```

1. Equalize **size**, **type**, and all elements.
2. Equalize **size**, **type**, and all elements in different order.
3. Inequalize **size**.
4. Inequalize **type**.

## Inequality operator `!=` {#set_inequality}
```sv linenums="1"
set<int   > set_0 = { 1 ,  2      };
set<int   > set_1 = { 2 ,  1      };
set<int   > set_2 = { 1 ,  2 ,  3 };
set<string> set_3 = {"1", "2"     };

bit bitVal_0, bitVal_1, bitVal_2, bitVal_3;
if (set_0 != set_0) bitVal_0 = 1;   //  bitVal_0: 0 -> 0 (1)
if (set_0 != set_1) bitVal_1 = 1;   //  bitVal_1: 0 -> 0 (2)
if (set_0 != set_2) bitVal_2 = 1;   //  bitVal_2: 0 -> 1 (3)
if (set_0 != set_3) bitVal_3 = 1;   //  bitVal_3: 0 -> 1 (4)
```

1. Equalize **size**, **type**, and all elements.
2. Equalize **size**, **type**, and all elements in different order.
3. Inequalize **size**.
4. Inequalize **type**.

## Set membership operator `in` {#set_in}
```sv linenums="1"
set<int> intSet = {1, 2};

bit bitVal_0, bitVal_1, bitVal_2;
if (1   in intSet) bitVal_0 = 1;    //  bitVal_0: 0 -> 1
if (3   in intSet) bitVal_1 = 1;    //  bitVal_1: 0 -> 0
if ("1" in intSet) bitVal_2 = 1;    //  bitVal_2: 0 -> 0
```

## `foreach` statement {#set_foreach}
```sv linenums="1"
set<int> intSet = {1, 2};

int sum = 0;
foreach (i:intSet) {
    sum += i;   //  sum: 0 -> 3
}
```

???+ Warning
    For `set`-type, *index variable* of `foreach` statament should **NOT** be used to specify `set` elements.
    ```sv linenums="1"
    foreach (intSet[i]) {}  //  ILLEGAL
    ```

---

## function int `size()` {#set_size}
```sv linenums="1"
set<int> intSet = {1, 2};

int intVal = intSet.size(); //  intVal: 0 -> 2
```

## function void `clear()` {#set_clear}
```sv linenums="1"
set<int> intSet = {1, 2};

intSet.clear(); // intSet: {1, 2} -> {}
```

## function void `delete(data_type element)` {#set_delete}
```sv linenums="1"
set<int> intSet = {1, 2};

intSet.delete( 2 ); //  intSet: {1, 2} -> {1}
intSet.delete( 3 ); //  ILLEGAL (1)
intSet.delete("1"); //  ILLEGAL (2)
```

1. The *element* is not exist in the set.
2. Data type of the *element* is not same as the set.

## function void `insert(data_type element)` {#set_insert}
```sv linenums="1"
set<int> intSet = {1, 2};

intSet.insert( 3 ); //  intSet: {1, 2}    -> {1, 2, 3}
intSet.insert( 2 ); //  intSet: {1, 2, 3} -> {1, 2, 3}
intSet.insert("4"); //  ILLEGAL (1)
```

1. Data type of the *element* is not same as the set.

## function list&lt;data_type&gt; `to_list()` {#set_to_list}
```sv linenums="1"
set<int> intSet = {1, 2};

list<int> intList = intSet.to_list();   //  intList: {} -> {1, 2}
```
