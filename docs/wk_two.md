# Week 2

## Data Representation & Number Systems

Computers operate using **binary (base 2)**, so we often need to convert between number systems and represent integers and real numbers efficiently.

---

### Number Bases

| System      | Base | Digits Used | Example |
| ----------- | ---- | ----------- | ------- |
| Decimal     | 10   | 0–9         | 245₁₀   |
| Binary      | 2    | 0–1         | 111101₂ |
| Octal       | 8    | 0–7         | 725₈    |
| Hexadecimal | 16   | 0–9, A–F    | A3F₁₆   |

---

### Conversions Between Bases

#### Decimal → Binary (Repeated division by 2)

1. Divide by 2.
2. Record remainder.
3. Continue until quotient = 0.
4. Binary result = remainders read **bottom → top**.

??? example "Example: 224₁₀ → Binary"
    ```
    224 ÷ 2 = 112 r0
    112 ÷ 2 = 56 r0
    56 ÷ 2 = 28 r0
    28 ÷ 2 = 14 r0
    14 ÷ 2 = 7 r0
    7 ÷ 2 = 3 r1
    3 ÷ 2 = 1 r1
    1 ÷ 2 = 0 r1
    11100000₂
    ```

#### Binary → Decimal (Positional weighting)

\[
(an…a_3a_2a_1a_0)\_2 = \sum a_i · 2^i
\]

??? example "Example: 1101₂ → Decimal"
    ```     (1×2³) + (1×2²) + (0×2¹) + (1×2⁰)
    = 8 + 4 + 0 + 1 = 13₁₀
    ```

---

### Binary ↔ Hexadecimal (Group by 4 bits)

??? example "Example: Binary → Hex"
    `     1101 0110 1001₂
    D    6    9
    → D69₁₆
    `

??? example "Example: Hex → Binary"
    `     A  F  2
    1010 1111 0010₂
    `

---

### Representing Integers in Binary

#### Unsigned Integers

With **N bits**, values range from:
\[
0 \text{ to } (2^N - 1)
\]

| Bits   | Range             |
| ------ | ----------------- |
| 8-bit  | 0 → 255           |
| 16-bit | 0 → 65,535        |
| 32-bit | 0 → ~4.29 billion |

---

#### Signed Integers (Two’s Complement)

To negate a number:

1. Invert each bit.
2. Add 1.

??? example "Example: Represent −24₁₀"
    ```
    +24 = 00011000₂
    invert → 11100111₂
    +1 → 11101000₂
    → −24 = 11101000₂
    ```

#### Two’s Complement Integer Range

\[
-(2^{N-1}) \text{ to } (2^{N-1} - 1)
\]

| Bits   | Range           |
| ------ | --------------- |
| 8-bit  | −128 → +127     |
| 16-bit | −32768 → +32767 |

---

#### Subtraction Using Two’s Complement

\[
a - b = a + (-b)
\]

??? example "Example: 3 − 13"
    ```
    3 = 00000011
    13 = 00001101

    -13 = invert + 1 = 11110011

    00000011
    +11110011
    ----------
    11110110 = −10₁₀
    ```

---

#### Floating Point Representation (IEEE 754)

Real numbers are stored in normalized form:

\[
(-1)^S · (1.F) · 2^E
\]

Where:

- **S** = sign bit
- **F** = fraction (mantissa)
- **E** = exponent (stored using a bias)

| Precision       | Total Bits | Sign | Exponent | Fraction | Bias |
| --------------- | ---------- | ---- | -------- | -------- | ---- |
| Single (float)  | 32         | 1    | 8        | 23       | 127  |
| Double (double) | 64         | 1    | 11       | 52       | 1023 |

Exponent stored as:
\[
E_b = E + \text{bias}
\]

---

### Converting Fractions to Binary

??? example "Example: 0.75₁₀ → Binary"
    `     0.75 × 2 = 1.5 → 1
    0.50 × 2 = 1.0 → 1
    → 0.11₂
    `

---

### Full IEEE 754 Encoding Example

Convert **−0.75₁₀** to **single precision**:

1. Convert to binary:  
   0.75 = 0.11₂ = 1.1₂ × 2⁻¹
2. Sign bit = **1** (negative)
3. Exponent = −1 → E_b = 127 − 1 = **126 = 01111110₂**
4. Fraction = **10000000000000000000000**

Final 32-bit value:

```
1 01111110 10000000000000000000000
```

---

## Quick Reference Summary

| Type             | Form              | Notes                                       |
| ---------------- | ----------------- | ------------------------------------------- |
| Two’s Complement | invert bits + 1   | Only one zero & supports direct subtraction |
| Float Normalize  | 1.F × 2^E         | Only one leading 1 (implicit)               |
| IEEE Exponent    | stored = E + bias | bias = 127 (float), 1023 (double)           |
| Binary ↔ Hex    | Group bits into 4 | Fast conversion                             |
