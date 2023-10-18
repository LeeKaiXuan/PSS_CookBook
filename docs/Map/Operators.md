---
title: Map Operators
description: PSSv2.1/7.9.4.1 Map operators
---

# Map Operators

## Index operator `[]` {#map_operators_index}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
int intVal = string2int["2"];   //  intVal: 0 -> 2;
int intVal = string2int["3"];   //  ILLEGAL (1)
```

1. Key "3" not exist.

## Assignment operator `=` {#map_operators_assignment}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
string2int["1"] = 0;    //  string2int: {"1":1, "2":2} -> {"1":0, "2":2}
string2int["3"] = 3;    //  string2int: {"1":0, "2":2} -> {"1":0, "2":2, "3":3}
```

## Equality operator `==` {#map_operators_equality}
```sv linenums="1"
map<string, int   > map_0 = {"1":1  , "2":2  };
map<string, int   > map_1 = {"1":0  , "2":2  };
map<string, int   > map_2 = {"0":1  , "2":2  };
map<string, int   > map_3 = {"2":2  , "1":1  };
map<string, int   > map_4 = {"1":1           };
map<int   , string> map_5 = {  1:"1",   2:"2"};

bit bitVal_0, bitVal_1, bitVal_2, bitVal_3, bitVal_4, bitVal_5;
if (map_0 == map_0) bitVal_0 = 1;   //  bitVal_0: 0 -> 1 (1)
if (map_0 == map_1) bitVal_1 = 1;   //  bitVal_1: 0 -> 0 (2)
if (map_0 == map_2) bitVal_2 = 1;   //  bitVal_2: 0 -> 0 (3)
if (map_0 == map_3) bitVal_3 = 1;   //  bitVal_3: 0 -> 1 (4)
if (map_0 == map_4) bitVal_4 = 1;   //  bitVal_4: 0 -> 0 (5)
if (map_0 == map_5) bitVal_5 = 1;   //  bitVal_5: 0 -> 0 (6)
```

1. Equalize **size**, **keys**, **elements**.
2. Inequalize **element**.
3. Inequalize **key**.
4. Equalize **size**, **keys**, **elements**.
5. Inequalize **size**.
6. Inequalize **keys**, **elements**.

## Inequality operator `==` {#map_operators_inequality}
```sv linenums="1"
map<string, int   > map_0 = {"1":1  , "2":2  };
map<string, int   > map_1 = {"1":0  , "2":2  };
map<string, int   > map_2 = {"0":1  , "2":2  };
map<string, int   > map_3 = {"2":2  , "1":1  };
map<string, int   > map_4 = {"1":1           };
map<int   , string> map_5 = {  1:"1",   2:"2"};

bit bitVal_0, bitVal_1, bitVal_2, bitVal_3, bitVal_4, bitVal_5;
if (map_0 != map_0) bitVal_0 = 1;   //  bitVal_0: 0 -> 0 (1)
if (map_0 != map_1) bitVal_1 = 1;   //  bitVal_1: 0 -> 1 (2)
if (map_0 != map_2) bitVal_2 = 1;   //  bitVal_2: 0 -> 1 (3)
if (map_0 != map_3) bitVal_3 = 1;   //  bitVal_3: 0 -> 0 (4)
if (map_0 != map_4) bitVal_4 = 1;   //  bitVal_4: 0 -> 1 (5)
if (map_0 != map_5) bitVal_5 = 1;   //  bitVal_5: 0 -> 1 (6)
```

1. Equalize **size**, **keys**, **elements**.
2. Inequalize **element**.
3. Inequalize **key**.
4. Equalize **size**, **keys**, **elements**.
5. Inequalize **size**.
6. Inequalize **keys**, **elements**.

## `foreach` statement {#map_operators_foreach}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};

foreach (string2int[i]) {
    string2int[i] = string2int[i] + 1;  //  string2int: {"1":1, "2":2} -> {"1":2, "2":3}
}
```

???+ note

    Operator can be used within **activity**, **constraint**, or **native exec code**.

