---
title: Traversal
description: PSSv2.1/12.3.2 Action handle array traversal
---

# Traversal

## Traversal Context
| Context                                   | Semantics                                                                     |
| :---------------------------------------- | :---------------------------------------------------------------------------- |
| [`parallel`](index.md#traversal_parallel) | All array elements are scheduled for traversal in parallel.                   |
| [`schedule`](index.md#traversal_schedule) | All array elements are scheduled for traversal independently.                 |
| [`select`](index.md#traversal_select)     | One array element is randomly selected and traversed.                         |
| [`sequence`](index.md#traversal_sequence) | All array elements are scheduled for traversal in sequence from `0` to `N-1`. |

## `parallel` {#traversal_parallel}
*Work in Progress*

## `schedule` {#traversal_schedule}
Both actions (i.e., sub with "Hello" and "World") in `schedule` block will be traversed in random order.
```sv linenums="1"
action top {
    activity {
        schedule {
            do sub with { str == "Hello"; };
            do sub with { str == "World"; };
        }
    }
}

action sub {
    rand string str;
    exec body ASM = """{{str}}""";
}
```

There have two possible results:
=== ""Hello" first"
    ```sv linenums="1"
    Hello
    World
    ```

=== ""World" first"
    ```sv linenums="1"
    World
    Hello
    ```

## `select` {#traversal_select}
Only one action in `select` block will be chosen and traversed.
```sv linenums="1"
action top {
    activity {
        select {
            do sub with { str == "Hello"; };
            do sub with { str == "World"; };
        }
    }
}

action sub {
    rand string str;
    exec body ASM = """{{str}}""";
}
```

There have two possible results:
=== ""Hello" chosen"
    ```sv linenums="1"
    Hello
    ```

=== ""World" chosen"
    ```sv linenums="1"
    World
    ```

## `sequence` {#traversal_sequence}
*Work in Progress*
