# Null Value Functions

Null value functions handle `NULL` values in SQL queries. These functions are crucial for data manipulation and ensuring accurate query results when dealing with missing or undefined data.

## Null Value Functions

### 1. `ISNULL()`
- **Description**: Returns a specified value if the expression is `NULL`, otherwise returns the expression.
- **Syntax**: `ISNULL(expression, replacement_value)`
- **Parameters**:
  - `expression`: The value or column to check.
  - `replacement_value`: The value to return if the expression is `NULL`.
- **Example**:
  ```sql
  SELECT ISNULL(NULL, 'No Value') AS result;
  ```

### 2. `IFNULL()`
- **Description**: Returns a specified value if the expression is `NULL`, otherwise returns the expression. Similar to `ISNULL()` but more common in MySQL.
- **Syntax**: `IFNULL(expression, replacement_value)`
- **Parameters**:
  - `expression`: The value or column to check.
  - `replacement_value`: The value to return if the expression is `NULL`.
- **Example**:
  ```sql
  SELECT IFNULL(NULL, 'No Value') AS result;
  ```

### 3. `COALESCE()`
- **Description**: Returns the first non-`NULL` value from a list of expressions.
- **Syntax**: `COALESCE(expression1, expression2, ..., expressionN)`
- **Parameters**:
  - `expressionN`: A list of values or columns.
- **Example**:
  ```sql
  SELECT COALESCE(NULL, NULL, 'First Non-Null') AS result;
  ```

### 4. `NVL()`
- **Description**: Returns a specified value if the expression is `NULL`, otherwise returns the expression. Common in Oracle.
- **Syntax**: `NVL(expression, replacement_value)`
- **Parameters**:
  - `expression`: The value or column to check.
  - `replacement_value`: The value to return if the expression is `NULL`.
- **Example**:
  ```sql
  SELECT NVL(NULL, 'Default Value') AS result;
  ```

### 5. `NULLIF()`
- **Description**: Returns `NULL` if two expressions are equal; otherwise, it returns the first expression.
- **Syntax**: `NULLIF(expression1, expression2)`
- **Parameters**:
  - `expression1`: The first value or column.
  - `expression2`: The second value or column to compare.
- **Example**:
  ```sql
  SELECT NULLIF(5, 5) AS result;
  ```



## Comparison of Null Value Functions Across SQL Implementations

| Feature/Function       | ANSI SQL | PostgreSQL | MySQL (8.0+) | SQL Server | Oracle       |
|------------------------|----------|------------|--------------|------------|--------------|
| **ISNULL()**           | Not Supported | Not Supported | Not Supported | Supported  | Not Supported |
| **IFNULL()**           | Not Supported | Not Supported | Supported     | Not Supported | Not Supported |
| **COALESCE()**         | Supported | Supported  | Supported    | Supported  | Supported     |
| **NVL()**              | Not Supported | Not Supported | Not Supported | Not Supported | Supported     |
| **NULLIF()**           | Supported | Supported  | Supported    | Supported  | Supported     |

### Notes on Differences

1. **ISNULL()**:
   - Supported only in SQL Server.
   - Alternative: Use `COALESCE()` in other databases.

2. **IFNULL()**:
   - Specific to MySQL.
   - Use `COALESCE()` for cross-database compatibility.

3. **COALESCE()**:
   - Universally supported in all major SQL databases.
   - Preferred for handling multiple `NULL` checks.

4. **NVL()**:
   - Exclusive to Oracle.
   - Use `COALESCE()` as a replacement in other databases.

5. **NULLIF()**:
   - Supported in all major SQL databases.
   - Useful for conditional handling of `NULL` values.