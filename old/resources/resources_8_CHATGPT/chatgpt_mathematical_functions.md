# Mathematical Functions

Mathematical functions are used to perform calculations and transformations on numerical data in SQL. These functions are commonly employed in queries to manipulate numbers, calculate results, and perform statistical or mathematical operations.

## Mathematical Functions

### 1. `ABS()`
- **Description**: Returns the absolute (positive) value of a number.
- **Syntax**: `ABS(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT ABS(-10) AS result;
  ```

### 2. `CEIL()` / `CEILING()`
- **Description**: Returns the smallest integer greater than or equal to a number.
- **Syntax**: `CEIL(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT CEIL(4.2) AS result;
  ```

### 3. `FLOOR()`
- **Description**: Returns the largest integer less than or equal to a number.
- **Syntax**: `FLOOR(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT FLOOR(4.7) AS result;
  ```

### 4. `ROUND()`
- **Description**: Rounds a number to a specified number of decimal places.
- **Syntax**: `ROUND(expression, decimal_places)`
- **Parameters**:
  - `expression`: The numeric value or column.
  - `decimal_places`: The number of decimal places to round to.
- **Example**:
  ```sql
  SELECT ROUND(4.567, 2) AS result;
  ```

### 5. `TRUNC()` / `TRUNCATE()`
- **Description**: Truncates a number to a specified number of decimal places.
- **Syntax**: `TRUNC(expression, decimal_places)`
- **Parameters**:
  - `expression`: The numeric value or column.
  - `decimal_places`: The number of decimal places to keep.
- **Example**:
  ```sql
  SELECT TRUNC(4.567, 2) AS result;
  ```

### 6. `MOD()`
- **Description**: Returns the remainder of a division operation.
- **Syntax**: `MOD(dividend, divisor)`
- **Parameters**:
  - `dividend`: The number to be divided.
  - `divisor`: The number to divide by.
- **Example**:
  ```sql
  SELECT MOD(10, 3) AS result;
  ```

### 7. `POWER()`
- **Description**: Raises a number to the power of another number.
- **Syntax**: `POWER(base, exponent)`
- **Parameters**:
  - `base`: The base number.
  - `exponent`: The power to raise the base to.
- **Example**:
  ```sql
  SELECT POWER(2, 3) AS result;
  ```

### 8. `SQRT()`
- **Description**: Returns the square root of a number.
- **Syntax**: `SQRT(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT SQRT(16) AS result;
  ```

### 9. `EXP()`
- **Description**: Returns e raised to the power of a number (e ≈ 2.718).
- **Syntax**: `EXP(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT EXP(1) AS result;
  ```

### 10. `LOG()`
- **Description**: Returns the natural logarithm (base e) of a number.
- **Syntax**: `LOG(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT LOG(2.718) AS result;
  ```

### 11. `LOG10()`
- **Description**: Returns the base-10 logarithm of a number.
- **Syntax**: `LOG10(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT LOG10(100) AS result;
  ```

### 12. `PI()`
- **Description**: Returns the constant π (approximately 3.14159).
- **Syntax**: `PI()`
- **Parameters**: None.
- **Example**:
  ```sql
  SELECT PI() AS result;
  ```

### 13. `SIGN()`
- **Description**: Returns the sign of a number: -1 for negative, 1 for positive, and 0 for zero.
- **Syntax**: `SIGN(expression)`
- **Parameters**:
  - `expression`: The numeric value or column.
- **Example**:
  ```sql
  SELECT SIGN(-10) AS result;
  ```

### 14. `RADIANS()`
- **Description**: Converts degrees to radians.
- **Syntax**: `RADIANS(expression)`
- **Parameters**:
  - `expression`: The angle in degrees.
- **Example**:
  ```sql
  SELECT RADIANS(180) AS result;
  ```

### 15. `DEGREES()`
- **Description**: Converts radians to degrees.
- **Syntax**: `DEGREES(expression)`
- **Parameters**:
  - `expression`: The angle in radians.
- **Example**:
  ```sql
  SELECT DEGREES(PI()) AS result;
  ```

### 16. `RANDOM()` / `RAND()`
- **Description**: Returns a random number between 0 and 1.
- **Syntax**: `RANDOM()`
- **Parameters**: None.
- **Example**:
  ```sql
  SELECT RANDOM() AS result;
  ```


## Comparison of Mathematical Functions Across SQL Implementations

| Feature/Function       | ANSI SQL | PostgreSQL | MySQL (8.0+) | SQL Server | Oracle |
|------------------------|----------|------------|--------------|------------|--------|
| **ABS()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **CEIL() / CEILING()** | Supported | Supported  | Supported    | Supported  | Supported |
| **FLOOR()**            | Supported | Supported  | Supported    | Supported  | Supported |
| **ROUND()**            | Supported | Supported  | Supported    | Supported  | Supported |
| **TRUNC()**            | Not Supported | Supported  | Supported    | Not Supported | Supported |
| **MOD()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **POWER()**            | Supported | Supported  | Supported    | Supported  | Supported |
| **SQRT()**             | Supported | Supported  | Supported    | Supported  | Supported |
| **EXP()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **LOG()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **LOG10()**            | Supported | Supported  | Supported    | Supported  | Supported |
| **PI()**               | Not Supported | Supported  | Supported    | Supported  | Supported |
| **SIGN()**             | Not Supported | Supported  | Supported    | Supported  | Supported |
| **RADIANS()**          | Supported | Supported  | Supported    | Supported  | Supported |
| **DEGREES()**          | Supported | Supported  | Supported    | Supported  | Supported |
| **RANDOM() / RAND()**  | Supported | `RANDOM()` | `RAND()`     | `RAND()`   | `DBMS_RANDOM.VALUE` |

### Notes on Differences

1. **TRUNC()**:
   - **ANSI SQL**: Not supported.
   - Supported in databases like PostgreSQL and Oracle.
   
2. **RANDOM() / RAND()**:
   - Terminology varies: PostgreSQL uses `RANDOM()`, while MySQL and SQL Server use `RAND()`.

3. **PI()**:
   - Some databases calculate π directly; not part of ANSI SQL.

4. **SIGN()**:
   - Not universally supported in all database systems.

