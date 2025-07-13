## SQL Operators in Oracle SQL

### 1. **Arithmetic Operators**  
Arithmetic operators are used to perform mathematical operations on numeric values.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `+`            | Addition                                              | `SELECT 5 + 3 FROM dual;` returns `8`                      |
| `-`            | Subtraction                                           | `SELECT 10 - 4 FROM dual;` returns `6`                     |
| `*`            | Multiplication                                        | `SELECT 4 * 2 FROM dual;` returns `8`                      |
| `/`            | Division                                              | `SELECT 10 / 2 FROM dual;` returns `5`                     |
| `%`            | Modulo (remainder after division)                     | `SELECT 10 % 3 FROM dual;` returns `1`                     |

#### Usage Example:
```sql
SELECT salary + 1000 AS new_salary FROM employees;
```

### 2. **Comparison Operators**  
Comparison operators are used to compare two values or expressions.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `=`            | Equal to                                              | `SELECT * FROM employees WHERE age = 30;`                 |
| `!=` or `<>`   | Not equal to                                          | `SELECT * FROM employees WHERE age != 30;`                |
| `>`            | Greater than                                          | `SELECT * FROM employees WHERE salary > 5000;`            |
| `<`            | Less than                                             | `SELECT * FROM employees WHERE salary < 5000;`            |
| `>=`           | Greater than or equal to                              | `SELECT * FROM employees WHERE salary >= 5000;`           |
| `<=`           | Less than or equal to                                 | `SELECT * FROM employees WHERE salary <= 5000;`           |

#### Usage Example:
```sql
SELECT name FROM employees WHERE age >= 30;
```

### 3. **Logical Operators**  
Logical operators are used to combine multiple conditions in a `WHERE` clause.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `AND`          | Returns true if both conditions are true              | `SELECT * FROM employees WHERE age > 30 AND salary > 5000;` |
| `OR`           | Returns true if at least one condition is true        | `SELECT * FROM employees WHERE age > 30 OR salary > 5000;`  |
| `NOT`          | Reverses the result of a condition                    | `SELECT * FROM employees WHERE NOT salary > 5000;`         |

#### Usage Example:
```sql
SELECT * FROM employees WHERE age > 30 AND department = 'IT';
```

### 4. **Set Operators**  
Set operators combine the results of two or more `SELECT` statements.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `UNION`        | Combines the results of two `SELECT` queries, removing duplicates | `SELECT name FROM employees WHERE department = 'IT' UNION SELECT name FROM employees WHERE department = 'HR';` |
| `UNION ALL`    | Combines the results of two `SELECT` queries, including duplicates | `SELECT name FROM employees WHERE department = 'IT' UNION ALL SELECT name FROM employees WHERE department = 'HR';` |
| `INTERSECT`    | Returns the common rows from two `SELECT` queries    | `SELECT name FROM employees WHERE department = 'IT' INTERSECT SELECT name FROM employees WHERE age > 30;` |
| `MINUS`        | Returns the rows from the first `SELECT` query that do not appear in the second query | `SELECT name FROM employees WHERE department = 'IT' MINUS SELECT name FROM employees WHERE salary < 5000;` |

#### Usage Example:
```sql
SELECT department FROM employees WHERE salary > 5000
UNION
SELECT department FROM employees WHERE age > 30;
```

### 5. **String Operators**  
String operators are used to manipulate text data.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `||`           | Concatenation operator; used to combine two strings   | `SELECT first_name || ' ' || last_name FROM employees;`    |
| `LIKE`         | Searches for a specified pattern in a column         | `SELECT * FROM employees WHERE name LIKE 'J%';`            |
| `BETWEEN`      | Selects values within a range                         | `SELECT * FROM employees WHERE salary BETWEEN 5000 AND 10000;` |

#### Usage Example:
```sql
SELECT first_name || ' ' || last_name AS full_name FROM employees;
```

### 6. **Null-Related Operators**  
These operators are used to handle `NULL` values in SQL queries.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `IS NULL`      | Tests if a value is `NULL`                           | `SELECT * FROM employees WHERE middle_name IS NULL;`      |
| `IS NOT NULL`  | Tests if a value is not `NULL`                       | `SELECT * FROM employees WHERE middle_name IS NOT NULL;`  |

#### Usage Example:
```sql
SELECT name FROM employees WHERE phone_number IS NULL;
```

### 7. **Existence Operators**  
These operators are used to test the existence of rows returned by a subquery.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `EXISTS`       | Returns true if a subquery returns one or more rows  | `SELECT * FROM employees WHERE EXISTS (SELECT 1 FROM department WHERE department_name = 'IT');` |
| `IN`           | Checks if a value matches any value in a list or subquery result | `SELECT * FROM employees WHERE department_id IN (1, 2, 3);` |

#### Usage Example:
```sql
SELECT * FROM employees WHERE department_id IN (1, 2, 3);
```

### 8. **Conditional Operators**  
Conditional operators are used to execute conditional expressions.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `CASE`         | Performs conditional logic (like an if-else statement) | `SELECT CASE WHEN salary > 5000 THEN 'High' ELSE 'Low' END AS salary_range FROM employees;` |
| `DECODE`       | Performs a lookup of values based on a condition (similar to `CASE`) | `SELECT DECODE(department_id, 1, 'HR', 2, 'IT', 'Other') FROM employees;` |

#### Usage Example:
```sql
SELECT name, 
       CASE WHEN salary > 5000 THEN 'High' ELSE 'Low' END AS salary_range 
FROM employees;
```

### 9. **Bitwise Operators**  
Bitwise operators perform bit-level operations on integers.

| **Operator**   | **Description**                                      | **Usage Example**                                         |
|----------------|------------------------------------------------------|-----------------------------------------------------------|
| `&`            | Bitwise AND operation                                | `SELECT 5 & 3 FROM dual;` returns `1`                      |
| `|`            | Bitwise OR operation                                 | `SELECT 5 | 3 FROM dual;` returns `7`                      |
| `^`            | Bitwise XOR operation                                | `SELECT 5 ^ 3 FROM dual;` returns `6`                      |
| `~`            | Bitwise NOT operation                                | `SELECT ~5 FROM dual;` returns `-6`                       |
| `<<`           | Bitwise left shift operation                         | `SELECT 5 << 2 FROM dual;` returns `20`                    |
| `>>`           | Bitwise right shift operation                        | `SELECT 5 >> 2 FROM dual;` returns `1`                     |

#### Usage Example:
```sql
SELECT 7 & 3 AS result FROM dual;
```

---

### Notes:
- **Precedence**: The precedence of operators can affect the outcome of expressions. Arithmetic operators have higher precedence than comparison operators, which in turn have higher precedence than logical operators.
- **NULL Handling**: `NULL` is treated as an unknown value. Using operators like `IS NULL` or `IS NOT NULL` is essential when working with columns that may contain `NULL` values.
