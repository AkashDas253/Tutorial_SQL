## Data Definition in Oracle SQL

### 1. **CREATE**
The `CREATE` statement is used to define new database objects like tables, indexes, views, or schemas.

#### 1.1 **CREATE TABLE**
Used to create a new table in the database.

| **Property**        | **Description**                                            | **Usage Example**                                         |
|---------------------|------------------------------------------------------------|-----------------------------------------------------------|
| **Basic Table**      | Defines a table structure with column names and data types | `CREATE TABLE employees (id INT PRIMARY KEY, name VARCHAR(50), salary DECIMAL(10,2));` |
| **With Constraints** | Specifies constraints such as `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL` | `CREATE TABLE employees (id INT PRIMARY KEY, name VARCHAR(50) NOT NULL, department_id INT, FOREIGN KEY (department_id) REFERENCES departments(id));` |
| **With Default Values** | Columns can have default values | `CREATE TABLE employees (id INT PRIMARY KEY, name VARCHAR(50) DEFAULT 'Unknown');` |

#### Usage Example:
```sql
-- Create a table with primary key and foreign key constraints
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(id)
);
```

#### 1.2 **CREATE INDEX**
Creates an index on a table to improve query performance.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Simple Index**      | Creates a basic index for faster data retrieval           | `CREATE INDEX idx_employee_name ON employees (name);`      |
| **Unique Index**      | Creates an index that ensures the values are unique       | `CREATE UNIQUE INDEX idx_employee_id ON employees (id);`  |
| **Composite Index**   | Creates an index on multiple columns                      | `CREATE INDEX idx_employee_salary_dept ON employees (salary, department_id);` |

#### Usage Example:
```sql
-- Create a simple index on the 'name' column
CREATE INDEX idx_employee_name ON employees (name);
```

#### 1.3 **CREATE VIEW**
A view is a virtual table based on the result of a query.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic View**        | Creates a view from a query                               | `CREATE VIEW employee_details AS SELECT id, name, salary FROM employees;` |
| **With Complex Queries** | Creates a view based on complex queries involving joins and conditions | `CREATE VIEW dept_employee_details AS SELECT e.id, e.name, d.department_name FROM employees e JOIN departments d ON e.department_id = d.id;` |

#### Usage Example:
```sql
-- Create a view for employee details
CREATE VIEW employee_details AS
SELECT id, name, salary
FROM employees
WHERE salary > 5000;
```

### 2. **ALTER**
The `ALTER` statement is used to modify an existing database object, such as a table, column, or constraint.

#### 2.1 **ALTER TABLE**
Used to add, drop, or modify columns and constraints in a table.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Add Column**        | Adds a new column to an existing table                    | `ALTER TABLE employees ADD hire_date DATE;`               |
| **Modify Column**     | Changes the data type or constraints of an existing column | `ALTER TABLE employees MODIFY salary DECIMAL(12, 2);`     |
| **Drop Column**       | Removes a column from a table                            | `ALTER TABLE employees DROP COLUMN hire_date;`            |
| **Add Constraint**    | Adds a new constraint (e.g., UNIQUE, CHECK) to a table    | `ALTER TABLE employees ADD CONSTRAINT salary_check CHECK (salary > 0);` |
| **Drop Constraint**   | Removes an existing constraint                           | `ALTER TABLE employees DROP CONSTRAINT salary_check;`     |

#### Usage Example:
```sql
-- Add a new column to an existing table
ALTER TABLE employees ADD hire_date DATE;

-- Modify the data type of an existing column
ALTER TABLE employees MODIFY salary DECIMAL(12, 2);
```

### 3. **DROP**
The `DROP` statement is used to remove database objects like tables, views, or indexes from the database.

#### 3.1 **DROP TABLE**
Removes a table and all its data.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic Drop**        | Deletes a table from the database                        | `DROP TABLE employees;`                                    |
| **Cascade**           | Deletes the table and all objects dependent on it        | `DROP TABLE employees CASCADE CONSTRAINTS;`                |

#### Usage Example:
```sql
-- Drop a table from the database
DROP TABLE employees;

-- Drop a table with cascade to remove dependent objects
DROP TABLE employees CASCADE CONSTRAINTS;
```

#### 3.2 **DROP INDEX**
Removes an index from a table.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic Drop Index**  | Deletes an index from the database                        | `DROP INDEX idx_employee_name;`                            |

#### Usage Example:
```sql
-- Drop an index from the database
DROP INDEX idx_employee_name;
```

#### 3.3 **DROP VIEW**
Removes a view from the database.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic Drop View**   | Deletes a view from the database                         | `DROP VIEW employee_details;`                             |

#### Usage Example:
```sql
-- Drop a view from the database
DROP VIEW employee_details;
```

### 4. **TRUNCATE**
The `TRUNCATE` statement removes all rows from a table but keeps the table structure intact.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Truncate Table**    | Removes all rows from a table, cannot be rolled back     | `TRUNCATE TABLE employees;`                               |

#### Usage Example:
```sql
-- Truncate a table (removes all records but not the structure)
TRUNCATE TABLE employees;
```

### 5. **RENAME**
The `RENAME` statement is used to rename a database object, such as a table or column.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Rename Table**      | Renames a table                                          | `RENAME employees TO employees_backup;`                   |
| **Rename Column**     | Renames a column in a table                              | `ALTER TABLE employees RENAME COLUMN salary TO monthly_salary;` |

#### Usage Example:
```sql
-- Rename a table
RENAME employees TO employees_backup;

-- Rename a column
ALTER TABLE employees RENAME COLUMN salary TO monthly_salary;
```

---

### Summary of Data Definition Operations:

| **Operation**    | **Description**                                      | **Syntax Example**                                        |
|------------------|------------------------------------------------------|-----------------------------------------------------------|
| **CREATE TABLE** | Defines a new table in the database                   | `CREATE TABLE employees (id INT PRIMARY KEY, name VARCHAR(50));` |
| **CREATE INDEX** | Creates an index on one or more columns               | `CREATE INDEX idx_employee_name ON employees (name);`      |
| **CREATE VIEW**  | Creates a virtual table (view) based on a query       | `CREATE VIEW employee_details AS SELECT id, name FROM employees;` |
| **ALTER TABLE**  | Modifies an existing table (add/drop/modify columns)  | `ALTER TABLE employees ADD hire_date DATE;`               |
| **DROP**         | Deletes a table, index, view, or other objects        | `DROP TABLE employees;`                                   |
| **TRUNCATE**     | Removes all rows from a table (cannot be rolled back) | `TRUNCATE TABLE employees;`                               |
| **RENAME**       | Renames a database object                             | `RENAME employees TO employees_backup;`                   |

---
