## Data Manipulation Language (DML)

### Overview
- **Definition**: DML is a subset of SQL used to manage data within database objects.
- **Purpose**: Perform operations such as inserting, updating, deleting, and calling stored procedures.

### Key Commands

#### INSERT
- **Purpose**: Add new rows to a table.
- **Syntax**:
  ```sql
  INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
  ```
  - `table_name`: The name of the table where the data will be inserted.
  - `column1, column2, ...`: The columns in the table where the data will be inserted.
  - `value1, value2, ...`: The values to be inserted into the specified columns.
- **Example**:
  ```sql
  -- Insert a new record into the employees table
  INSERT INTO employees (name, position) VALUES ('John Doe', 'Developer');
  ```

#### UPDATE
- **Purpose**: Modify existing rows in a table.
- **Syntax**:
  ```sql
  UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
  ```
  - `table_name`: The name of the table to update.
  - `column1 = value1, column2 = value2, ...`: The columns and their new values.
  - `condition`: The condition to specify which rows to update.
- **Example**:
  ```sql
  -- Update the position of an employee
  UPDATE employees SET position = 'Senior Developer' WHERE name = 'John Doe';
  ```

#### DELETE
- **Purpose**: Remove rows from a table.
- **Syntax**:
  ```sql
  DELETE FROM table_name WHERE condition;
  ```
  - `table_name`: The name of the table to delete rows from.
  - `condition`: The condition to specify which rows to delete.
- **Example**:
  ```sql
  -- Delete an employee record
  DELETE FROM employees WHERE name = 'John Doe';
  ```

#### CALL
- **Purpose**: Execute a stored procedure.
- **Syntax**:
  ```sql
  CALL procedure_name(parameters);
  ```
  - `procedure_name`: The name of the stored procedure to call.
  - `parameters`: The parameters to pass to the stored procedure.
- **Example**:
  ```sql
  -- Call a stored procedure to update employee salaries
  CALL update_employee_salaries();
  ```

#### EXPLAIN
- **Purpose**: Display the execution plan for a query.
- **Syntax**:
  ```sql
  EXPLAIN query;
  ```
  - `query`: The query to explain.
- **Example**:
  ```sql
  -- Explain the execution plan for a select query
  EXPLAIN SELECT * FROM employees WHERE position = 'Developer';
  ```

#### LOCK
- **Purpose**:

 Control

 concurrent access to database objects.
- **Syntax**:
  ```sql
  LOCK TABLE table_name IN {SHARE | EXCLUSIVE} MODE;
  ```
  - `table_name`: The name of the table to lock.
  - `{SHARE | EXCLUSIVE}`: The mode of the lock.
- **Example**:
  ```sql
  -- Lock the employees table in exclusive mode
  LOCK TABLE employees IN EXCLUSIVE MODE;
  ```


### Usage Considerations
- **Data Integrity**: Ensure that DML operations maintain the integrity of the data.
- **Concurrency Control**: Use locks and transactions to manage concurrent access to data.
- **Performance**: Optimize DML operations to improve performance and reduce resource usage.

### Best Practices
- **Use Transactions**: Group related DML operations into transactions to ensure atomicity.
- **Handle Exceptions**: Implement error handling to manage exceptions during DML operations.
- **Optimize Queries**: Use indexes and optimize queries to improve performance.
- **Minimize Locks**: Keep locks short to reduce contention and improve concurrency.

### Comparison of DML Commands in Different SQL Implementations

| Feature            | MySQL Syntax Example | PostgreSQL Syntax Example | SQL Server Syntax Example | Oracle SQL Syntax Example |
|--------------------|-----------------------|---------------------------|---------------------------|---------------------------|
| Insert             | `INSERT INTO ...;`    | `INSERT INTO ...;`        | `INSERT INTO ...;`        | `INSERT INTO ...;`        |
| Update             | `UPDATE ...;`         | `UPDATE ...;`             | `UPDATE ...;`             | `UPDATE ...;`             |
| Delete             | `DELETE FROM ...;`    | `DELETE FROM ...;`        | `DELETE FROM ...;`        | `DELETE FROM ...;`        |
| Call               | `CALL ...;`           | `CALL ...;`               | `EXEC ...;`               | `CALL ...;`               |
| Explain            | `EXPLAIN ...;`        | `EXPLAIN ...;`            | `EXPLAIN ...;`            | `EXPLAIN ...;`            |
| Lock               | `LOCK TABLE ...;`     | `LOCK TABLE ...;`         | `LOCK TABLE ...;`         | `LOCK TABLE ...;`         |

### Additional Details

#### Handling NULL Values
- **Definition**: NULL represents missing or unknown data.
- **Syntax**:
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, NULL);
  ```
- **Example**:
  ```sql
  -- Insert a record with a NULL value
  INSERT INTO employees (name, position) VALUES ('Jane Doe', NULL);
  ```

#### Using Subqueries
- **Definition**: A subquery is a query nested inside another query.
- **Syntax**:
  ```sql
  INSERT INTO table_name (column1, column2) SELECT value1, value2 FROM another_table WHERE condition;
  ```
- **Example**:
  ```sql
  -- Insert records from another table
  INSERT INTO employees (name, position) SELECT name, position FROM new_employees WHERE start_date > '2023-01-01';
  ```

#### Conditional Updates
- **Definition**: Update rows based on specific conditions.
- **Syntax**:
  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```
- **Example**:
  ```sql
  -- Update the position of employees based on their current position
  UPDATE employees SET position = 'Lead Developer' WHERE position = 'Senior Developer';
  ```

#### Deleting with Subqueries
- **Definition**: Use subqueries to specify which rows to delete.
- **Syntax**:
  ```sql
  DELETE FROM table_name WHERE column IN (SELECT column FROM another_table WHERE condition);
  ```
- **Example**:
  ```sql
  -- Delete employees who are not in the active projects list
  DELETE FROM employees WHERE id NOT IN (SELECT employee_id FROM active_projects);
  ```

#### Calling Stored Procedures with Parameters
- **Definition**: Execute stored procedures with input parameters.
- **Syntax**:
  ```sql
  CALL procedure_name(parameter1, parameter2);
  ```
- **Example**:
  ```sql
  -- Call a stored procedure to update an employee's salary
  CALL update_salary('John Doe', 75000);
  ```

#### Locking Specific Rows
- **Definition**: Lock specific rows to control concurrent access.
- **Syntax**:
  ```sql
  SELECT * FROM table_name WHERE condition FOR UPDATE;
  ```
- **Example**:
  ```sql
  -- Lock rows of employees who are developers
  SELECT * FROM employees WHERE position = 'Developer' FOR UPDATE;
  ```
