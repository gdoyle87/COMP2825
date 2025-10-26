# Boolean Algebra, Logic Simplification, K-Maps, and Logic Gates

These notes summarize the key concepts needed to understand Boolean expressions, simplification methods, truth tables, Karnaugh maps, and the design and interpretation of logic circuits.

---

## Boolean Algebra Basics

Boolean algebra deals with **binary values** and **logic operations**.

| Concept    | Description                              |
| ---------- | ---------------------------------------- |
| Variables  | A, B, C, ...                             |
| Values     | 0 (false), 1 (true)                      |
| Functions  | F(A,B,C), G(A,B), ...                    |
| Operations | NOT (A'), AND (A·B), OR (A+B), XOR (A⊕B) |

??? example "Examples of Boolean expressions"
    A·B  
    A + B  
    A'(B + C)  
    A ⊕ B

---

## Truth Tables

A truth table lists **all possible input combinations** and the resulting output.

??? example "Example Truth Table for AND"
    | A | B | A·B |
    |---|---|-----|
    | 0 | 0 | 0 |
    | 0 | 1 | 0 |
    | 1 | 0 | 0 |
    | 1 | 1 | 1 |

---

## Boolean Identities (Simplification Rules)

| Rule       | Identity                         |
| ---------- | -------------------------------- |
| Complement | A + A' = 1, A·A' = 0             |
| Identity   | A + 0 = A, A·1 = A               |
| Null       | A + 1 = 1, A·0 = 0               |
| Idempotent | A + A = A, A·A = A               |
| De Morgan  | (A+B)' = A'·B', (A·B)' = A' + B' |

Use these identities to reduce expressions and minimize gate usage.

---

## Simplification Example

Simplify:
F = A'B + AB' + AB

??? example "Step-by-Step Simplification"
    F = A'B + AB' + AB  
     = B(A' + A) + AB'  
     = B(1) + AB'  
     = B + AB'  
     = (B + A)(B + B')  
     = A + B
    
**Final Answer:**  
F = A + B

---

## Canonical Forms

### Sum of Products (SOP)

- Use rows in truth table where **F = 1**
- Form **minterms** (AND of input variables)
- OR them together

### Product of Sums (POS)

- Use rows in truth table where **F = 0**
- Form **maxterms** (OR of input variables)
- AND them together

---

## Karnaugh Maps (K-Maps)

K-maps are visual tools for simplifying Boolean expressions.

### Rules

- Group **1s** in sizes **1, 2, 4, 8, ...**
- Groups must be **rectangular**
- Groups may **wrap around edges**
- Each **1** must be included in at least one group
- Larger groups produce simpler expressions

---

### K-Map Example (3 variables: A, B, C)

Truth table function values:
F = 1 for m1, m3, m5, m7  
(binary inputs 001, 011, 101, 111)

K-Map:

| AB \ C | 0   | 1   |
| ------ | --- | --- |
| 00     | 0   | 1   |
| 01     | 0   | 1   |
| 11     | 0   | 1   |
| 10     | 0   | 1   |

Group the column where C = 1 → all 1’s in one group.

This means **C** remains; A and B vary → they drop out.

**Simplified Expression:**  
F = C

??? example "Why this simplifies to C"
    C is the only input that is 1 in all grouped minterms.
    A and B change, so they do not appear in the final expression.

---

## Logic Gates

| Gate | Symbol   | Function                       |
| ---- | -------- | ------------------------------ |
| NOT  | A'       | Inverts input                  |
| AND  | A·B      | Output 1 if both inputs = 1    |
| OR   | A + B    | Output 1 if any input = 1      |
| XOR  | A ⊕ B    | Output 1 only if inputs differ |
| NAND | (A·B)'   | Inverted AND                   |
| NOR  | (A + B)' | Inverted OR                    |

---
