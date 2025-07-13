## Numeric Functions in MySQL

**Numeric functions** in MySQL handle operations involving numbers, such as arithmetic, rounding, absolute values, powers, trigonometry, logarithms, and random number generation.

---

### 🔹 Inner Index

* [Basic Arithmetic Functions](#basic-arithmetic-functions)
* [Rounding Functions](#rounding-functions)
* [Absolute and Sign Functions](#absolute-and-sign-functions)
* [Power and Root Functions](#power-and-root-functions)
* [Logarithmic Functions](#logarithmic-functions)
* [Trigonometric Functions](#trigonometric-functions)
* [Random and Other Utility Functions](#random-and-other-utility-functions)
* [Usage Scenarios](#usage-scenarios)

---

### Basic Arithmetic Functions

| Function           | Description                                     |
| ------------------ | ----------------------------------------------- |
| `+`, `-`, `*`, `/` | Addition, Subtraction, Multiplication, Division |
| `MOD(n, m)`        | Remainder (n mod m)                             |
| `DIV`              | Integer division                                |

```sql
SELECT 10 DIV 3; -- 3
SELECT MOD(10, 3); -- 1
```

---

### Rounding Functions

| Function                     | Description                 |
| ---------------------------- | --------------------------- |
| `ROUND(num, decimals)`       | Rounds to given decimals    |
| `TRUNCATE(num, decimals)`    | Truncates to given decimals |
| `CEIL(num)` / `CEILING(num)` | Smallest integer ≥ num      |
| `FLOOR(num)`                 | Largest integer ≤ num       |

```sql
SELECT ROUND(12.3456, 2); -- 12.35
SELECT TRUNCATE(12.3456, 2); -- 12.34
```

---

### Absolute and Sign Functions

| Function    | Description                       |
| ----------- | --------------------------------- |
| `ABS(num)`  | Absolute value                    |
| `SIGN(num)` | Returns -1, 0, or 1 based on sign |

```sql
SELECT ABS(-23); -- 23
SELECT SIGN(-23); -- -1
```

---

### Power and Root Functions

| Function      | Description         |
| ------------- | ------------------- |
| `POWER(x, y)` | x raised to power y |
| `SQRT(x)`     | Square root of x    |

```sql
SELECT POWER(2, 4); -- 16
SELECT SQRT(25); -- 5
```

---

### Logarithmic Functions

| Function   | Description          |
| ---------- | -------------------- |
| `LOG(x)`   | Natural log (base e) |
| `LOG10(x)` | Log base 10          |
| `LOG2(x)`  | Log base 2           |
| `EXP(x)`   | e raised to x        |

```sql
SELECT LOG(10); -- 2.302585
SELECT LOG10(100); -- 2
SELECT EXP(1); -- 2.7182818
```

---

### Trigonometric Functions

| Function     | Description              |
| ------------ | ------------------------ |
| `SIN(x)`     | Sine of x (x in radians) |
| `COS(x)`     | Cosine of x              |
| `TAN(x)`     | Tangent of x             |
| `ASIN(x)`    | Inverse sine             |
| `ACOS(x)`    | Inverse cosine           |
| `ATAN(x)`    | Inverse tangent          |
| `RADIANS(x)` | Degrees to radians       |
| `DEGREES(x)` | Radians to degrees       |

```sql
SELECT SIN(RADIANS(90)); -- 1
SELECT DEGREES(PI()); -- 180
```

---

### Random and Other Utility Functions

| Function       | Description                             |
| -------------- | --------------------------------------- |
| `RAND()`       | Random float \[0, 1)                    |
| `RAND(N)`      | Seeded random                           |
| `PI()`         | Returns the constant π (3.14159…)       |
| `FORMAT(x, d)` | Formats number with commas and decimals |

```sql
SELECT RAND(); -- 0.285714 (example)
SELECT FORMAT(12345.6789, 2); -- '12,345.68'
```

---

### Usage Scenarios

* **Generate a random discount:**

  ```sql
  SELECT ROUND(RAND() * 50); -- Random 0–50
  ```

* **Round prices:**

  ```sql
  SELECT ROUND(price, 0) FROM products;
  ```

* **Normalize a column to absolute values:**

  ```sql
  SELECT ABS(score_diff) FROM matches;
  ```

* **Use conditional math with sign:**

  ```sql
  SELECT amount * SIGN(profit) FROM deals;
  ```

---

### Conclusion

Numeric functions are essential in calculations, transformations, and statistical queries. They enable dynamic computations directly within SQL statements, eliminating the need for external processing.

---
