---
title: Expression Operators
description: 9.4 Expression operators
---

# Expression Operators
## Expression operators and data types

| Operator token            | Operator name                         | Operator data types                   | Result data type              |
| :------------------------ | :------------------------------------ | :-----------------------------------: | :---------------------------: |
| `?:`                      | Conditional operator                  | Any plain-data type or reference type | Same as operands              |
| `-`                       | Unary arithmetic negation operator    | Numeric                               | Same as operand               |
| `~`                       | Unary bitwise negation operator       | Numeric                               | Same as operand               |
| `!`                       | Unary Boolean negation operator       | Boolean                               | Boolean                       |
| `& | ^`                   | Unary bitwise reduction operators     | Numeric                               | 1-bit                         |
| `+ - * / % **`            | Binary arithmetic operators           | Numeric                               | 1-bit                         |
| `& | ^`                   | Binary bitwise operators              | Numeric                               | 1-bit                         |
| `>> <<`                   | Binary shift operators                | Numeric                               | Same as left operand          |
| `&& ||`                   | Binary Boolean logical operators      | Boolean                               | Same as operands              |
| `< <= > >=`               | Binary relational operators           | Numeric                               | Boolean                       |
| `== !=`                   | Binary logical equality operators     | Any plain-data type or reference type | Boolean                       |
| `cast`                    | Data type conversion operator         | Numeric, Boolean, enum                | Casting type                  |
| `in`                      | Binary set membership operator        | Any plain-data type                   | Boolean                       |
| `[expression]`            | Index operator                        | Array, list, map                      | Same as element of collection |
| `[expression]`            | Bit-select operators                  | Numeric                               | Numeric                       |
| `[expression:expression]` | Part-select operator                  | Numeric                               | Numeric                       |

## Operator precedence and associativity

| Operator                          | Associativity | Precesence    |
| :-------------------------------- | :-----------: | :-----------: |
| `()` `[]`                         | Left          | 1 (Highest)   |
| `cast`                            | Right         | 2             |
| `-` `!` `~` `&` `|` `^` (unary)   |               | 2             |
| `**`                              | Left          | 3             |
| `*` `/` `%`                       | Left          | 4             |
| `+` `-` (binary)                  | Left          | 5             |
| `<<` `>>`                         | Left          | 6             |
| `<` `<=` `>` `>=` `in`            | Left          | 7             |
| `==` `!=`                         | Left          | 8             |
| `&` (binary)                      | Left          | 9             |
| `^` (binary)                      | Left          | 10            |
| `|` (binary)                      | Left          | 11            |
| `&&`                              | Left          | 12            |
| `||`                              | Left          | 13            |
| `?:` (conditional operator)       | Right         | 14 (Lowest)   |

