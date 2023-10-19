---
title: List
description: PSSv2.1/7.9.3 Lists
---

# List {#list}

## Declarations
```sv linenums="1"
list<int     > intList   ;  //  declare an integer list
list<bit [8] > byteList  ;  //  declare a byte list
list<bool    > boolList  ;  //  declare a bool list
list<string  > stringList;  //  declare a string list
list<eSTR2NUM> enumList  ;  //  declare an enum list (1)
list<sSTR2NUM> structList;  //  declare a struct list (2)
```

1. Assume defined enum type before
```sv linenums="1"
enum eSTR2NUM {
    ZERO, ONE, TWO
};
```

2. Assume defined struct type before
```sv linenums="1"
struct sSTR2NUM {
    string stringVal;
    int intVal;
};
```

## Declare list by `rand` keyword:
[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")
```sv linenums="1"
rand list<int    > intList   ;
rand list<bit [8]> byteList  ;
rand list<string > stringList;
```

## List Operators
| Operator                                                  | Description                                                                                                                               |
| :-------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| [`[]`](Lists.md#index "Index operator `[]`")              | Used to access a specific element of a list.                                                                                              |
| [`=`](Lists.md#assignment "Assignment operator `=`")      | Creates a copy of the `list`-type expression on the RHS and assigns it to the list on the LHS.                                            |
| [`==`](Lists.md#equality "Equality operator `==`")        | Evaluates to *true* if all elements with corresponding indexes are equal.                                                                 |
| [`!=`](Lists.md#inequality "Inequality operator `!=`")    | Evaluates to *true* if not all elements with corresponding indexes are equal.                                                             |
| [`in`](Lists.md#in "Set membership operator `in`")        | It evaluates to *true* if the element specified on the left of the operator exists in the list collection on the right of the operator.   |
| [`foreach`](Lists.md#foreach "`foreach` statement")       | The foreach statement can be applied to a list to iterate over the list elements.                                                         |

## List Methods
| Method                                                                                                                                        | Description                                                       |
| :-------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| [int `size()`](Lists.md#size "function int `size()`")                                                                                         | Returns the number of elements in the list.                       |
| [`clear()`](Lists.md#clear "function void `clear()`")                                                                                         | Removes all elements.                                             |
| [&lt;data_type&gt; `delete(int index)`](Lists.md#delete "function &lt;data_type&gt; `delete(intindex)`")                                      | Moves out element at the specified index.                         |
| [`insert(int index, data_type element)`](Lists.md#insert "function void `insert(int index, data_type element)`")                              | Adds element at the specified index.                              |
| [&lt;data_type&gt; `pop_front()`](Lists.md#pop_front "function &lt;data_type&gt; `pop_front()`")                                              | Moves out first element. Same as `delete(0)`.                     |
| [`push_front(data_type element)`](Lists.md#push_front "function void `push_front(data_type element)`")                                        | Adds element at beginning of list. Same as `insert(0, element)`.  |
| [&lt;data_type&gt; `pop_back()`](Lists.md#pop_back "function &lt;data_type&gt; `pop_back()`")                                                 | Moves out last element. Same as `delete(size()-1)`.               |
| [`push_back(data_typeelement)`](Lists.md#push_back "function void `push_back(data_type element)`")                                            | Adds element at end of list. Same as `insert(size(), element)`.   |
| [set&lt;data_type&gt; `to_set()`](Lists.md#to_set "function set&lt;data_type&gt; `to_set()`")                                                 | Returns all elements to a [`set`](Sets.md#set)-type.              |
| [`shuffle()`](Lists.md#shuffle "function void `shuffle()`")<br>[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")  | Randomizes orders of elements.                                    |

---

## Index operator `[]` {#index}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList[1];    //  intVal: 0 -> 2
```

## Assignment operator `=` {#assignment}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList[0] = 4;             //  intVal: {1, 2, 3} -> {4, 2, 3}
```

## Equality operator `==` {#equality}
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

## Inequality operator `!=` {#inequality}
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

## Set membership operator `in` {#in}
```sv linenums="1"
list<int> intList = {1, 2, 3};

bit bitVal_0, bitVal_1;
if ( 1 in intList) bitVal_0 = 1;            //  bitVal_0: 0 -> 1;
if ( 0 in intList) bitVal_1 = 1;            //  bitVal_1: 0 -> 0;
```

???+ note

    Operator that do not modify contents can be used within **activity**, **constraint**, or **covergroup**.

## `foreach` statement {#foreach}
```sv linenums="1"
list<int> intList = {1, 2, 3};

foreach (intList[i]) {
    intList[i] = intList[i] + 1;            //  intList: {1, 2, 3} -> {2, 3, 4}
}
```

???+ note

    Operator can be used within **activity**, **constraint**, or **native exec code**.

---

## function int `size()` {#size}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.size();        //  intVal: 0 -> 3
```

## function void `clear()` {#clear}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.clear();                    //  intList: {1, 2, 3} -> {}
```

## function &lt;data_type&gt; `delete(index)` {#delete}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.delete(1);     //  intVal: 0 -> 2; intList: {1, 2, 3} -> {1, 3}
```

## function void `insert(index, element)` {#insert}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.insert(1, 6);               //  intList: {1, 2, 3} -> {1, 6, 2, 3}
```

## function &lt;data_type&gt; `pop_front()` {#pop_front}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.pop_front();   //  intVal: 0 -> 1; intList: {1, 2, 3} -> {2, 3}
```

## function void `push_front(element)` {#push_front}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.push_front(4);              //  intList: {1, 2, 3} -> {4, 1, 2, 3}
```

## function &lt;data_type&gt; `pop_back()` {#pop_back}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.pop_back();    //  intVal: 0 -> 3; intList: {1, 2, 3} -> {1, 2}
```

## function void `push_back(element)` {#push_back}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.push_back(4);               //  intList: {1, 2, 3} -> {1, 2, 3, 4}
```

## function set&lt;data_type&gt; `to_set()` {#to_set}
```sv linenums="1"
list<int> intList = {1, 2, 1};
set<int> intSet = intList.to_set(); //  intSet: {} -> {1, 2}
```

## function void `shuffle()` {#shuffle}
[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")
```sv linenums="1"
list<int> intList = {1, 2};
intList.shuffle();                  //  intList: {1, 2} -> {1, 2} or {2, 1}
```
