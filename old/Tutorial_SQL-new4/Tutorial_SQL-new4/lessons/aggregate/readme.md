# Aggregate Functions

Aggregate functions perform a calculation on a set of values and return a single value. They are often used with the `GROUP BY` clause of the `SELECT` statement.

## Aggregate Functions

### 1. `COUNT()`
- **Description**: Returns the number of rows that match a specified condition.
- **Syntax**: `COUNT(expression)`
- **Parameters**:
  - `expression`: The column or expression to count. Use `*` to count all rows.
- **Example**:
  ```sql
  SELECT COUNT(*) FROM employees;
  ```

### 2. `SUM()`
- **Description**: Returns the total sum of a numeric column.
- **Syntax**: `SUM(expression)`
- **Parameters**:
  - `expression`: The column or expression to sum.
- **Example**:
  ```sql
  SELECT SUM(salary) FROM employees;
  ```

### 3. `AVG()`
- **Description**: Returns the average value of a numeric column.
- **Syntax**: `AVG(expression)`
- **Parameters**:
  - `expression`: The column or expression to average.
- **Example**:
  ```sql
  SELECT AVG(salary) FROM employees;
  ```

### 4. `MIN()`
- **Description**: Returns the smallest value of the selected column.
- **Syntax**: `MIN(expression)`
- **Parameters**:
  - `expression`: The column or expression to find the minimum value.
- **Example**:
  ```sql
  SELECT MIN(salary) FROM employees;
  ```

### 5. `MAX()`
- **Description**: Returns the largest value of the selected column.
- **Syntax**: `MAX(expression)`
- **Parameters**:
  - `expression`: The column or expression to find the maximum value.
- **Example**:
  ```sql
  SELECT MAX(salary) FROM employees;
  ```

### 6. `GROUP_CONCAT()`
- **Description**: Concatenates values from multiple rows into a single string.
- **Syntax**: `GROUP_CONCAT(expression [ORDER BY expression] [SEPARATOR 'separator'])`
- **Parameters**:
  - `expression`: The column or expression to concatenate.
  - `ORDER BY expression`: Optional. Specifies the order of concatenated values.
  - `SEPARATOR 'separator'`: Optional. Specifies the separator between concatenated values.
- **Example**:
  ```sql
  SELECT GROUP_CONCAT(employee_name SEPARATOR ', ') FROM employees;
  ```

### 7. `VARIANCE()`
- **Description**: Returns the variance of a numeric column.
- **Syntax**: `VARIANCE(expression)`
- **Parameters**:
  - `expression`: The column or expression to calculate the variance.
- **Example**:
  ```sql
  SELECT VARIANCE(salary) FROM employees;
  ```

### 8. `STDDEV()`
- **Description**: Returns the standard deviation of a numeric column.
- **Syntax**: `STDDEV(expression)`
- **Parameters**:
  - `expression`: The column or expression to calculate the standard deviation.
- **Example**:
  ```sql
  SELECT STDDEV(salary) FROM employees;
  ```

### 9. `MEDIAN()`
- **Description**: Returns the median value of a numeric column.
- **Syntax**: `MEDIAN(expression)`
- **Parameters**:
  - `expression`: The column or expression to calculate the median.
- **Example**:
  ```sql
  SELECT MEDIAN(salary) FROM employees;
  ```

### 10. `MODE()`
- **Description**: Returns the most frequent value in a column.
- **Syntax**: `MODE() WITHIN GROUP (ORDER BY expression)`
- **Parameters**:
  - `expression`: The column or expression to find the mode.
- **Example**:
  ```sql
  SELECT MODE() WITHIN GROUP (ORDER BY salary) FROM employees;
  ```

### 11. `PERCENTILE_CONT()`
- **Description**: Returns a percentile of a continuous distribution of values.
- **Syntax**: `PERCENTILE_CONT(percentile) WITHIN GROUP (ORDER BY expression)`
- **Parameters**:
  - `percentile`: A number between 0 and 1 representing the desired percentile.
  - `expression`: The column or expression to calculate the percentile.
