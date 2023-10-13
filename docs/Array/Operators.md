---
title: Array Operators
description: PSSv2.1/7.9.2.1 Array operators
---

# Array Operators

## Index operator `[]` {#array_operators_index}
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

## Assignment operator `=` {#array_operators_assignment}
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

## Equality operator `==` {#array_operators_equality}
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

## Inequality operator `!=` {#array_operators_inequality}
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

## Set membership operator `in` {#array_operators_in}
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

## `foreach` statement {#array_operators_foreach}
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
