---
title: Array Operators
description: 8.8.2.1 Array operators
---

# Array Operators
## Index operator `[]`: {#array_operators_index}
=== "Template"
    ```sv linenums="1"
    array<int, 3> intArray;
    int intVal = intArray[2];  ///<  get element 2 of intArray;
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [3];
    int intVal = intArray[2];  ///<  get element 2 of intArray;
    ```

???+ note

    Operator that do not modify contents may be used in **activity**, **constraint**, and **covergroup**.

## Assignment operator `=`: {#array_operators_assignment}
=== "Template"
    ```sv linenums="1"
    array<int, 3> intArray = { 1, 2, 3 };   ///<  assign values while declaration
    intArray[2] = intArray[1];              ///<  assign value of element 2 by element 1
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [3] = { 1, 2, 3 };         ///<  assign values while declaration
    intArray[2] = intArray[1];              ///<  assign value of element 2 by element 1
    ```

???+ note

    Operator that do not modify contents may be used in **exec block** and **native functions**.
## Equality operator `==`: {#array_operators_equality}
=== "Template"
    ```sv linenums="1"
    array<int   , 2> intArray_0    = {  1 ,  2      };
    array<int   , 3> intArray_1    = {  1 ,  2 ,  3 };
    array<string, 2> stringArray_0 = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2, bitVal_3;
    if (intArray_0    == intArray_0   ) bitVal_0 = 1;  ///<  bitVal_0: 0 -> 1 (1)
    if (intArray_0[1] == intArray_1[1]) bitVal_1 = 1;  ///<  bitVal_1: 0 -> 1 (2)
    if (intArray_0    == intArray_1   ) bitVal_2 = 1;  ///<  bitVal_2: 0 -> 0 (3)
    if (intArray_0    == stringArray_0) bitVal_3 = 1;  ///<  bitVal_3: 0 -> 0 (4)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Equalize **type**, **context**.
    3. Inequalize **size**, **context**.
    4. Inequalize **type**.

=== "Square"
    ```sv linenums="1"
    int    intArray_0    [2] = {  1 ,  2      };
    int    intArray_1    [3] = {  1 ,  2 ,  3 };
    string stringArray_0 [2] = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2, bitVal_3;
    if (intArray_0    == intArray_0   ) bitVal_0 = 1;  ///<  bitVal_0: 0 -> 1 (1)
    if (intArray_0[1] == intArray_1[1]) bitVal_1 = 1;  ///<  bitVal_1: 0 -> 1 (2)
    if (intArray_0    == intArray_1   ) bitVal_2 = 1;  ///<  bitVal_2: 0 -> 0 (3)
    if (intArray_0    == stringArray_0) bitVal_3 = 1;  ///<  bitVal_3: 0 -> 0 (4)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Equalize **type**, **context**.
    3. Inequalize **size**, **context**.
    4. Inequalize **type**.

???+ note

    Operator that do not modify contents may be used in **activity**, **constraint**, and **covergroup**.

## Inequality operator `!=`: {#array_operators_inequality}
=== "Template"
    ```sv linenums="1"
    array<int   , 2> intArray_0    = {  1 ,  2      };
    array<int   , 3> intArray_1    = {  1 ,  2 ,  3 };
    array<string, 2> stringArray_0 = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2, bitVal_3;
    if (intArray_0    != intArray_0   ) bitVal_0 = 1;  ///<  bitVal_0: 0 -> 0 (1)
    if (intArray_0[1] != intArray_1[1]) bitVal_1 = 1;  ///<  bitVal_1: 0 -> 0 (2)
    if (intArray_0    != intArray_1   ) bitVal_2 = 1;  ///<  bitVal_2: 0 -> 1 (3)
    if (intArray_0    != stringArray_0) bitVal_3 = 1;  ///<  bitVal_3: 0 -> 1 (4)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Equalize **type**, **context**.
    3. Inequalize **size**, **context**.
    4. Inequalize **type**.

=== "Square"
    ```sv linenums="1"
    int    intArray_0    [2] = {  1 ,  2      };
    int    intArray_1    [3] = {  1 ,  2 ,  3 };
    string stringArray_0 [2] = { "1", "2"     };

    bit bitVal_0, bitVal_1, bitVal_2, bitVal_3;
    if (intArray_0    != intArray_0   ) bitVal_0 = 1;  ///<  bitVal_0: 0 -> 0 (1)
    if (intArray_0[1] != intArray_1[1]) bitVal_1 = 1;  ///<  bitVal_1: 0 -> 0 (2)
    if (intArray_0    != intArray_1   ) bitVal_2 = 1;  ///<  bitVal_2: 0 -> 1 (3)
    if (intArray_0    != stringArray_0) bitVal_3 = 1;  ///<  bitVal_3: 0 -> 1 (4)
    ```

    1. Equalize **size**, **type**, **context**.
    2. Equalize **type**, **context**.
    3. Inequalize **size**, **context**.
    4. Inequalize **type**.

???+ note

    Operator that do not modify contents may be used in **activity**, **constraint**, and **covergroup**.

## Set membership operator `in`: {#array_operators_in}
=== "Template"
    ```sv linenums="1"
    array<int, 2> intArray_0 = { 1, 2    };
    array<int, 3> intArray_1 = { 1, 2, 3 };

    bit bitVal_0, bitVal_1;
    if (            1 in intArray_0) bitVal_0 = 1;  ///<  bitval_0: 0 -> 1
    if (intArray_0[1] in intArray_1) bitVal_1 = 1;  ///<  bitVal_1: 0 -> 1
    ```

=== "Square"
    ```sv linenums="1"
    int intArray_0 [2] = { 1, 2    };
    int intArray_1 [3] = { 1, 2, 3 };

    bit bitVal_0, bitVal_1;
    if (            1 in intArray_0) bitVal_0 = 1;  ///<  bitval_0: 0 -> 1
    if (intArray_0[1] in intArray_1) bitVal_1 = 1;  ///<  bitVal_1: 0 -> 1
    ```

???+ note

    Operator that do not modify contents may be used in **activity**, **constraint**, and **covergroup**.

## `foreach` statement: {#array_operators_foreach}
=== "Template"
    ```sv linenums="1"
    array<int, 2> intArray = { 1, 2 };

    int intVal = 0;
    foreach (intArray[j]) {
        intVal = intArray[j];  ///<  intVal: 0 -> 1 -> 2
    }
    ```

=== "Square"
    ```sv linenums="1"
    int intArray [2] = { 1, 2 };

    int intVal = 0;
    foreach (intArray[j]) {
        intVal = intArray[j];  ///<  intVal: 0 -> 1 -> 2
    }
    ```

???+ note

    Operator that do not modify contents may be used in **activity**, **constraint**, **native exec code** and **covergroup**.