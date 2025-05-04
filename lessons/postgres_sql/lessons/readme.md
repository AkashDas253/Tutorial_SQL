
## **SQL Syntax in PostgreSQL (PGSQL)**  

### **Basic Structure of SQL Statements**  
SQL statements in PostgreSQL follow a structure of keywords, clauses, and expressions.

#### **Syntax Format**  
```sql
SELECT column1, column2, ... 
FROM table_name 
WHERE condition
ORDER BY column_name;
```

- **Keywords**: Reserved words like `SELECT`, `FROM`, `WHERE`, `ORDER BY`.  
- **Clauses**: Specific components of an SQL statement like `SELECT`, `FROM`, `WHERE`.  
- **Expressions**: Values, columns, or calculations like `column1`, `COUNT(*)`.  

---

### **SQL Keywords in PostgreSQL**  
SQL keywords perform operations on databases.

| **Keyword**   | **Description**                                                | **Example**                                               |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------|
| `SELECT`     | Retrieves data from one or more tables                         | `SELECT * FROM employees;`                                |
| `FROM`       | Specifies the table from which to retrieve the data            | `SELECT * FROM customers;`                                |
| `WHERE`      | Filters records based on a condition                           | `SELECT name FROM employees WHERE age > 30;`              |
| `ORDER BY`   | Sorts the results of the query                                | `SELECT * FROM employees ORDER BY name;`                  |
| `GROUP BY`   | Groups records for aggregate functions                         | `SELECT department, COUNT(*) FROM employees GROUP BY department;` |
| `HAVING`     | Filters records after grouping, often with aggregate functions | `SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 50000;` |
| `INSERT INTO`| Inserts data into a table                                      | `INSERT INTO employees (id, name, salary) VALUES (1, 'John', 50000);` |
| `UPDATE`     | Modifies existing records in a table                           | `UPDATE employees SET salary = 60000 WHERE id = 1;`       |
| `DELETE`     | Removes records from a table                                  | `DELETE FROM employees WHERE id = 1;`                     |

---

### **Identifiers in PostgreSQL**  
Identifiers are names assigned to database objects.

| **Identifier Type** | **Examples**             | **Notes**                                           |
|---------------------|--------------------------|-----------------------------------------------------|
| **Table Names**     | `employees`, `orders`    | Alphanumeric, must start with a letter             |
| **Column Names**    | `name`, `age`, `salary`  | Case-sensitive when quoted `"Name"` vs. `name`     |
| **Alias**           | `SELECT name AS "Employee Name"` | Shortened names for better readability |

---

### **Literals in PostgreSQL**  
Literals are fixed values used in SQL queries.

| **Literal Type**   | **Examples**             | **Notes**                                  |
|--------------------|--------------------------|--------------------------------------------|
| **String Literals** | `'John'`, `'New York'`   | Enclosed in single quotes                 |
| **Numeric Literals**| `100`, `3.14`            | Represents numerical values               |
| **Date Literals**   | `'2025-01-01'`           | Enclosed in single quotes                 |

---

### **SQL Clauses in PostgreSQL**  
SQL clauses define specific parts of an SQL query.

| **Clause**    | **Purpose**                                                  | **Syntax Example**                                      |
|--------------|--------------------------------------------------------------|--------------------------------------------------------|
| **SELECT**   | Specifies the columns to retrieve                            | `SELECT name, age FROM employees;`                     |
| **FROM**     | Specifies the table from which to retrieve data              | `SELECT * FROM employees;`                             |
| **WHERE**    | Specifies conditions to filter the rows                      | `SELECT * FROM employees WHERE age > 30;`              |
| **GROUP BY** | Groups rows based on a common attribute                      | `SELECT department, COUNT(*) FROM employees GROUP BY department;` |
| **ORDER BY** | Orders the result set based on one or more columns           | `SELECT * FROM employees ORDER BY name ASC;`           |
| **LIMIT**    | Limits the number of rows returned                           | `SELECT * FROM employees LIMIT 5;`                     |
| **OFFSET**   | Skips a number of rows before returning results              | `SELECT * FROM employees OFFSET 5;`                    |

---

### **Comments in PostgreSQL**  
Comments help annotate SQL code for better readability.

| **Comment Type** | **Syntax**                               | **Example**                           |
|-----------------|-----------------------------------------|--------------------------------------|
| **Single-Line** | `-- comment`                            | `-- This is a comment`              |
| **Multi-Line**  | `/* comment */`                        | `/* This is a multi-line comment */`|

---

### **Expressions in PostgreSQL**  
Expressions combine values, operators, and functions.

| **Expression Type**     | **Examples**              | **Notes**                                        |
|------------------------|--------------------------|------------------------------------------------|
| **Arithmetic**        | `salary * 1.1`           | Used for mathematical operations              |
| **String Concatenation** | `'Mr. ' || name`        | Combines multiple string values               |
| **Date Operations**   | `CURRENT_DATE + INTERVAL '30 days'` | Adds 30 days to current date |

---

### **Functions in PostgreSQL**  
SQL functions perform operations on data.

| **Function Type**   | **Examples**                  | **Description**                                         |
|---------------------|------------------------------|---------------------------------------------------------|
| **Aggregate**      | `COUNT()`, `SUM()`, `AVG()`  | Operates on a group of values and returns a single result |
| **String**         | `CONCAT()`, `LENGTH()`       | Manipulates string values                               |
| **Date**          | `NOW()`, `CURRENT_DATE`      | Manipulates date and time values                       |
| **Numeric**       | `ROUND()`, `MOD()`           | Performs numeric calculations                          |

---

### **SQL Execution Order in PostgreSQL**  
SQL queries in PostgreSQL are processed in this order:

1. `FROM`  
2. `WHERE`  
3. `GROUP BY`  
4. `HAVING`  
5. `SELECT`  
6. `ORDER BY`  
7. `LIMIT` / `OFFSET`

---

### **Special SQL Syntax in PostgreSQL**  

#### **Using `DISTINCT` to avoid duplicates**  
```sql
SELECT DISTINCT column_name FROM table_name;
```

#### **Using `LIMIT` and `OFFSET`**  
```sql
SELECT * FROM employees LIMIT 10 OFFSET 5;
```

#### **Using `RETURNING` in `INSERT`, `UPDATE`, and `DELETE`**  
```sql
INSERT INTO employees (name, age) VALUES ('Alice', 25) RETURNING id;
UPDATE employees SET salary = salary * 1.1 WHERE id = 1 RETURNING salary;
DELETE FROM employees WHERE id = 1 RETURNING *;
```

---

### **Example Query**  
```sql
SELECT name, age FROM employees 
WHERE department = 'HR' 
ORDER BY age DESC 
LIMIT 5;
```

---

### **Notes:**
- **Case Sensitivity**: SQL keywords are case-insensitive, but column and table names are case-sensitive unless quoted.  
- **Reserved Words**: Words like `SELECT`, `FROM`, `WHERE` are reserved and require quoting if used as identifiers.  
- **Performance**: Use indexing (`CREATE INDEX`) for optimizing queries with `WHERE`, `ORDER BY`, and `JOIN`.  

---
