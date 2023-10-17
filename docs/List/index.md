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
| Operator                                                                  | Description                                                                                                                                   |
| :------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| [`[]`](Operators.md#list_operators_index "Index operator `[]`")           | Used to access a specific element of a list.                                                                                                  |
| [`=`](Operators.md#list_operators_assignment "Assignment operator `=`")   | Creates a copy of the list-type expression on the RHS and assigns it to the list on the LHS.                                                  |
| [`==`](Operators.md#list_operators_equality "Equality operator `==`")     | Evaluates to *true* if all elements with corresponding indexes are equal.                                                                     |
| [`!=`](Operators.md#list_operators_inequality "Inequality operator `!=`") | Evaluates to *true* if not all elements with corresponding indexes are equal.                                                                 |
| [`in`](Operators.md#list_operators_in "Set membership operator `in`")     | It evaluates to *true* if the element specified on the left of the operator exists in the **list** collection on the right of the operator.   |
| [`foreach`](Operators.md#list_operators_foreach "`foreach` statement")    | The foreach statement can be applied to a list to iterate over the list elements.                                                             |

## List Methods
| Method                                                                                                                                                        | Description                                                       |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------- |
| [int `size()`](Methods.md#list_methods_size "function int `size()`")                                                                                          | Returns the number of elements in the list.                       |
| [`clear()`](Methods.md#list_methods_clear "function void `clear()`")                                                                                          | Removes all elements.                                             |
| [&lt;data_type&gt; `delete(index)`](Methods.md#list_methods_delete "function &lt;data_type&gt; `delete(index)`")                                              | Move out element at the specified index.                          |
| [`insert(index, element)`](Methods.md#list_methods_insert "function `insert(index, element)`")                                                                | Add element at the specified index.                               |
| [&lt;data_type&gt; `pop_front()`](Methods.md#list_methods_pop_front "function &lt;data_type&gt; `pop_front()`")                                               | Move out first element. Same as `delete(0)`.                      |
| [`push_front(element)`](Methods.md#list_methods_push_front "function void `push_front(element)`")                                                             | Add element at beginning of list. Same as `insert(0, element)`.   |
| [&lt;data_type&gt; `pop_back()`](Methods.md#list_methods_pop_back "function &lt;data_type&gt; `pop_back()`")                                                  | Move out last element. Same as `delete(size()-1)`.                |
| [`push_back(element)`](Methods.md#list_methods_push_back "function void `push_back(element)`")                                                                | Add element at end of list. Same as `insert(size(), element)`.    |
| [set&lt;data_type&gt; `to_set()`](Methods.md#list_methods_to_set "function set&lt;data_type&gt; `to_set()`")                                                  | Convert list to unordered set.                                    |
| [`shuffle()`](Methods.md#list_methods_shuffle "function void `shuffle()`")<br>[:material-engine-outline: v2.1](../index.md#reference "LRM minimum version")   | Randomize orders of elements.                                     |
