
## Common SQL Functions for Working with NULL Values

### 1. IS NULL
- `column_name IS NULL`  # Check if a column value is NULL

### 2. IS NOT NULL
- `column_name IS NOT NULL`  # Check if a column value is not NULL

### 3. COALESCE
- `COALESCE(expression1, expression2, ...)`  # Return the first non-NULL expression

### 4. NULLIF
- `NULLIF(expression1, expression2)`  # Return NULL if the two expressions are equal, otherwise return the first expression

### 5. IFNULL
- `IFNULL(expression, value)`  # Return the value if the expression is NULL (MySQL specific)

### 6. NVL
- `NVL(expression, value)`  # Return the value if the expression is NULL (Oracle specific)

### 7. NVL2
- `NVL2(expression, value_if_not_null, value_if_null)`  # Return different values depending on whether the expression is NULL (Oracle specific)

### 8. ISNULL
- `ISNULL(expression, value)`  # Return the value if the expression is NULL (SQL Server specific)

### 9. LNNVL
- `LNNVL(condition)`  # Return TRUE if the condition is FALSE or UNKNOWN (Oracle specific)

### 10. DECODE
- `DECODE(expression, search, result, ..., default)`  # Return different results based on the value of the expression, with handling for NULL (Oracle specific)