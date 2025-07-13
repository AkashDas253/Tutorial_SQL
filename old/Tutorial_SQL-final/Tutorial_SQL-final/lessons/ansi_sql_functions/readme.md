## ANSI SQL Functions

SQL functions are used to perform operations on data in a database and return a value. They can be used in SQL queries to calculate, manipulate, or format data. SQL functions are categorized into **Aggregate Functions**, **Scalar Functions**, and **Date and Time Functions**.

### Types of ANSI SQL Functions

| **Function Type**            | **Description**                                                                                           | **Example**                                                       |  
|------------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| **Aggregate Functions**       | Perform a calculation on a set of values and return a single result.                                      | `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`                     |  
| **Scalar Functions**          | Operate on individual values and return a single result for each row.                                     | `UCASE()`, `LCASE()`, `CONCAT()`, `ROUND()`                       |  
| **Date and Time Functions**   | Used to manipulate date and time data types.                                                              | `NOW()`, `CURDATE()`, `DATEPART()`                               |  
| **String Functions**          | Used to manipulate string values.                                                                          | `LENGTH()`, `SUBSTRING()`, `REPLACE()`                            |  
| **Mathematical Functions**    | Used to perform mathematical calculations.                                                                 | `ABS()`, `CEILING()`, `FLOOR()`                                   |  
| **Conversion Functions**      | Convert data from one type to another.                                                                     | `CAST()`, `CONVERT()`                                             |  

---

### **Aggregate Functions**

Aggregate functions operate on a set of rows and return a single result.

| **Function**        | **Description**                                                    | **Example**                                                       |  
|---------------------|--------------------------------------------------------------------|-------------------------------------------------------------------|  
| `COUNT()`           | Returns the number of rows in a specified column or expression.     | `SELECT COUNT(*) FROM employees;`                                 |  
| `SUM()`             | Returns the sum of values in a specified numeric column.            | `SELECT SUM(salary) FROM employees;`                              |  
| `AVG()`             | Returns the average value of a numeric column.                      | `SELECT AVG(salary) FROM employees;`                              |  
| `MIN()`             | Returns the minimum value in a specified column.                    | `SELECT MIN(salary) FROM employees;`                              |  
| `MAX()`             | Returns the maximum value in a specified column.                    | `SELECT MAX(salary) FROM employees;`                              |  
| `GROUP_CONCAT()`     | Concatenates values from multiple rows into a single string.        | `SELECT GROUP_CONCAT(name) FROM employees;`                        |  

**Usage Example**:  
```sql
SELECT AVG(salary) FROM employees WHERE department_id = 2;
```

---

### **Scalar Functions**

Scalar functions operate on individual values and return a single result for each row.

| **Function**        | **Description**                                                    | **Example**                                                       |  
|---------------------|--------------------------------------------------------------------|-------------------------------------------------------------------|  
| `UCASE()`           | Converts a string to uppercase.                                    | `SELECT UCASE(first_name) FROM employees;`                        |  
| `LCASE()`           | Converts a string to lowercase.                                    | `SELECT LCASE(first_name) FROM employees;`                        |  
| `CONCAT()`          | Concatenates two or more strings into one.                          | `SELECT CONCAT(first_name, ' ', last_name) FROM employees;`       |  
| `ROUND()`           | Rounds a numeric value to a specified number of decimal places.    | `SELECT ROUND(salary, 2) FROM employees;`                         |  
| `TRIM()`            | Removes leading and trailing spaces from a string.                  | `SELECT TRIM(first_name) FROM employees;`                         |  
| `REPLACE()`         | Replaces occurrences of a substring within a string.               | `SELECT REPLACE(address, 'Street', 'St.') FROM employees;`        |  

