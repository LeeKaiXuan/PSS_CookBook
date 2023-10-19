---
title: Array
description: PSSv2.1/7.9.2 Arrays
---

# Array {#array}

## Declarations
Array has 2 declaration formats: `Template`, `Square`.
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

    1. `square` format **not** support for declare nested array

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
| Operator                                                  | Description                                                                                                                               |
| :-------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| [`[]`](Arrays.md#index "Index operator `[]`")             | Used to access a specific element of an array.                                                                                            |
| [`=`](Arrays.md#assignment "Assignment operator `=`")     | Creates a copy of the `array`-type expression on the RHS and assigns it to the array on the LHS.                                          |
| [`==`](Arrays.md#equality "Equality operator `==`")       | Evaluates to *true* if all elements with corresponding indexes are equal.                                                                 |
| [`!=`](Arrays.md#inequality "Inequality operator `!=`")   | Evaluates to *true* if not all elements with corresponding indexes are equal.                                                             |
| [`in`](Arrays.md#in "Set membership operator `in`")       | It evaluates to *true* if the element specified on the left of the operator exists in the array collection on the right of the operator.  |
| [`foreach`](Arrays.md#foreach "`foreach` statement")      | The foreach statement can be applied to an array to iterate over the array elements.                                                      |

## Array Methods
| Method                                                                                                | Description                                                       |
| :---------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| [int `size()`](Arrays.md#size "function int `size()`")                                                | Returns the number of elements in the arrays.                     |
| [int `sum()`](Arrays.md#sum "function int `sum()`")                                                   | Returns the sum of all elements currently stored in the array.    |
| [list&lt;data_type&gt; `to_list()`](Arrays.md#to_list "function list&lt;data_type&gt; `to_list()`")   | Returns all elements in a [`list`](Lists.md#list)-type.           |
| [set&lt;data_type&gt; `to_set()`:](Arrays.md#to_set "function set&lt;data_type&gt; `to_set()`")       | Returns all elements in a [`set`](Sets.md#set)-type.              |

---

## Index operator `[]` {#index}
=== "Template"
    ```sv linenums="1"
    array<int, 3> intArray = {1, 2, 3};
    int intVal = intArray[2];   //  intVal: 0 -> 3
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [3] = {1, 2, 3};
    int intVal = intArray[2];   //  intVal: 0 -> 3
    ```

???+ note

    Operator that do not modify contents can be used within **activity**, **constraint**, or **covergroup**.

## Assignment operator `=` {#assignment}
=== "Template"
    ```sv linenums="1"
    array<int, 3> intArray = {1, 2, 3};
    intArray[2] = 4;            //  intArray: {1, 2, 3} -> {1, 2, 4}
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [3] = {1, 2, 3};
    intArray[2] = 4;            //  intArray: {1, 2, 3} -> {1, 2, 4}
    ```

???+ note

    Operator that do not modify contents can be used within **exec block** or **native functions**.

## Equality operator `==` {#equality}
=== "Template"
    ```sv linenums="1"
    array<int   , 2> intArray_0  = {  1 ,  2      };
    array<int   , 3> intArray_1  = {  1 ,  2 ,  3 };
    array<string, 2> stringArray = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2;
    if (intArray_0 == intArray_0 ) bitVal_0 = 1;    //  bitVal_0: 0 -> 1 (1)
    if (intArray_0 == intArray_1 ) bitVal_1 = 1;    //  bitVal_1: 0 -> 0 (2)
    if (intArray_0 == stringArray) bitVal_2 = 1;    //  bitVal_2: 0 -> 0 (3)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Inequalize **size**, **context**.
    3. Inequalize **type**.

=== "Square"
    ```sv linenums="1"
    int    intArray_0  [2] = {  1 ,  2      };
    int    intArray_1  [3] = {  1 ,  2 ,  3 };
    string stringArray [2] = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2;
    if (intArray_0 == intArray_0 ) bitVal_0 = 1;    //  bitVal_0: 0 -> 1 (1)
    if (intArray_0 == intArray_1 ) bitVal_1 = 1;    //  bitVal_1: 0 -> 0 (2)
    if (intArray_0 == stringArray) bitVal_2 = 1;    //  bitVal_2: 0 -> 0 (3)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Inequalize **size**, **context**.
    3. Inequalize **type**.

???+ note

    Operator that do not modify contents can be used within **activity**, **constraint**, or **covergroup**.

## Inequality operator `!=` {#inequality}
=== "Template"
    ```sv linenums="1"
    array<int   , 2> intArray_0  = {  1 ,  2      };
    array<int   , 3> intArray_1  = {  1 ,  2 ,  3 };
    array<string, 2> stringArray = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2;
    if (intArray_0 != intArray_0 ) bitVal_0 = 1;    //  bitVal_0: 0 -> 0 (1)
    if (intArray_0 != intArray_1 ) bitVal_1 = 1;    //  bitVal_1: 0 -> 1 (3)
    if (intArray_0 != stringArray) bitVal_2 = 1;    //  bitVal_2: 0 -> 1 (4)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Inequalize **size**, **context**.
    3. Inequalize **type**.

=== "Square"
    ```sv linenums="1"
    int    intArray_0  [2] = {  1 ,  2      };
    int    intArray_1  [3] = {  1 ,  2 ,  3 };
    string stringArray [2] = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2;
    if (intArray_0 != intArray_0 ) bitVal_0 = 1;    //  bitVal_0: 0 -> 0 (1)
    if (intArray_0 != intArray_1 ) bitVal_1 = 1;    //  bitVal_1: 0 -> 1 (2)
    if (intArray_0 != stringArray) bitVal_2 = 1;    //  bitVal_2: 0 -> 1 (3)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Inequalize **size**, **context**.
    3. Inequalize **type**.

???+ note

    Operator that do not modify contents can be used within **activity**, **constraint**, or **covergroup**.

## Set membership operator `in` {#in}
=== "Template"
    ```sv linenums="1"
    array<int, 3> intArray = {1, 2, 3};

    bit bitVal_0, bitVal_1;
    if (1 in intArray) bitVal_0 = 1;                //  bitval_0: 0 -> 1
    if (0 in intArray) bitVal_1 = 1;                //  bitVal_1: 0 -> 0
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [3] = {1, 2, 3};

    bit bitVal_0, bitVal_1;
    if (1 in intArray) bitVal_0 = 1;                //  bitval_0: 0 -> 1
    if (0 in intArray) bitVal_1 = 1;                //  bitVal_1: 0 -> 0
    ```

???+ note

    Operator that do not modify contents can be used within **activity**, **constraint**, or **covergroup**.

## `foreach` statement {#foreach}
=== "Template"
    ```sv linenums="1"
    array<int, 3> intArray = {1, 2, 3};

    foreach (intArray[i]) {
        intArray[i] = intArray[i] + 1;  //  intArray: {1, 2, 3} -> {2, 3, 4}
    }
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [3] = {1, 2, 3};

    foreach (intArray[i]) {
        intArray[i] = intArray[i] + 1;  //  intArray: {1, 2, 3} -> {2, 3, 4}
    }
    ```

???+ note

    Operator that do not modify contents can be used within **activity**, **constraint**, **native exec code** or **covergroup**.

---

## function int `size()` {#size}
=== "Template"
    ```sv linenums="1"
    array<int, 2> intArray;
    int intVal = intArray.size();  //  intVal: 0 -> 2
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [2];
    int intVal = intArray.size();  //  intVal: 0 -> 2
    ```

???+ note

    Considered as a **constant** expression.

## function int `sum()` {#sum}
=== "Template"
    ```sv linenums="1"
    array<int    , 2> intArray    = {  1   ,  2    };
    array<bit [2], 2> bitArray    = { 2'b01, 2'b10 };
    array<string , 2> stringArray = { "1"  , "2"   };
    int intVal_0 = intArray.sum()   ;  //  intVal_0: 0 -> 3
    int intVal_1 = bitArray.sum()   ;  //  intVal_1: 0 -> 3
    int intVal_2 = stringArray.sum();  //  ILLEGAL (1)
    ```

    1. `string` can't be calculated

=== "Square"
    ```sv linenums="1"
    int     intArray    [2] = {  1   ,  2    };
    bit [2] bitArray    [2] = { 2'b01, 2'b10 };
    string  stringArray [2] = { "1"  , "2"   };
    int intVal_0 = intArray.sum()   ;  //  intVal_0: 0 -> 3
    int intVal_1 = bitArray.sum()   ;  //  intVal_1: 0 -> 3
    int intVal_2 = stringArray.sum();  //  ILLEGAL (1)
    ```

    1. `string` can't be calculated

???+ note

    Only can used on numeric data type (`int` or `bit`).

???+ tip "Usage: use `sum()` to constrain a random array"

    === "Template"
        ```sv linenums="1"
        rand array<int, 2> intArray;
        constraint {
            intArray.sum() == 3;
            intArray[0] == 2;   //  intArray: {0, 0} -> {2, 1}
        }
        ```

    === "Square"
        ```sv linenums="1"
        rand int intArray [2];
        constraint {
            intArray.sum() == 3;
            intArray[0] == 2;   //  intArray: {0, 0} -> {2, 1}
        }
        ```

## function list&lt;data_type&gt; `to_list()` {#to_list}
=== "Template"
    ```sv linenums="1"
    array<int   , 3> intArray    = {  2 ,  1 ,  2  };
    array<string, 3> stringArray = { "2", "1", "2" };
    list<int   > intList    = intArray.to_list()   ;    //  intList: {} -> {2, 1, 2}
    list<string> stringList = stringArray.to_list();    //  stringList: {} -> {"2", "1", "2"};
    ```

=== "Square"
    ```sv linenums="1"
    int    intArray    [3] = {  2 ,  1 ,  2  };
    string stringArray [3] = { "2", "1", "2" };
    list<int   > intList    = intArray.to_list()   ;    //  intList: {} -> {2, 1, 2}
    list<string> stringList = stringArray.to_list();    //  stringList: {} -> {"2", "1", "2"};
    ```

## function set&lt;data_type&gt; `to_set()` {#to_set}
=== "Template"
    ```sv linenums="1"
    array<int   , 3> intArray    = {  2 ,  1 ,  2  };
    array<string, 3> stringArray = { "2", "1", "2" };
    set<int   > intSet    = intArray.to_set()   ;       //  intSet: {} -> {2, 1}
    set<string> stringSet = stringArray.to_set();       //  stringSet: {} -> {"2", "1"}
    ```

=== "Square"
    ```sv linenums="1"
    int    intArray    [3] = {  2 ,  1 ,  2  };
    string stringArray [3] = { "2", "1", "2" };
    set<int   > intSet    = intArray.to_set()   ;       //  intSet: {} -> {2, 1}
    set<string> stringSet = stringArray.to_set();       //  stringSet: {} -> {"2", "1"}
    ```
