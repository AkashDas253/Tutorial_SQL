## ANSI Data Definition Language (DDL)

DDL is a subset of SQL used to define, modify, and remove database structures such as tables, indexes, and views. It ensures the structure and schema of a database are created and managed.

### DDL Commands

| **Command**             | **Description**                                                                                         | **Example**                                                         |  
|-------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `CREATE`                | Defines a new database object such as a table, view, or index.                                           | `CREATE TABLE employees (id INT, name VARCHAR(50));`               |  
| `ALTER`                 | Modifies an existing database object, such as adding or removing columns or constraints.                | `ALTER TABLE employees ADD COLUMN age INT;`                         |  
| `DROP`                  | Deletes an existing database object, such as a table, view, or index.                                    | `DROP TABLE employees;`                                             |  
| `TRUNCATE`              | Deletes all rows from a table, but the table structure remains intact.                                   | `TRUNCATE TABLE employees;`                                         |  
| `RENAME`                | Renames a database object, such as a table or column.                                                    | `RENAME TABLE old_name TO new_name;`                                |  

---

### `CREATE` Command

The `CREATE` statement defines new database objects. It can be used to create tables, views, indexes, and databases.

#### 1. **CREATE TABLE**
Defines a new table and its columns, including their data types and constraints.

| **Clause**             | **Description**                                                                        | **Example**                                                      |  
|------------------------|----------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `CREATE TABLE`         | Defines the new table name.                                                            | `CREATE TABLE employees`                                         |  
| `column_name`          | Specifies the name of the column.                                                      | `id INT`                                                         |  
| `data_type`            | Defines the type of data that the column can store (e.g., `INT`, `VARCHAR`, `DATE`).    | `name VARCHAR(50)`                                                |  
| `CONSTRAINT`           | Adds constraints (e.g., `PRIMARY KEY`, `UNIQUE`, `NOT NULL`).                          | `CONSTRAINT pk_employee PRIMARY KEY(id)`                         |  

**Usage Example**:  
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    hire_date DATE
);
```

#### 2. **CREATE DATABASE**
Defines a new database.

| **Clause**             | **Description**                                                                        | **Example**                                                      |  
|------------------------|----------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `CREATE DATABASE`      | Defines the new database name.                                                         | `CREATE DATABASE company_db;`                                    |  

**Usage Example**:  
```sql
CREATE DATABASE company_db;
```

---

### `ALTER` Command

The `ALTER` statement modifies an existing database object.

#### 1. **ALTER TABLE**
Used to add, drop, or modify columns and constraints.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `ADD COLUMN`           | Adds a new column to an existing table.                                                                  | `ALTER TABLE employees ADD COLUMN age INT;`                      |  
| `DROP COLUMN`          | Removes an existing column from the table.                                                                | `ALTER TABLE employees DROP COLUMN age;`                         |  
| `MODIFY COLUMN`        | Changes the data type or constraints of an existing column.                                              | `ALTER TABLE employees MODIFY COLUMN name VARCHAR(100);`         |  
| `ADD CONSTRAINT`       | Adds a new constraint to an existing table.                                                              | `ALTER TABLE employees ADD CONSTRAINT fk_department FOREIGN KEY(department_id) REFERENCES departments(id);`  |  

**Usage Example**:  
```sql
ALTER TABLE employees ADD COLUMN department_id INT;
```

#### 2. **ALTER DATABASE**
Modifies properties of an existing database.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `ALTER DATABASE`       | Modifies the properties of an existing database (e.g., rename).                                           | `ALTER DATABASE company_db MODIFY NAME company_database;`       |  

---

### `DROP` Command

The `DROP` statement is used to remove an existing database object.

#### 1. **DROP TABLE**
Deletes a table and all its data from the database.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `DROP TABLE`           | Deletes the table and all its data permanently.                                                          | `DROP TABLE employees;`                                          |  

#### 2. **DROP DATABASE**
Deletes a database and all its objects permanently.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `DROP DATABASE`        | Deletes the specified database.                                                                          | `DROP DATABASE company_db;`                                      |  

#### 3. **DROP INDEX**
Deletes an index from the database.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `DROP INDEX`           | Deletes an index from the table.                                                                         | `DROP INDEX idx_employee_name;`                                  |  

---

### `TRUNCATE` Command

The `TRUNCATE` statement removes all data from a table without deleting the table itself.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `TRUNCATE TABLE`       | Deletes all rows in a table, but retains the structure for future use.                                   | `TRUNCATE TABLE employees;`                                      |  

**Usage Example**:  
```sql
TRUNCATE TABLE employees;
```

---

### `RENAME` Command

The `RENAME` statement changes the name of a database object, such as a table or column.

#### 1. **RENAME TABLE**
Changes the name of a table.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `RENAME TABLE`         | Renames a table from its old name to a new one.                                                          | `RENAME TABLE old_employees TO new_employees;`                   |  

#### 2. **RENAME COLUMN**
Changes the name of a column.

| **Clause**             | **Description**                                                                                         | **Example**                                                      |  
|------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|  
| `RENAME COLUMN`        | Renames an existing column in a table.                                                                   | `RENAME COLUMN name TO full_name;`                               |  

---

### Conclusion  

DDL commands are essential for defining and modifying the structure of a database. They help manage the database schema, making it possible to create, alter, and delete tables, indexes, views, and databases. These commands are fundamental to establishing the foundation of any relational database.
