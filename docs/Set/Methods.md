---
title: Set Methods
description: PSSv2.1/7.9.5.2 Set methods
---

# Set Methods

## function int `size()` {#set_methods_size}
```sv linenums="1"
set<int> intSet = {1, 2};

int intVal = intSet.size(); //  intVal: 0 -> 2
```

## function void `clear()` {#set_methods_clear}
```sv linenums="1"
set<int> intSet = {1, 2};

intSet.clear(); // intSet: {1, 2} -> {}
```

## function void `delete(data_type element)` {#set_methods_delete}
```sv linenums="1"
set<int> intSet = {1, 2};

intSet.delete( 2 ); //  intSet: {1, 2} -> {1}
intSet.delete( 3 ); //  ILLEGAL (1)
intSet.delete("1"); //  ILLEGAL (2)
```

1. The *element* is not exist in the set.
2. Data type of the *element* is not same as the set.

## function void `insert(data_type element)` {#set_methods_insert}
```sv linenums="1"
set<int> intSet = {1, 2};

intSet.insert( 3 ); //  intSet: {1, 2}    -> {1, 2, 3}
intSet.insert( 2 ); //  intSet: {1, 2, 3} -> {1, 2, 3}
intSet.insert("4"); //  ILLEGAL (1)
```

1. Data type of the *element* is not same as the set.

## function list&lt;data_type&gt; `to_list()` {#set_methods_to_list}
```sv linenums="1"
set<int> intSet = {1, 2};

list<int> intList = intSet.to_list();   //  intList: {} -> {1, 2}
```