**Usage Example**:  
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employees;
```

---

### **Date and Time Functions**

Date and time functions are used to manipulate date and time values.

| **Function**        | **Description**                                                    | **Example**                                                       |  
|---------------------|--------------------------------------------------------------------|-------------------------------------------------------------------|  
| `NOW()`             | Returns the current date and time.                                 | `SELECT NOW();`                                                   |  
| `CURDATE()`         | Returns the current date (without time).                           | `SELECT CURDATE();`                                               |  
| `DATEPART()`        | Extracts a specific part of a date (e.g., year, month, day).       | `SELECT DATEPART(year, CURDATE());`                               |  
| `DATEDIFF()`        | Returns the difference in days between two dates.                  | `SELECT DATEDIFF('2025-02-18', '2025-01-01');`                    |  
| `DATEADD()`         | Adds a specified time interval to a date.                           | `SELECT DATEADD(day, 5, CURDATE());`                              |  

**Usage Example**:  
```sql
SELECT CURDATE();  -- Returns current date
SELECT DATEPART(month, CURDATE());  -- Returns the current month
```

---

### **String Functions**

String functions are used to manipulate string values.

| **Function**        | **Description**                                                    | **Example**                                                       |  
|---------------------|--------------------------------------------------------------------|-------------------------------------------------------------------|  
| `LENGTH()`          | Returns the length of a string (number of characters).             | `SELECT LENGTH(first_name) FROM employees;`                       |  
| `SUBSTRING()`       | Extracts a substring from a string, starting at a specified position. | `SELECT SUBSTRING(first_name, 1, 3) FROM employees;`              |  
| `REPLACE()`         | Replaces a substring within a string with another substring.       | `SELECT REPLACE(address, 'Street', 'St.') FROM employees;`        |  
| `TRIM()`            | Removes leading and trailing spaces from a string.                  | `SELECT TRIM(first_name) FROM employees;`                         |  
| `INSTR()`           | Returns the position of the first occurrence of a substring in a string. | `SELECT INSTR(first_name, 'a') FROM employees;`                  |  

**Usage Example**:  
```sql
SELECT SUBSTRING(first_name, 1, 3) FROM employees;
```

---

### **Mathematical Functions**

Mathematical functions are used to perform mathematical operations.

| **Function**        | **Description**                                                    | **Example**                                                       |  
|---------------------|--------------------------------------------------------------------|-------------------------------------------------------------------|  
| `ABS()`             | Returns the absolute value of a number.                            | `SELECT ABS(-5);`                                                 |  
| `CEILING()`         | Returns the smallest integer greater than or equal to the number.  | `SELECT CEILING(3.14);`                                           |  
| `FLOOR()`           | Returns the largest integer less than or equal to the number.      | `SELECT FLOOR(3.14);`                                             |  
| `POWER()`           | Returns the value of a number raised to the power of another number. | `SELECT POWER(2, 3);`                                           |  
| `SQRT()`            | Returns the square root of a number.                               | `SELECT SQRT(9);`                                                |  

**Usage Example**:  
```sql
SELECT POWER(2, 3);  -- Result: 8
```

---

### **Conversion Functions**

Conversion functions are used to convert data from one type to another.

| **Function**        | **Description**                                                    | **Example**                                                       |  
|---------------------|--------------------------------------------------------------------|-------------------------------------------------------------------|  
| `CAST()`            | Converts one data type to another.                                | `SELECT CAST(123 AS VARCHAR(10));`                                |  
| `CONVERT()`         | Converts one data type to another (SQL Server-specific).           | `SELECT CONVERT(VARCHAR, 123);`                                   |  

**Usage Example**:  
```sql
SELECT CAST(123 AS VARCHAR(10));  -- Converts 123 to '123'
```

---

### Conclusion

ANSI SQL functions are powerful tools that allow for complex data manipulation. From **aggregate functions** that operate on groups of rows to **scalar functions** that work on individual values, these functions are essential in querying and transforming data. The **date and time**, **string**, **mathematical**, and **conversion functions** provide further flexibility in handling different data types and performing computations.
