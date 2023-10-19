---
title: Map
description: PSSv2.1/7.9.4 Maps
---

# Map {#map}

## Properties
- Unordered.
- Non-randomizable.
- Elements can be added or removed within `exec` blocks.
- *Key* and *element* can be any [*scalar*](../DataTypes/index.md#datatypes_scalar "e.g., `bit`, `int`, `bool`, `enum`, `string`, `float32`, `float64`, `chandle`") or [*aggregate*](../DataTypes/index.md#datatypes_aggregate "e.g., `array`, `list`, `map`, `set`, `struct`") of scalars.
- *Key*s must be unique.

## Declarations
=== "Without Initialization Assignment"
    ```sv linenums="1"
    map<bit [4] , int    > nibble2int  ;    //  nibble2int  : {}
    map<int     , bool   > int2bool    ;    //  int2bool    : {}
    map<bool    , string > bool2string ;    //  bool2string : {}
    map<string  , float32> string2float;    //  string2float: {}
    map<float32 , int    > float2int   ;    //  float2int   : {}
    map<eSTR2NUM, int    > enum2int    ;    //  enum2int    : {} (1)
    ```

    1. Assume defined enum type before
    ```sv linenums="1"
    enum eSTR2NUM {
        ZERO, ONE, TWO
    };
    ```

=== "With Initialization Assignment"
    ```sv linenums="1"
    map<bit [4] , int    > nibble2int   = {4'b1110:3      , 4'b0110:2     };
    map<int     , bool   > int2bool     = {      4:true   ,       5:false };
    map<bool    , string > bool2string  = {  false:"FALSE",    true:"TRUE"};
    map<string  , float32> string2float = {  "2.1":2.1    ,   "2.2":2.2   };
    map<float32 , int    > float2int    = {    2.4:2      ,     2.6:3     };
    map<eSTR2NUM, int    > enum2int     = {    ONE:1      ,     TWO:2     }; // (1)!
    ```

    1. Assume defined enum type before
    ```sv linenums="1"
    enum eSTR2NUM {
        ZERO, ONE, TWO
    };
    ```

## Map Operators
| Operator                                              | Description                                                                                   |
| :---------------------------------------------------- | :-------------------------------------------------------------------------------------------- |
| [`[]`](Maps.md#index "Index operator `[]`")           | Used to access a specific element of a map.                                                   |
| [`=`](Maps.md#assignment "Assignment operator `=`")   | Creates a copy of the `map`-type expression on the RHS and assigns it to the map on the LHS.  |
| [`==`](Maps.md#equality "Equality operator `==`")     | Evaluates to *true* if all elements with corresponding keys are equal.                        |
| [`!=`](Maps.md#inequality "Inequality operator `!=`") | Evaluates to *true* if not all elements with corresponding keys are equal.                    |
| [`foreach`](Maps.md#foreach "`foreach` statement")    | The foreach statement can be applied to a map to iterate over the map elements.               |


## Map Methods
| Method                                                                                            | Description                                               |
| :------------------------------------------------------------------------------------------------ | :-------------------------------------------------------- |
| [int `size()`](Maps.md#size "function int `size()`")                                              | Returns the number of elements in the map.                |
| [`clear()`](Maps.md#clear "function void `clear()`")                                              | Removes all elements.                                     |
| [&lt;data_type&gt; `delete(key)`](Maps.md#delete "function &lt;data_type&gt; `delete(key)`")      | Moves out element with the specified key.                 |
| [`insert(key, element)`](Maps.md#insert "function void `insert(key, element)`")                   | Adds or replace element with the specified key.           |
| [set&lt;data_type&gt; `keys()`](Maps.md#keys "function set&lt;data_type&gt; `keys()`")            | Returns all keys in a [`set`](Sets.md#set)-type.          |
| [list&lt;data_type&gt; `values()`](Maps.md#values "function list&lt;data_type&gt; `values()`")    | Returns all elements in a [`list`](Lists.md#list)-type.   |

---

## Index operator `[]` {#index}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
int intVal = string2int["2"];   //  intVal: 0 -> 2;
int intVal = string2int["3"];   //  ILLEGAL (1)
```

1. Key `"3"` not exist.

## Assignment operator `=` {#assignment}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
string2int["1"] = 0;    //  string2int: {"1":1, "2":2} -> {"1":0, "2":2}
string2int["3"] = 3;    //  string2int: {"1":0, "2":2} -> {"1":0, "2":2, "3":3}
```

## Equality operator `==` {#equality}
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

## Inequality operator `==` {#inequality}
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

## `foreach` statement {#foreach}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};

foreach (string2int[i]) {
    string2int[i] = string2int[i] + 1;  //  string2int: {"1":1, "2":2} -> {"1":2, "2":3}
}
```

???+ note

    Operator can be used within **activity**, **constraint**, or **native exec code**.

---

## function int `size()` {#size}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
int intVal = string2int.size(); //  intVal: 0 -> 2
```

## function void `clear()` {#clear}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
string2int.clear(); //  string2int: {"1":1, "2":2} -> {}
```

## function &lt;data_type&gt; `delete(data_type key)` {#delete}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
map.delete("1");    //  string2int: {"1":1, "2":2} -> {"2":2}
map.delete("3");    //  ILLEGAL (1)
```

1. Key `"3"` not exist.

## function void `insert(data_type key, data_type element)` {#insert}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
string2int.insert("1", 0  );    //  string2int: {"1":1, "2":2} -> {"1":0, "2":2}
string2int.insert("3", 3  );    //  string2int: {"1":0, "2":2} -> {"1":0, "2":2, "3":3}
string2int.insert("4", 4.0);    //  ILLEGAL (1)
string2int.insert(5  , 5  );    //  ILLEGAL (2)
```

1. Data type of *element* is not same.
2. Data type of *key* is not same.

## function set&lt;data_type&gt; `keys()` {#keys}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2, "2.5":2};

set<string> stringSet = string2int.keys();  //  stringSet: {} -> {"1", "2", "2.5"}
```

## function list&lt;data_type&gt; `values()` {#values}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2, "2.5":2};

list<int> intList = string2int.values();    //  intList: {} -> {1, 2, 2}
```
