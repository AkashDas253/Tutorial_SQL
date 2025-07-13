## SQL Syntax in Oracle SQL  

### 1. **Basic Structure of SQL Statements**  
SQL statements generally follow a basic structure of keywords, clauses, and expressions.

#### Syntax Format  
```sql
SELECT column1, column2, ... 
FROM table_name 
WHERE condition
ORDER BY column_name;
```

- **Keywords**: Reserved words (e.g., `SELECT`, `FROM`, `WHERE`, `ORDER BY`)
- **Clauses**: Parts of a SQL query (e.g., `SELECT`, `FROM`, `WHERE`)
- **Expressions**: Values, columns, or functions (e.g., `column1`, `COUNT(*)`)

### 2. **SQL Keywords**  
SQL keywords are reserved words used to perform specific operations on databases.

| **Keyword**   | **Description**                                                | **Example**                                               |
|---------------|----------------------------------------------------------------|-----------------------------------------------------------|
| `SELECT`      | Retrieves data from one or more tables                         | `SELECT * FROM employees;`                                |
| `FROM`        | Specifies the table from which to retrieve the data           | `SELECT * FROM customers;`                                |
| `WHERE`       | Filters records based on a condition                           | `SELECT name FROM employees WHERE age > 30;`              |
| `ORDER BY`    | Sorts the results of the query                                | `SELECT * FROM employees ORDER BY name;`                  |
| `GROUP BY`    | Groups records for aggregate functions                         | `SELECT department, COUNT(*) FROM employees GROUP BY department;` |
| `HAVING`      | Filters records after grouping, often with aggregate functions | `SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 50000;` |
| `INSERT INTO` | Inserts data into a table                                      | `INSERT INTO employees (id, name, salary) VALUES (1, 'John', 50000);` |

### 3. **Identifiers**  
Identifiers refer to names given to database objects like tables, columns, views, etc.

| **Identifier Type** | **Examples**             | **Notes**                                             |
|---------------------|--------------------------|-------------------------------------------------------|
| **Table Names**      | `employees`, `orders`    | Can be alphanumeric and must start with a letter      |
| **Column Names**     | `name`, `age`, `salary`  | Must be enclosed in quotes if case-sensitive          |
| **Alias**            | `SELECT name AS "Employee Name"` | Shortened names for readability in queries       |

### 4. **Literals**  
Literals are fixed values used in SQL queries.

| **Literal Type**   | **Examples**             | **Notes**                                                |
|--------------------|--------------------------|----------------------------------------------------------|
| **String Literals** | `'John'`, `'New York'`   | Enclosed in single quotes.                               |
| **Numeric Literals**| `100`, `3.14`            | Represent numerical values.                              |
| **Date Literals**   | `'2025-01-01'`           | Enclosed in single quotes. Date format can vary.         |

### 5. **SQL Clauses**  
SQL clauses define specific parts of a SQL query.

| **Clause**    | **Purpose**                                                  | **Syntax Example**                                      |
|---------------|--------------------------------------------------------------|--------------------------------------------------------|
| **SELECT**    | Specifies the columns to retrieve                            | `SELECT name, age FROM employees;`                     |
| **FROM**      | Specifies the table from which to retrieve data              | `SELECT * FROM employees;`                             |
| **WHERE**     | Specifies conditions to filter the rows                       | `SELECT * FROM employees WHERE age > 30;`              |
| **GROUP BY**  | Groups rows based on a common attribute                       | `SELECT department, COUNT(*) FROM employees GROUP BY department;` |
| **ORDER BY**  | Orders the result set based on one or more columns            | `SELECT * FROM employees ORDER BY name ASC;`           |

### 6. **Comments in SQL**  
Comments are used to annotate SQL code for better readability.

| **Comment Type** | **Syntax**                              | **Example**                                           |
|------------------|-----------------------------------------|-------------------------------------------------------|
| **Single-Line**  | `--`                                     | `-- This is a comment`                                |
| **Multi-Line**   | `/* comment */`                          | `/* This is a multi-line comment */`                  |

### 7. **Expressions in SQL**  
Expressions are combinations of values, operators, and functions that produce results.

| **Expression Type** | **Examples**             | **Notes**                                                |
|---------------------|--------------------------|----------------------------------------------------------|
| **Arithmetic**       | `salary * 1.1`           | Used to perform mathematical operations.                 |
| **String Concatenation** | `'Mr. ' || name`       | Combines multiple string values.                         |
| **Date Operations**  | `SYSDATE + 30`           | Adds days to a date value.                               |

### 8. **SQL Functions**  
SQL functions perform operations on data and return a result.

| **Function Type**   | **Examples**                  | **Description**                                         |
|---------------------|-------------------------------|---------------------------------------------------------|
| **Aggregate Functions** | `COUNT()`, `SUM()`, `AVG()` | Operates on a group of values and returns a single result. |
| **String Functions** | `CONCAT()`, `LENGTH()`        | Manipulates string values.                              |
| **Date Functions**   | `SYSDATE`, `CURRENT_DATE()`   | Manipulates date and time values.                       |
| **Numeric Functions**| `ROUND()`, `MOD()`            | Performs operations on numeric data.                    |

### 9. **SQL Execution Order**  
The typical order in which SQL statements are processed:

1. `FROM`
2. `WHERE`
3. `GROUP BY`
4. `HAVING`
5. `SELECT`
6. `ORDER BY`

### 10. **SQL Syntax for Special Statements**  
- **Using `DISTINCT` to avoid duplicates**  
```sql
SELECT DISTINCT column_name FROM table_name;
```

- **Using `LIMIT`/`FETCH FIRST` for row limits**  
```sql
SELECT * FROM employees FETCH FIRST 10 ROWS ONLY;
```

### Example Query  
```sql
SELECT name, age FROM employees 
WHERE department = 'HR' 
ORDER BY age DESC;
```

### Notes:
- **Case Sensitivity**: SQL keywords are case-insensitive, but table and column names are case-sensitive unless quoted.
- **Reserved Words**: Certain words are reserved in SQL (e.g., `SELECT`, `FROM`, `WHERE`) and cannot be used as table or column names without quoting.
