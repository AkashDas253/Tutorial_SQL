## **PostgreSQL Numeric Data Types, Functions, and Operations**  

---

### **1. Numeric Data Types**  
| Data Type | Storage | Range | Notes |
|-----------|--------|-------|-------|
| `SMALLINT` | 2 bytes | -32,768 to 32,767 | Integer type |
| `INTEGER` (`INT`) | 4 bytes | -2,147,483,648 to 2,147,483,647 | Common integer type |
| `BIGINT` | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | Large integer type |
| `DECIMAL(p, s)` | Variable | Up to `131072` digits before and `16383` after the decimal | Exact precision |
| `NUMERIC(p, s)` | Variable | Same as `DECIMAL` | Exact precision |
| `REAL` | 4 bytes | ~6 decimal digits | Approximate precision |
| `DOUBLE PRECISION` | 8 bytes | ~15 decimal digits | Higher precision |
| `SERIAL` | 4 bytes | 1 to 2,147,483,647 | Auto-incrementing integer |
| `BIGSERIAL` | 8 bytes | 1 to 9,223,372,036,854,775,807 | Large auto-incrementing integer |

---

### **2. Numeric Operators**  
| Operator | Description | Example |
|----------|-------------|---------|
| `+` | Addition | `SELECT 10 + 5;` → `15` |
| `-` | Subtraction | `SELECT 10 - 5;` → `5` |
| `*` | Multiplication | `SELECT 10 * 5;` → `50` |
| `/` | Division | `SELECT 10 / 5;` → `2` |
| `%` | Modulus (Remainder) | `SELECT 10 % 3;` → `1` |
| `^` | Power | `SELECT 2 ^ 3;` → `8` |
| `|/` | Square Root | `SELECT |/ 25;` → `5` |
| `||/` | Cube Root | `SELECT ||/ 27;` → `3` |
| `!` | Factorial | `SELECT 5!;` → `120` |
| `@` | Absolute Value | `SELECT @ -10;` → `10` |

---

### **3. Numeric Functions**  
| Function | Description | Example |
|----------|-------------|---------|
| `ABS(x)` | Absolute value | `SELECT ABS(-10);` → `10` |
| `CEIL(x)` | Smallest integer ≥ `x` | `SELECT CEIL(2.3);` → `3` |
| `FLOOR(x)` | Largest integer ≤ `x` | `SELECT FLOOR(2.9);` → `2` |
| `ROUND(x, d)` | Round `x` to `d` decimals | `SELECT ROUND(2.678, 2);` → `2.68` |
| `TRUNC(x, d)` | Truncate `x` to `d` decimals | `SELECT TRUNC(2.678, 2);` → `2.67` |
| `MOD(x, y)` | Modulus (`x % y`) | `SELECT MOD(10, 3);` → `1` |
| `POWER(x, y)` | `x` raised to power `y` | `SELECT POWER(2, 3);` → `8` |
| `SQRT(x)` | Square root | `SELECT SQRT(25);` → `5` |
| `CBRT(x)` | Cube root | `SELECT CBRT(27);` → `3` |
| `PI()` | Returns `π` | `SELECT PI();` → `3.14159265358979` |
| `EXP(x)` | `e^x` | `SELECT EXP(1);` → `2.71828182845905` |
| `LN(x)` | Natural log (`logₑ(x)`) | `SELECT LN(10);` → `2.30258509299405` |
| `LOG(base, x)` | Logarithm of `x` base `base` | `SELECT LOG(10, 1000);` → `3` |
| `RANDOM()` | Random float between `0` and `1` | `SELECT RANDOM();` → `0.7563` |
| `SETSEED(x)` | Set random seed (`-1` to `1`) | `SELECT SETSEED(0.5);` |

---

### **4. Type Casting & Conversion**  
| Action | Command Example |
|--------|----------------|
| Cast to Integer | `SELECT CAST(5.9 AS INTEGER);` → `5` |
| Cast to Numeric | `SELECT '123.45'::NUMERIC;` → `123.45` |
| Cast to Double Precision | `SELECT CAST(10 AS DOUBLE PRECISION);` |
