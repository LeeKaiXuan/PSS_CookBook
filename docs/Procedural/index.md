---
title: Procedural
description: PSSv2.1/21.7 Procedural constructs
---

# Procedural

## `void` Function Calls {#void}
Declare a function that no return value.

*WIP*

## `return` Statement {#return}
Returns a value to the caller from a function or `exec` block.
Syntax:
> return *expression* ;

- *expression* : An **optional** value need for returned to the caller.

## `repeat` Statement {#repeat}
Executes *procedural_stmt* repeatedly by specified the number of *iteration*.
Syntax:
> repeat (*index_identifier* : *expression*) *procedural_stmt*

- *index_identifier* : An **optional** index-variable identifier can be specified that ranges from `0` to `*iteration* - 1`.
- *expression* : Specify *iteration* by a non-negative integer (e.g., `int` or `bit`).
- *procedural_stmt* : Iterated by the number of *iteration*. Not executed if *iteration* is `0`.

```sv linenums="1"
int intVal = 0;

repeat (i : 3) {
    intVal = i;     //  intVal: 0 -> 1 -> 2 -> 3
}
```

## `repeat`-`while` Statement {#repeat_while}
Executes *procedural_stmt* repeatedly as long as the *expression* is **true**.
Syntax:
> repeat *procedural_stmt* while (*expression*);

- *procedural_stmt* : Iterated so long as the *expression* is **true**.
- *expression* : Evaluates **true** or **false** everytime after *procedural_stmt*.

```sv linenums="1"
int intVal = 0;

repeat {
    intVal += 1;    //  intVal: 0 -> 1 -> 2 -> 3
} while (intVal < 1);
```

## `while` Statement {#while}
Executes *procedural_stmt* repeatedly as long as the *expression* is **true**.
Syntax:
> while (*expression*) *procedural_stmt*

- *procedural_stmt* : Iterated so long as the *expression* is **true**.
- *expression* : Evaluates **true** or **false** everytime before *procedural_stmt*.

```sv linenums="1"
int intVal = 0;

while (intVal < 3) {
    intVal += 1;    //  intVal: 0 -> 1 -> 2 -> 3
}
```

## `foreach` Statement {#foreach}
Executes *procedural_stmt* for each *element* of the *expression*.
Syntax:
> foreach (*iterator_identifier* : *expression* [*index_identifier*]) *procedural_stmt*

- *iterator_identifier* : An **optional** iterator-variable identifier with collection *element* type, an is an lias to current *element*.
- *index_identifier* : An **optional** index-variable identifier can be specified that ranges from `0` to `size() - 1` when *expression* is `array`-type or `list`-type; or can be specified of all *key*s when *expression* is `map`-type.
- *expression* : A collection type (e.g., `array`, `list`, `map`, or `set`).
- *procedural_stmt* : Iterated by the number of `size()` of the *expression*.

!!! Warning
    - For `set`-type, *index_identifier* should **NOT** be specified.
    - At least one of *iterator_identifier* or *index_identifier* should be specified.
    - Both *iterator_identifier* and *index_identifier* should **NOT** be changed inside *procedural_stmt*.

???+ Note
    - A colon (`:`) must be append after *iterator_identifier* if its specified.
    - A pair of square brackets (`[]`) must be used to contain *index_identifier* if its specified.
    - The order of *key*s are undetermined when *expression* is `map`-type.

```sv linenums="1"
array<bit [4], 3> nibbleArray = {4'd4, 4'd5, 4'd6};
bit [4] nibbleVal = 0;
int intVal = 0;

foreach (i : intArray[j]) {
    nibbleVal = i;  //  nibbleVal: 0 -> 4'd4 -> 4'd5 -> 4'd6
    intVal    = j;  //  intVal   : 0 ->   0  ->   1  ->   2
}
```

## `if`-`else` Statement {#if_else}
Executes *procedural_stmt_for_true* when *expression* is **true**.
Syntax:
> if (*expression*) *procedural_stmt_for_true* else *procedural_stmt_for_false*

- *expression* : Evaluates **true** or **false**.
- *procedural_stmt_for_true* : Executed when the *expression* is **true**.
- *procedural_stmt_for_false* : An **optional** procedural will be executed when the *expression* is **false**.

```sv linenums="1"
int intVal = 3;
bit bitVal = 0;

if (intVal > 0) {
    bitVal = 1;     //  bitVal: 0 -> 1
}
else {
    bitVal = 0;
}
```

## `match` Statement {#match}
Executes *procedural_stmt* when corresponding *range* is match to the *expression*.
Syntax:
> match (*expression*) {<br>
>   [*range*] : *procedural_stmt*<br>
>   [*range*] : *procedural_stmt*<br>
>   ...<br>
>   default : *procedural_stmt*<br>
> }

- *expression* : The item to be evaluated.
- *range* : An open range list is compared to *expression*.
- *procedural_stmt* : Executed when *expression* matches any one in corresponding *range*.
- default : An **optional** procedural will be executed when not any *range* was matched.

!!! Warning
    - Only one of *range*s should be matched.
    - The `default` must be exist and executed if no any *range* was matched.

```sv linenums="1"
int intVal = 3;
bit [4] nibbleVal = 0;

match (intVal) {
    [..-1]       : nibbleVal = 4'b0001;
    [0..9]       : nibbleVal = 4'b0010;
    [10, 12, 14] : nibbleVal = 4'b0100; //  nibbleVal: 0 -> 4'b0100
    [100..]      : nibbleVal = 4'b1000;
    default      : nibbleVal = 4'b1111;
}
```

## `break` Statement {#break}
Continues execution after enclosing innermost loop construct.
Syntax:
> break;

!!! Warning
    The `break` statement may only appear within loop statements (`repeat`, `repeat`-`while`, `while`, or `foreach`).

```sv linenums="1"
int intVal = 1;

while (intVal > 0) {
    intVal += 1;    //  intVal: 0 -> 1 -> 2 -> 3
    if (intVal > 2) break;
}
```

## `continue` Statement {#continue}
Continues next loop iteration.
Syntax:
> continue;

!!! Warning
    The `continue` statement may only appear within loop statements (`repeat`, `repeat`-`while`, `while`, or `foreach`).

```sv linenums="1"
int intVal = 0;

repeat (i : 3) {
    if (i < 2) continue;
    intVal = i;     //  intVal: 0 -> 2
}
```

## `rand` Statement {#rand}
*WIP*

## `exec` Block {#exec}
*WIP*
