## ANSI Joins

ANSI Joins are used to combine records from two or more tables based on related columns between them. Joins are fundamental for querying multiple tables to retrieve relevant data in a single result set. There are different types of joins in SQL, each serving different use cases.

### Types of ANSI Joins

| **Join Type**            | **Description**                                                                                           | **Example**                                                        |  
|--------------------------|-----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|  
| `INNER JOIN`             | Returns records that have matching values in both tables.                                                   | `SELECT * FROM employees INNER JOIN departments ON employees.dept_id = departments.id;`    |  
| `LEFT JOIN` (or `LEFT OUTER JOIN`) | Returns all records from the left table and the matched records from the right table. If no match is found, NULL values are returned for the right table. | `SELECT * FROM employees LEFT JOIN departments ON employees.dept_id = departments.id;`      |  
| `RIGHT JOIN` (or `RIGHT OUTER JOIN`) | Returns all records from the right table and the matched records from the left table. If no match is found, NULL values are returned for the left table. | `SELECT * FROM employees RIGHT JOIN departments ON employees.dept_id = departments.id;`     |  
| `FULL JOIN` (or `FULL OUTER JOIN`)   | Returns all records when there is a match in either the left or right table. If no match is found, NULL values are returned for the non-matching side. | `SELECT * FROM employees FULL JOIN departments ON employees.dept_id = departments.id;`      |  
| `CROSS JOIN`             | Returns the Cartesian product of the two tables. Every row from the first table is combined with every row from the second table. | `SELECT * FROM employees CROSS JOIN departments;`                 |  
| `SELF JOIN`              | Joins a table with itself. It requires table aliases to differentiate the instances of the table.         | `SELECT A.name, B.name FROM employees A, employees B WHERE A.manager_id = B.id;`   |  

---

### `INNER JOIN`

The `INNER JOIN` is the most common type of join. It returns records that have matching values in both tables involved in the join. If there is no match, the row is excluded from the result.

#### Syntax Overview

| **Clause**           | **Description**                                                                                         | **Example**                                                        |  
|----------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|  
| `INNER JOIN`         | Combines rows from both tables where there is a match between the specified columns.                     | `SELECT * FROM table1 INNER JOIN table2 ON table1.column = table2.column;`   |  

**Usage Example**:  
```sql
SELECT employees.name, departments.name
FROM employees
INNER JOIN departments
ON employees.dept_id = departments.id;
```

---

### `LEFT JOIN` (or `LEFT OUTER JOIN`)

The `LEFT JOIN` returns all rows from the left table (the first table), along with the matching rows from the right table (the second table). If no match is found in the right table, the result is `NULL` for the columns of the right table.

#### Syntax Overview

| **Clause**           | **Description**                                                                                         | **Example**                                                        |  
|----------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|  
| `LEFT JOIN`          | Returns all rows from the left table and matching rows from the right table. If there is no match, NULL values are returned for the right table. | `SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column;`  |  

**Usage Example**:  
```sql
SELECT employees.name, departments.name
FROM employees
LEFT JOIN departments
ON employees.dept_id = departments.id;
```

---

### `RIGHT JOIN` (or `RIGHT OUTER JOIN`)

The `RIGHT JOIN` works similarly to `LEFT JOIN`, except it returns all rows from the right table and the matching rows from the left table. If no match is found in the left table, `NULL` values are returned for the left table's columns.

#### Syntax Overview

| **Clause**           | **Description**                                                                                         | **Example**                                                        |  
|----------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|  
| `RIGHT JOIN`         | Returns all rows from the right table and matching rows from the left table. If there is no match, NULL values are returned for the left table. | `SELECT * FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;`  |  

**Usage Example**:  
```sql
SELECT employees.name, departments.name
FROM employees
RIGHT JOIN departments
ON employees.dept_id = departments.id;
```

---

### `FULL JOIN` (or `FULL OUTER JOIN`)

The `FULL JOIN` returns all records when there is a match in either the left or right table. If there is no match, `NULL` values are returned for the non-matching side.

#### Syntax Overview

| **Clause**           | **Description**                                                                                         | **Example**                                                        |  
|----------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|  
| `FULL JOIN`          | Returns all rows from both the left and right tables. If no match is found, NULL values are returned for the non-matching side. | `SELECT * FROM table1 FULL JOIN table2 ON table1.column = table2.column;`  |  

**Usage Example**:  
```sql
SELECT employees.name, departments.name
FROM employees
FULL JOIN departments
ON employees.dept_id = departments.id;
```

---

### `CROSS JOIN`

The `CROSS JOIN` returns the Cartesian product of two tables. Every row from the first table is combined with every row from the second table. This join does not require any condition to join the tables.

#### Syntax Overview

| **Clause**           | **Description**                                                                                         | **Example**                                                        |  
|----------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|  
| `CROSS JOIN`         | Returns the Cartesian product of the two tables (every row of the first table is joined with every row of the second table). | `SELECT * FROM table1 CROSS JOIN table2;`  |  

**Usage Example**:  
```sql
SELECT employees.name, departments.name
FROM employees
CROSS JOIN departments;
```

---

### `SELF JOIN`

A `SELF JOIN` is a join where a table is joined with itself. It is used when a table has a relationship with itself, such as an employee table where each employee has a manager who is also an employee.

#### Syntax Overview

| **Clause**           | **Description**                                                                                         | **Example**                                                        |  
|----------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|  
| `SELF JOIN`          | Joins a table with itself using table aliases.                                                          | `SELECT A.name, B.name FROM table1 A, table1 B WHERE A.column = B.column;` |  

**Usage Example**:  
```sql
SELECT A.name AS Employee, B.name AS Manager
FROM employees A, employees B
WHERE A.manager_id = B.id;
```

---

### Conclusion

ANSI Joins are essential for combining data from multiple tables in relational databases. The different types of joins—`INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`, `CROSS JOIN`, and `SELF JOIN`—provide flexibility in how data can be retrieved based on different matching conditions between tables.
