## Data Manipulation Language (DML)

### Overview
- **Definition**: DML is a subset of SQL used to manage data within database objects.
- **Purpose**: Insert, update, delete, and retrieve data from database tables.

### Key Commands

#### INSERT
- **Purpose**: Add new records to a table.
- **Syntax**:
  ```sql
  INSERT INTO table_name (column1, column2, ...)
  VALUES (value1, value2, ...);
  ```
- **Examples**:
  ```sql
  -- Insert a new record into the employees table
  INSERT INTO employees (id, name, position, salary)
  VALUES (1, 'John Doe', 'Manager', 75000.00);
  ```

#### UPDATE
- **Purpose**: Modify existing records in a table.
- **Syntax**:
  ```sql
  UPDATE table_name
  SET column1 = value1, column2 = value2, ...
  WHERE condition;
  ```
- **Examples**:
  ```sql
  -- Update the salary of an employee
  UPDATE employees
  SET salary = 80000.00
  WHERE id = 1;
  ```

#### DELETE
- **Purpose**: Remove records from a table.
- **Syntax**:
  ```sql
  DELETE FROM table_name
  WHERE condition;
  ```
- **Examples**:
  ```sql
  -- Delete an employee record
  DELETE FROM employees
  WHERE id = 1;
  ```

#### SELECT
- **Purpose**: Retrieve records from a table.
- **Syntax**:
  ```sql
  SELECT column1, column2, ...
  FROM table_name
  WHERE condition;
  ```
- **Examples**:
  ```sql
  -- Select all records from the employees table
  SELECT * FROM employees;

  -- Select specific columns from the employees table
  SELECT name, position FROM employees
  WHERE salary > 50000.00;
  ```

### Usage Considerations
- **Data Integrity**: Ensure data integrity by using appropriate constraints and conditions.
- **Performance**: Optimize queries for better performance, especially with large datasets.
- **Transactions**: Use transactions to ensure atomicity and consistency of data operations.

### Best Practices
- **Validation**: Validate data before inserting or updating records.
- **Indexing**: Use indexes to speed up data retrieval operations.
- **Normalization**: Normalize your database to reduce redundancy and improve data integrity.
- **Error Handling**: Implement error handling to manage exceptions during data operations.

### Comparison of DML Commands in Different SQL Implementations

| Feature       | MySQL Syntax Example | PostgreSQL Syntax Example | SQL Server Syntax Example | Oracle SQL Syntax Example |
|---------------|-----------------------|---------------------------|---------------------------|---------------------------|
| Insert Record | `INSERT INTO ...`     | `INSERT INTO ...`         | `INSERT INTO ...`         | `INSERT INTO ...`         |
| Update Record | `UPDATE ... SET ...`  | `UPDATE ... SET ...`      | `UPDATE ... SET ...`      | `UPDATE ... SET ...`      |
| Delete Record | `DELETE FROM ...`     | `DELETE FROM ...`         | `DELETE FROM ...`         | `DELETE FROM ...`         |
| Select Record | `SELECT ... FROM ...` | `SELECT ... FROM ...`     | `SELECT ... FROM ...`     | `SELECT ... FROM ...`     |

### Additional Details

#### Transactions
- **Definition**: A sequence of one or more SQL operations treated as a single unit.
- **Purpose**: Ensure data consistency and integrity.
- **Syntax**:
  ```sql
  -- Start a transaction
  BEGIN;

  -- Perform DML operations
  INSERT INTO employees (id, name, position, salary) VALUES (2, 'Jane Smith', 'Developer', 65000.00);

  -- Commit the transaction
  COMMIT;

  -- Rollback the transaction
  ROLLBACK;
  ```

#### Joins
- **Definition**: Combine records from two or more tables based on a related column.
- **Purpose**: Retrieve related data from multiple tables.
- **Types**:
  - **INNER JOIN**: Returns records that have matching values in both tables.
  - **LEFT JOIN (LEFT OUTER JOIN)**: Returns all records from the left table, and the matched records from the right table.
  - **RIGHT JOIN (RIGHT OUTER JOIN)**: Returns all records from the right table, and the matched records from the left table.
  - **FULL JOIN (FULL OUTER JOIN)**: Returns all records when there is a match in either left or right table.
- **Syntax**:
  ```sql
  SELECT columns
  FROM table1
  JOIN table2
  ON table1.column = table2.column;
  ```
- **Examples**:
  ```sql
  -- Inner join example
  SELECT employees.name, departments.department_name
  FROM employees
  JOIN departments
  ON employees.department_id = departments.id;

  -- Left join example
  SELECT employees.name, departments.department_name
  FROM employees
  LEFT JOIN departments
  ON employees.department_id = departments.id;

  -- Right join example
  SELECT employees.name, departments.department

```markdown
### Additional Details

#### Transactions
- **Definition**: A sequence of one or more SQL operations treated as a single unit.
- **Purpose**: Ensure data consistency and integrity.
- **Syntax**:
  ```sql
  -- Start a transaction
  BEGIN;

  -- Perform DML operations
  INSERT INTO employees (id, name, position, salary) VALUES (2, 'Jane Smith', 'Developer', 65000.00);

  -- Commit the transaction
  COMMIT;

  -- Rollback the transaction
  ROLLBACK;
  ```

#### Joins
- **Definition**: Combine records from two or more tables based on a related column.
- **Purpose**: Retrieve related data from multiple tables.
- **Syntax**:
  ```sql
  SELECT columns
  FROM table1
  JOIN table2
  ON table1.column = table2.column;
  ```
- **Examples**:
  ```sql
  -- Inner join example
  SELECT employees.name, departments.department_name
  FROM employees
  JOIN departments
  ON employees.department_id = departments.id;
  ```
