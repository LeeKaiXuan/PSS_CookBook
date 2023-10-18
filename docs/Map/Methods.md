---
title: Map Methods
description: PSSv2.1/7.9.4.2 Map methods
---

# Map Methods

## function int `size()` {#map_methods_size}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
int intVal = string2int.size(); //  intVal: 0 -> 2
```

## function void `clear()` {#map_methods_clear}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
string2int.clear(); //  string2int: {"1":1, "2":2} -> {}
```

## function &lt;data_type&gt; `delete(data_type key)` {#map_methods_delete}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
map.delete("1");    //  string2int: {"1":1, "2":2} -> {"2":2}
map.delete("3");    //  ILLEGAL (1)
```

1. Key "3" not exist.

## function void `insert(data_type key, data_type element)` {#map_methods_insert}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2};
string2int.insert("1", 0  );    //  string2int: {"1":1, "2":2} -> {"1":0, "2":2}
string2int.insert("3", 3  );    //  string2int: {"1":0, "2":2} -> {"1":0, "2":2, "3":3}
string2int.insert("4", 4.0);    //  ILLEGAL (1)
string2int.insert(5  , 5  );    //  ILLEGAL (2)
```

1. Data type of *element* is not same.
2. Data type of *key* is not same.

## function set&lt;data_type&gt; `keys()` {#map_methods_keys}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2, "2.5":2};

set<string> stringSet = string2int.keys();  //  stringSet: {} -> {"1", "2", "2.5"}
```

## function list&lt;data_type&gt; `values()` {#map_methods_values}
```sv linenums="1"
map<string, int> string2int = {"1":1, "2":2, "2.5":2};

list<int> intList = string2int.values();    //  intList: {} -> {1, 2, 2}
```