- **Example**:
  ```sql
  SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) FROM employees;
  ```

### 12. `PERCENTILE_DISC()`
- **Description**: Returns the first value whose cumulative distribution function equals or exceeds the percentile.
- **Syntax**: `PERCENTILE_DISC(percentile) WITHIN GROUP (ORDER BY expression)`
- **Parameters**:
  - `percentile`: A number between 0 and 1 representing the desired percentile.
  - `expression`: The column or expression to calculate the percentile.
- **Example**:
  ```sql
  SELECT PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY salary) FROM employees;
  ```

### 13. `COUNT(DISTINCT)`
- **Description**: Returns the number of distinct (unique) values in a column.
- **Syntax**: `COUNT(DISTINCT expression)`
- **Parameters**:
  - `expression`: The column or expression to count distinct values.
- **Example**:
  ```sql
  SELECT COUNT(DISTINCT department) FROM employees;
  ```

### 14. `CUME_DIST()`
- **Description**: Returns the cumulative distribution of a value in a group of values.
- **Syntax**: `CUME_DIST() WITHIN GROUP (ORDER BY expression)`
- **Parameters**:
  - `expression`: The column or expression to calculate the cumulative distribution.
- **Example**:
  ```sql
  SELECT CUME_DIST() WITHIN GROUP (ORDER BY salary) FROM employees;
  ```

### 15. `DENSE_RANK()`
- **Description**: Returns the rank of a row in a group of rows, with no gaps in ranking values.
- **Syntax**: `DENSE_RANK() OVER (ORDER BY expression)`
- **Parameters**:
  - `expression`: The column or expression to rank.
- **Example**:
  ```sql
  SELECT DENSE_RANK() OVER (ORDER BY salary) FROM employees;
  ```

### 16. `RANK()`
- **Description**: Returns the rank of a row in a group of rows, with gaps in ranking values.
- **Syntax**: `RANK() OVER (ORDER BY expression)`
- **Parameters**:
  - `expression`: The column or expression to rank.
- **Example**:
  ```sql
  SELECT RANK() OVER (ORDER BY salary) FROM employees;
  ```

### 17. `ROW_NUMBER()`
- **Description**: Returns the sequential number of a row within a partition of a result set.
- **Syntax**: `ROW_NUMBER() OVER (ORDER BY expression)`
- **Parameters**:
  - `expression`: The column or expression to order the rows.
- **Example**:
  ```sql
  SELECT ROW_NUMBER() OVER (ORDER BY salary) FROM employees;
  ```

### 18. `NTILE()`
- **Description**: Distributes the rows in an ordered partition into a specified number of groups.
- **Syntax**: `NTILE(number) OVER (ORDER BY expression)`
- **Parameters**:
  - `number`: The number of groups to divide the rows into.
  - `expression`: The column or expression to order the rows.
- **Example**:
  ```sql
  SELECT NTILE(4) OVER (ORDER BY salary) FROM employees;
  ```

### 19. `BIT_AND()`
- **Description**: Returns the bitwise AND of all non-null input values.
- **Syntax**: `BIT_AND(expression)`
- **Parameters**:
  - `expression`: The column or expression to perform the bitwise AND operation.
- **Example**:
  ```sql
  SELECT BIT_AND(flags) FROM employees;
  ```

### 20. `BIT_OR()`
- **Description**: Returns the bitwise OR of all non-null input values.
- **Syntax**: `BIT_OR(expression)`
- **Parameters**:
  - `expression`: The column or expression to perform the bitwise OR operation.
- **Example**:
  ```sql
  SELECT BIT_OR(flags) FROM employees;
  ```

### 21. `BIT_XOR()`
- **Description**: Returns the bitwise XOR of all non-null input values.
- **Syntax**: `BIT_XOR(expression)`
- **Parameters**:
  - `expression`: The column or expression to perform the bitwise XOR operation.
- **Example**:
  ```sql
  SELECT BIT_XOR(flags) FROM employees;
  ```

### 22. `JSON_AGG()`
- **Description**: Aggregates values as a JSON array.
- **Syntax**: `JSON_AGG(expression)`
- **Parameters**:
  - `expression`: The column or expression to aggregate as JSON.
