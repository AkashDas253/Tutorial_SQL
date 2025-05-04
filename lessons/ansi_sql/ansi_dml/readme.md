## ANSI Data Manipulation Language (DML)

DML is a subset of SQL used to manage and manipulate data within existing database structures. It allows users to perform operations such as querying, inserting, updating, and deleting data from tables. Unlike DDL, which deals with database structure, DML focuses on the data inside the tables.

### DML Commands

| **Command**            | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `SELECT`               | Retrieves data from one or more tables.                                                                  | `SELECT * FROM employees;`                                          |  
| `INSERT INTO`          | Adds new records into a table.                                                                            | `INSERT INTO employees (name, age) VALUES ('John Doe', 28);`        |  
| `UPDATE`               | Modifies existing records in a table.                                                                     | `UPDATE employees SET age = 30 WHERE name = 'John Doe';`            |  
| `DELETE FROM`          | Removes records from a table.                                                                             | `DELETE FROM employees WHERE age < 30;`                              |  

---

### `SELECT` Command

The `SELECT` statement is used to query data from one or more tables.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `SELECT`               | Specifies the columns to retrieve.                                                                       | `SELECT name, age`                                                  |  
| `FROM`                 | Specifies the table(s) from which to retrieve data.                                                      | `FROM employees`                                                    |  
| `WHERE`                | Filters results based on a condition.                                                                    | `WHERE age > 30`                                                    |  
| `ORDER BY`             | Sorts the results based on one or more columns.                                                          | `ORDER BY name ASC`                                                 |  
| `LIMIT`                | Limits the number of rows returned.                                                                      | `LIMIT 10`                                                          |  

**Usage Example**:  
```sql
SELECT name, age 
FROM employees 
WHERE age > 30 
ORDER BY name ASC 
LIMIT 5;
```

---

### `INSERT INTO` Command

The `INSERT INTO` statement is used to add new records into a table.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `INSERT INTO`          | Specifies the table to insert data into.                                                                  | `INSERT INTO employees`                                             |  
| `column_name`          | Specifies the column names to insert data into.                                                          | `name, age`                                                         |  
| `VALUES`               | Specifies the values to be inserted into the respective columns.                                          | `'John Doe', 28`                                                    |  

**Usage Example**:  
```sql
INSERT INTO employees (name, age) 
VALUES ('John Doe', 28);
```

#### Inserting Multiple Records

You can insert multiple rows in a single query.

**Usage Example**:  
```sql
INSERT INTO employees (name, age) 
VALUES ('John Doe', 28), ('Jane Doe', 32), ('Sam Smith', 25);
```

---

### `UPDATE` Command

The `UPDATE` statement is used to modify existing records in a table.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `UPDATE`               | Specifies the table to modify.                                                                           | `UPDATE employees`                                                  |  
| `SET`                  | Specifies the column(s) to update and their new values.                                                  | `SET age = 30`                                                      |  
| `WHERE`                | Specifies the condition to identify the rows to be updated.                                              | `WHERE name = 'John Doe'`                                           |  

**Usage Example**:  
```sql
UPDATE employees 
SET age = 30 
WHERE name = 'John Doe';
```

---

### `DELETE` Command

The `DELETE` statement is used to remove records from a table.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `DELETE FROM`          | Specifies the table to delete records from.                                                              | `DELETE FROM employees`                                             |  
| `WHERE`                | Specifies the condition to identify the rows to be deleted.                                              | `WHERE age < 30`                                                    |  

**Usage Example**:  
```sql
DELETE FROM employees 
WHERE age < 30;
```

#### Deleting All Records

If the `WHERE` clause is omitted, all records from the table will be deleted.

**Usage Example**:  
```sql
DELETE FROM employees;
```

---

### DML Functions & Clauses

#### 1. **DISTINCT**

The `DISTINCT` keyword is used to return only unique (distinct) values from a query.

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `DISTINCT`             | Filters out duplicate records from the result set.                                                       | `SELECT DISTINCT name FROM employees;`                              |  

#### 2. **GROUP BY**

The `GROUP BY` clause groups rows that have the same values into summary rows, like finding the total or average.

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `GROUP BY`             | Groups rows that have the same values in one or more columns.                                            | `SELECT department, COUNT(*) FROM employees GROUP BY department;`  |  

#### 3. **HAVING**

The `HAVING` clause is used to filter records after the `GROUP BY` has been applied.

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `HAVING`               | Filters groups of rows based on conditions.                                                              | `HAVING COUNT(*) > 5`                                               |  

---

### Conclusion

DML is essential for data manipulation within a database, providing commands for inserting, querying, updating, and deleting data. These operations are crucial for maintaining and interacting with the data stored in relational databases.
