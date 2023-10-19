---
title: Set Operators
description: PSSv2.1/7.9.5.1 Set operators
---

# Set Operators

## Assignment operator `=` {#set_operators_assignment}
```sv linenums="1"
set<int> intSet;

intSet = {1, 2};    //  intSet: {}     -> {1, 2}
intSet = {3, 3, 4}; //  intSet: {1, 2} -> {3, 4} (1)
```

1. Same element will appear only once.

## Equality operator `==` {#set_operators_equality}
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

## Inequality operator `!=` {#set_operators_inequality}
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

## Set membership operator `in` {#set_operators_in}
```sv linenums="1"
set<int> intSet = {1, 2};

bit bitVal_0, bitVal_1, bitVal_2;
if (1   in intSet) bitVal_0 = 1;    //  bitVal_0: 0 -> 1
if (3   in intSet) bitVal_1 = 1;    //  bitVal_1: 0 -> 0
if ("1" in intSet) bitVal_2 = 1;    //  bitVal_2: 0 -> 0
```

## `foreach` statement {#set_operators_foreach}
```sv linenums="1"
set<int> intSet = {1, 2};

int sum = 0;
foreach (i:intSet) {
    sum += i;   //  sum: 0 -> 3
}
```

???+ Warning
    For `set`-type, *index variable* of `foreach` statament should **NOT** be used to specify `set` elements.
