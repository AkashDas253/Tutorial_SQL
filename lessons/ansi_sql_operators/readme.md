## ANSI SQL Operators

SQL operators are special symbols or keywords used to perform operations on values in SQL queries. Operators allow for comparison, mathematical calculations, logical operations, and more. The main categories of operators in ANSI SQL include **Arithmetic Operators**, **Comparison Operators**, **Logical Operators**, and **Set Operators**.

### Types of ANSI SQL Operators

| **Operator Type**           | **Description**                                                                                           | **Example**                                                       |  
|-----------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| **Arithmetic Operators**     | Perform mathematical operations like addition, subtraction, multiplication, and division.               | `+`, `-`, `*`, `/`                                                |  
| **Comparison Operators**     | Used to compare two values, returning boolean results.                                                   | `=`, `!=`, `>`, `<`, `>=`, `<=`, `BETWEEN`, `IN`, `LIKE`, `IS NULL` |  
| **Logical Operators**        | Used to combine multiple conditions or expressions and return boolean values.                            | `AND`, `OR`, `NOT`                                                |  
| **Set Operators**            | Used to combine results from multiple queries.                                                           | `UNION`, `INTERSECT`, `EXCEPT`                                    |  
| **String Operators**         | Specific operators for string manipulation.                                                              | `||` (Concatenation)                                              |  
| **Miscellaneous Operators**  | Other operators for specific tasks, such as `ANY` and `ALL`.                                             | `ANY`, `ALL`, `EXISTS`                                            |  

---

### **Arithmetic Operators**

Arithmetic operators perform basic mathematical operations such as addition, subtraction, multiplication, and division.

| **Operator**   | **Description**                                     | **Example**                                                   |  
|----------------|-----------------------------------------------------|---------------------------------------------------------------|  
| `+`            | Adds two numbers or concatenates strings.            | `SELECT 5 + 3;` (Result: `8`)                                  |  
| `-`            | Subtracts the right operand from the left operand.   | `SELECT 10 - 2;` (Result: `8`)                                 |  
| `*`            | Multiplies two numbers.                             | `SELECT 4 * 2;` (Result: `8`)                                  |  
| `/`            | Divides the left operand by the right operand.       | `SELECT 8 / 2;` (Result: `4`)                                  |  
| `%`            | Returns the remainder of a division operation.      | `SELECT 8 % 3;` (Result: `2`)                                  |  

**Usage Example**:  
```sql
SELECT price * quantity AS total_price
FROM orders;
```

---

### **Comparison Operators**

Comparison operators are used to compare two values, returning `TRUE`, `FALSE`, or `UNKNOWN` based on the result.

| **Operator**   | **Description**                                     | **Example**                                                   |  
|----------------|-----------------------------------------------------|---------------------------------------------------------------|  
| `=`            | Equal to.                                           | `SELECT * FROM employees WHERE salary = 50000;`               |  
| `!=` or `<>`   | Not equal to.                                       | `SELECT * FROM employees WHERE salary != 50000;`              |  
| `>`            | Greater than.                                       | `SELECT * FROM employees WHERE salary > 50000;`               |  
| `<`            | Less than.                                          | `SELECT * FROM employees WHERE salary < 50000;`               |  
| `>=`           | Greater than or equal to.                           | `SELECT * FROM employees WHERE salary >= 50000;`              |  
| `<=`           | Less than or equal to.                              | `SELECT * FROM employees WHERE salary <= 50000;`              |  
| `BETWEEN`      | Checks if a value is within a range of two values.   | `SELECT * FROM employees WHERE salary BETWEEN 40000 AND 60000;` |  
| `IN`           | Checks if a value is in a list of values.            | `SELECT * FROM employees WHERE department_id IN (1, 2, 3);`   |  
| `LIKE`         | Matches a pattern in a string (supports wildcards). | `SELECT * FROM employees WHERE name LIKE 'J%';`               |  
| `IS NULL`      | Checks if a value is NULL.                          | `SELECT * FROM employees WHERE salary IS NULL;`               |  

**Usage Example**:  
```sql
SELECT * FROM employees
WHERE department_id IN (1, 2, 3);
```

---

### **Logical Operators**

Logical operators are used to combine multiple conditions in SQL queries and return boolean results.

| **Operator**   | **Description**                                     | **Example**                                                   |  
|----------------|-----------------------------------------------------|---------------------------------------------------------------|  
| `AND`          | Returns `TRUE` if both conditions are true.         | `SELECT * FROM employees WHERE salary > 50000 AND department_id = 2;` |  
| `OR`           | Returns `TRUE` if either condition is true.         | `SELECT * FROM employees WHERE salary > 50000 OR department_id = 2;` |  
| `NOT`          | Reverses the result of a condition.                 | `SELECT * FROM employees WHERE NOT salary > 50000;`            |  

**Usage Example**:  
```sql
SELECT * FROM employees
WHERE salary > 50000 AND department_id = 2;
```

---

### **Set Operators**

Set operators are used to combine the results of two or more SELECT queries. These operators remove duplicates unless `ALL` is used.

| **Operator**   | **Description**                                     | **Example**                                                   |  
|----------------|-----------------------------------------------------|---------------------------------------------------------------|  
| `UNION`        | Combines the results of two queries, removing duplicates. | `SELECT department_id FROM employees UNION SELECT department_id FROM managers;` |  
| `UNION ALL`    | Combines the results of two queries, including duplicates. | `SELECT department_id FROM employees UNION ALL SELECT department_id FROM managers;` |  
| `INTERSECT`    | Returns the common records between two queries.      | `SELECT department_id FROM employees INTERSECT SELECT department_id FROM managers;` |  
| `EXCEPT`       | Returns records from the first query that do not exist in the second query. | `SELECT department_id FROM employees EXCEPT SELECT department_id FROM managers;` |  

**Usage Example**:  
```sql
SELECT department_id FROM employees
UNION
SELECT department_id FROM managers;
```

---

### **String Operators**

String operators are used for string manipulation.

| **Operator**   | **Description**                                     | **Example**                                                   |  
|----------------|-----------------------------------------------------|---------------------------------------------------------------|  
| `\|\|`         | Concatenates two strings.                           | ``SELECT first_name || ' ' || last_name FROM employees;``        |  

**Usage Example**:  
```sql
SELECT first_name || ' ' || last_name AS full_name
FROM employees;
```

---

### **Miscellaneous Operators**

These operators perform special functions for specific tasks in SQL queries.

| **Operator**   | **Description**                                     | **Example**                                                   |  
|----------------|-----------------------------------------------------|---------------------------------------------------------------|  
| `ANY`          | Compares a value to any value in a list or result set. | `SELECT * FROM employees WHERE salary > ANY (SELECT salary FROM employees WHERE department_id = 1);` |  
| `ALL`          | Compares a value to all values in a list or result set. | `SELECT * FROM employees WHERE salary > ALL (SELECT salary FROM employees WHERE department_id = 1);` |  
| `EXISTS`       | Checks if a subquery returns any rows.              | `SELECT * FROM employees WHERE EXISTS (SELECT * FROM departments WHERE id = employees.department_id);` |  

**Usage Example**:  
```sql
SELECT * FROM employees
WHERE salary > ANY (SELECT salary FROM employees WHERE department_id = 1);
```

---

### Conclusion

ANSI SQL operators are vital for performing a wide range of operations in SQL queries. From basic arithmetic to complex logical and set operations, understanding these operators is essential for effective data manipulation and retrieval. Each operator type—**arithmetic**, **comparison**, **logical**, **set**, **string**, and **miscellaneous**—plays a unique role in constructing SQL queries to solve different data-related tasks.
