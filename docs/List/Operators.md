---
title: List Operators
description: PSSv2.1/7.9.3.1 List operators
---

# List Operators

## Index operator `[]` {#list_operators_index}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList[1];    //  intVal: 0 -> 2
```

## Assignment operator `=` {#list_operators_assignment}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList[0] = 4;             //  intVal: {1, 2, 3} -> {4, 2, 3}
```

## Equality operator `==` {#list_operators_equality}
```sv linenums="1"
list<int   > intList_0  = { 1 ,  2 ,  3      };
list<int   > intList_1  = { 1 ,  2 ,  3 ,  4 };
list<string> stringList = {"1", "2", "3"};

bit bitVal_0, bitVal_1, bitVal_2;
if (intList_0 == intList_0 ) bitVal_0 = 1;  //  bitVal_0: 0 -> 1; (1)
if (intList_0 == intList_1 ) bitVal_1 = 1;  //  bitVal_1: 0 -> 0; (2)
if (intList_0 == stringList) bitVal_2 = 1;  //  bitVal_2: 0 -> 0; (3)
```

1. Equalize **size**, **type**, **context**.
2. Inequalize **size**, **context**.
3. Inequalize **type**.

## Inequality operator `!=` {#list_operators_inequality}
```sv linenums="1"
list<int   > intList_0  = { 1 ,  2 ,  3      };
list<int   > intList_1  = { 1 ,  2 ,  3 ,  4 };
list<string> stringList = {"1", "2", "3"};

bit bitVal_0, bitVal_1, bitVal_2;
if (intList_0 != intList_0 ) bitVal_0 = 1;  //  bitVal_0: 0 -> 0; (1)
if (intList_0 != intList_1 ) bitVal_1 = 1;  //  bitVal_1: 0 -> 1; (2)
if (intList_0 != stringList) bitVal_2 = 1;  //  bitVal_2: 0 -> 1; (3)
```

1. Equalize **size**, **type**, **context**.
2. Inequalize **size**, **context**.
3. Inequalize **type**.

## Set membership operator `in` {#list_operators_in}
```sv linenums="1"
list<int> intList = {1, 2, 3};

bit bitVal_0, bitVal_1;
if ( 1 in intList) bitVal_0 = 1;            //  bitVal_0: 0 -> 1;
if ( 0 in intList) bitVal_1 = 1;            //  bitVal_1: 0 -> 0;
```

???+ note

    Operator that do not modify contents can be used within **activity**, **constraint**, or **covergroup**.

## `foreach` statement {#list_operators_foreach}
```sv linenums="1"
list<int> intList = {1, 2, 3};

foreach (intList[i]) {
    intList[i] = intList[i] + 1;            //  intList: {1, 2, 3} -> {2, 3, 4}
}
```

???+ note

    Operator can be used within **activity**, **constraint**, or **native exec code**.