- **Example**:
  ```sql
  SELECT JSON_AGG(employee_name) FROM employees;
  ```

### 23. `STRING_AGG()`
- **Description**: Concatenates values from multiple rows into a single string, with a specified separator.
- **Syntax**: `STRING_AGG(expression, separator)`
- **Parameters**:
  - `expression`: The column or expression to concatenate.
  - `separator`: The separator to use between concatenated values.
- **Example**:
  ```sql
  SELECT STRING_AGG(employee_name, ', ') FROM employees;
  ```


### Notes
- Aggregate functions ignore `NULL` values except for `COUNT(*)`.
- They are often used in conjunction with the `GROUP BY` clause to group rows that have the same values in specified columns into summary rows.
- Some databases may have additional aggregate functions or variations.

### Example with `GROUP BY`
```sql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id;
```


## Comparison of Aggregate Functions Across SQL Implementations

| Feature/Function       | ANSI SQL | PostgreSQL | MySQL (8.0+) | SQL Server | Oracle |
|------------------------|----------|------------|--------------|------------|--------|
| **COUNT()**            | Supported | Supported  | Supported    | Supported  | Supported |
| **SUM()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **AVG()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **MIN()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **MAX()**              | Supported | Supported  | Supported    | Supported  | Supported |
| **COUNT(DISTINCT)**    | Supported | Supported  | Supported    | Supported  | Supported |
| **GROUP_CONCAT()**     | Not Supported | `STRING_AGG()` | Supported    | `STRING_AGG()` | `LISTAGG()` |
| **VARIANCE()**         | Not Supported | Supported  | Supported    | Supported  | Supported |
| **STDDEV()**           | Not Supported | Supported  | Supported    | Supported  | Supported |
| **MEDIAN()**           | Not Supported | Supported  | Supported    | Supported  | Supported |
| **MODE()**             | Not Supported | Supported  | Not Supported| Not Supported | Supported |
| **PERCENTILE_CONT()**  | Not Supported | Supported  | Not Supported| Supported  | Supported |
| **PERCENTILE_DISC()**  | Not Supported | Supported  | Not Supported| Supported  | Supported |
| **CUME_DIST()**        | Not Supported | Supported  | Not Supported| Supported  | Supported |
| **DENSE_RANK()**       | Not Supported | Supported  | Supported    | Supported  | Supported |
| **RANK()**             | Not Supported | Supported  | Supported    | Supported  | Supported |
| **ROW_NUMBER()**       | Not Supported | Supported  | Supported    | Supported  | Supported |
| **NTILE()**            | Not Supported | Supported  | Supported    | Supported  | Supported |

### Notes on Differences

1. **GROUP_CONCAT()**:
   - **ANSI SQL**: Not supported.
   - **PostgreSQL**: Uses `STRING_AGG()` for similar functionality.
   - **MySQL**: Directly supports `GROUP_CONCAT()`.
   - **SQL Server**: Uses `STRING_AGG()` for similar functionality.
   - **Oracle**: Uses `LISTAGG()` for similar functionality.

2. **VARIANCE() and STDDEV()**:
   - **ANSI SQL**: Not supported.
   - Supported across all major databases with similar syntax.

3. **MEDIAN()**:
   - **ANSI SQL**: Not supported.
   - Supported across all major databases with similar syntax.

4. **MODE()**:
   - **ANSI SQL**: Not supported.
   - **PostgreSQL** and **Oracle**: Directly support `MODE()`.
   - **MySQL** and **SQL Server**: Do not have built-in support for `MODE()`.

5. **PERCENTILE_CONT() and PERCENTILE_DISC()**:
   - **ANSI SQL**: Not supported.
   - **PostgreSQL, SQL Server, Oracle**: Support these functions.
   - **MySQL**: Does not support these functions.

6. **CUME_DIST(), DENSE_RANK(), RANK(), ROW_NUMBER(), NTILE()**:
   - **ANSI SQL**: Not supported.
   - Supported across all major databases with similar syntax.

