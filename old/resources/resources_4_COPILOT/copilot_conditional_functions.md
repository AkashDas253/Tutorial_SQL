# Conditional Functions

Conditional functions allow SQL developers to execute logic based on specific conditions. They enable queries to adapt dynamically to varying data values or requirements.


## Conditional Functions

### 1. `CASE`
- **Description**: Performs conditional evaluations and returns a value based on the first satisfied condition.
- **General Syntax**:
  ```sql
  CASE 
      WHEN condition1 THEN result1
      WHEN condition2 THEN result2
      ...
      ELSE default_result
  END
  ```
- **Example**:
  ```sql
  SELECT 
      product_id,
      CASE 
          WHEN price > 100 THEN 'Expensive'
          WHEN price BETWEEN 50 AND 100 THEN 'Moderate'
          ELSE 'Cheap'
      END AS price_category
  FROM products;
  ```

### 2. `IF()`
- **Description**: A shorthand for simple conditional evaluations. Commonly used in MySQL.
- **Syntax**:
  ```sql
  IF(condition, true_value, false_value)
  ```
- **Example**:
  ```sql
  SELECT IF(quantity > 50, 'High Stock', 'Low Stock') AS stock_status
  FROM inventory;
  ```

### 3. `IFNULL()`
- **Description**: Returns a specified value if the input expression is `NULL`. Commonly used in MySQL and PostgreSQL.
- **Syntax**:
  ```sql
  IFNULL(expression, default_value)
  ```
- **Example**:
  ```sql
  SELECT IFNULL(discount, 0) AS discount_value
  FROM sales;
  ```

### 4. `NULLIF()`
- **Description**: Compares two expressions and returns `NULL` if they are equal; otherwise, returns the first expression.
- **Syntax**:
  ```sql
  NULLIF(expression1, expression2)
  ```
- **Example**:
  ```sql
  SELECT NULLIF(sales, 0) AS safe_sales
  FROM revenue;
  ```

### 5. `COALESCE()`
- **Description**: Returns the first non-`NULL` value from a list of expressions.
- **Syntax**:
  ```sql
  COALESCE(expression1, expression2, ..., default_value)
  ```
- **Example**:
  ```sql
  SELECT COALESCE(phone, email, 'No Contact Info') AS preferred_contact
  FROM customers;
  ```

### 6. `IIF()`
- **Description**: A shorthand for conditional evaluation, similar to `IF`, but specific to SQL Server.
- **Syntax**:
  ```sql
  IIF(condition, true_value, false_value)
  ```
- **Example**:
  ```sql
  SELECT IIF(salary > 5000, 'High Earner', 'Low Earner') AS salary_status
  FROM employees;
  ```



## Comparison of Conditional Functions Across SQL Implementations

| Function/Feature      | ANSI SQL      | MySQL              | SQL Server       | Oracle          | PostgreSQL       |
|-----------------------|---------------|--------------------|------------------|-----------------|------------------|
| **CASE**              | Supported     | Supported          | Supported        | Supported       | Supported        |
| **IF()**              | Not Supported | Supported          | Not Supported    | Not Supported   | Not Supported    |
| **IFNULL()**          | Not Supported | Supported          | Not Supported    | Not Supported   | Supported        |
| **NULLIF()**          | Supported     | Supported          | Supported        | Supported       | Supported        |
| **COALESCE()**        | Supported     | Supported          | Supported        | Supported       | Supported        |
| **IIF()**             | Not Supported | Not Supported      | Supported        | Not Supported   | Not Supported    |


## Key Notes and Use Cases

1. **General Condition Handling**:
   - `CASE` is ANSI SQL-compliant and universally supported for complex conditions.
2. **Simple Conditions**:
   - MySQL provides `IF()` as a shorthand for single conditions.
3. **Null Handling**:
   - `IFNULL()` and `COALESCE()` are useful for handling missing or null values.
   - `COALESCE()` is more versatile as it works with multiple expressions.
4. **Equality-Based Null Handling**:
   - `NULLIF()` is useful when you want to replace specific values with `NULL` dynamically.
5. **Shorthand Conditional**:
   - `IIF()` in SQL Server is concise but not as flexible as `CASE`.


### Example Query Combining Functions
```sql
SELECT 
    customer_id,
    COALESCE(phone, email, 'No Contact') AS contact_info,
    CASE 
        WHEN total_spent > 1000 THEN 'VIP'
        ELSE 'Regular'
    END AS customer_type,
    NULLIF(discount, 0) AS valid_discount,
    IIF(total_orders > 10, 'Frequent Buyer', 'Occasional Buyer') AS order_category
FROM customers;
```
