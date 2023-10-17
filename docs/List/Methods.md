---
title: List Methods
description: PSSv2.1/7.9.3.2 List methods
---

# List Methods

## function int `size()` {#list_methods_size}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.size();        //  intVal: 0 -> 3
```

## function void `clear()` {#list_methods_clear}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.clear();                    //  intList: {1, 2, 3} -> {}
```

## function &lt;data_type&gt; `delete(index)` {#list_methods_delete}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.delete(1);     //  intVal: 0 -> 2; intList: {1, 2, 3} -> {1, 3}
```

## function void `insert(index, element)` {#list_methods_insert}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.insert(1, 6);               //  intList: {1, 2, 3} -> {1, 6, 2, 3}
```

## function &lt;data_type&gt; `pop_front()` {#list_methods_pop_front}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.pop_front();   //  intVal: 0 -> 1; intList: {1, 2, 3} -> {2, 3}
```

## function void `push_front(element)` {#list_methods_push_front}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.push_front(4);              //  intList: {1, 2, 3} -> {4, 1, 2, 3}
```

## function &lt;data_type&gt; `pop_back()` {#list_methods_pop_back}
```sv linenums="1"
list<int> intList = {1, 2, 3};
int intVal = intList.pop_back();    //  intVal: 0 -> 3; intList: {1, 2, 3} -> {1, 2}
```

## function void `push_back(element)` {#list_methods_push_back}
```sv linenums="1"
list<int> intList = {1, 2, 3};
intList.push_back(4);               //  intList: {1, 2, 3} -> {1, 2, 3, 4}
```

## function set&lt;data_type&gt; `to_set()` {#list_methods_to_set}
```sv linenums="1"
list<int> intList = {1, 2, 1};
set<int> intSet = intList.to_set(); //  intSet: {} -> {1, 2}
```

## function void `shuffle()` {#list_methods_shuffle}
[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")
```sv linenums="1"
list<int> intList = {1, 2};
intList.shuffle();                  //  intList: {1, 2} -> {1, 2} or {2, 1}
```

