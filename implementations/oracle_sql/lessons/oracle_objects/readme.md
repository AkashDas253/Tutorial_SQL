## Database Objects in Oracle SQL

### 1. **Tables**
Tables are the basic units of storage in a database. They consist of rows and columns, where each row represents a record and each column represents a field.

| **Property**       | **Description**                                       | **Usage Example**                                         |
|--------------------|-------------------------------------------------------|-----------------------------------------------------------|
| **Structure**      | Defined by columns (fields) and rows (records)         | `CREATE TABLE employees (id NUMBER, name VARCHAR2(50));`  |
| **Primary Key**    | Uniquely identifies each record in the table           | `PRIMARY KEY (id)`                                         |
| **Foreign Key**    | Defines a relationship between tables                  | `FOREIGN KEY (department_id) REFERENCES departments(id)`  |
| **Constraints**    | Rules that ensure data integrity (e.g., `NOT NULL`)    | `CHECK (salary > 0)`                                       |

#### Usage Example:
```sql
CREATE TABLE employees (
    id NUMBER PRIMARY KEY,
    name VARCHAR2(50),
    department_id NUMBER,
    salary NUMBER CHECK (salary > 0)
);
```

### 2. **Views**
A view is a virtual table that provides a simplified, aggregated, or customized view of data from one or more tables. It does not store data physically but runs a query to generate the result.

| **Property**       | **Description**                                      | **Usage Example**                                         |
|--------------------|------------------------------------------------------|-----------------------------------------------------------|
| **Virtual Table**  | A view behaves like a table but does not store data  | `CREATE VIEW employee_view AS SELECT * FROM employees;`   |
| **Read-Only**      | Some views are read-only (cannot be modified)        | `SELECT * FROM employee_view;`                            |
| **Updatable**      | Views that allow updates (with some restrictions)    | `CREATE VIEW employee_salary_view AS SELECT id, salary FROM employees;` |

#### Usage Example:
```sql
CREATE VIEW employee_view AS
SELECT id, name, salary
FROM employees
WHERE salary > 5000;
```

### 3. **Indexes**
Indexes are database objects that speed up the retrieval of rows from a table by creating pointers to the data. Indexes are created on one or more columns of a table.

| **Property**       | **Description**                                        | **Usage Example**                                          |
|--------------------|--------------------------------------------------------|------------------------------------------------------------|
| **Unique Index**   | Ensures that the indexed column(s) contain unique values | `CREATE UNIQUE INDEX idx_employee_id ON employees(id);`    |
| **Non-Unique Index** | Improves query performance, but does not enforce uniqueness | `CREATE INDEX idx_employee_salary ON employees(salary);`  |
| **Composite Index** | An index on multiple columns                          | `CREATE INDEX idx_composite ON employees(id, salary);`     |

#### Usage Example:
```sql
CREATE INDEX idx_employee_salary ON employees(salary);
```

### 4. **Sequences**
A sequence is a database object that generates a sequence of unique numbers, typically used for generating primary key values.

| **Property**       | **Description**                                       | **Usage Example**                                         |
|--------------------|-------------------------------------------------------|-----------------------------------------------------------|
| **Increment**      | Specifies the value by which the sequence is incremented | `INCREMENT BY 1`                                           |
| **Start Value**    | Specifies the starting value for the sequence          | `START WITH 1`                                             |
| **Cycle**          | Determines whether the sequence can start over after reaching its maximum value | `CYCLE`                                                     |

#### Usage Example:
```sql
CREATE SEQUENCE emp_id_seq
START WITH 1
INCREMENT BY 1
CYCLE;
```

#### Usage Example to get the next value:
```sql
SELECT emp_id_seq.NEXTVAL FROM dual;
```

### 5. **Synonyms**
A synonym is an alias for a database object (like a table, view, or sequence). It simplifies queries by allowing users to refer to objects by a different name.

| **Property**       | **Description**                                      | **Usage Example**                                         |
|--------------------|------------------------------------------------------|-----------------------------------------------------------|
| **Public Synonym** | Can be accessed by all users in the database          | `CREATE PUBLIC SYNONYM emp FOR employees;`                |
| **Private Synonym** | Only accessible by the schema owner or explicitly granted users | `CREATE SYNONYM emp FOR schema_name.employees;`          |

#### Usage Example:
```sql
CREATE SYNONYM emp FOR employees;
```

### 6. **Triggers**
A trigger is a stored procedure that is automatically executed in response to certain events (e.g., INSERT, UPDATE, DELETE) on a table or view.

| **Property**       | **Description**                                        | **Usage Example**                                         |
|--------------------|--------------------------------------------------------|-----------------------------------------------------------|
| **BEFORE Trigger** | Executes before an operation on the table              | `CREATE TRIGGER before_insert_emp BEFORE INSERT ON employees FOR EACH ROW BEGIN ... END;` |
| **AFTER Trigger**  | Executes after an operation on the table               | `CREATE TRIGGER after_update_emp AFTER UPDATE ON employees FOR EACH ROW BEGIN ... END;` |

#### Usage Example:
```sql
CREATE TRIGGER emp_salary_check
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
   IF :NEW.salary < 1000 THEN
      RAISE_APPLICATION_ERROR(-20001, 'Salary cannot be less than 1000');
   END IF;
END;
```

### 7. **Procedures**
A procedure is a set of SQL statements grouped together to perform a specific task. It can accept parameters and return values.

| **Property**       | **Description**                                        | **Usage Example**                                         |
|--------------------|--------------------------------------------------------|-----------------------------------------------------------|
| **Stored Procedure** | A procedure stored in the database to be executed later | `CREATE PROCEDURE update_salary (emp_id NUMBER, new_salary NUMBER) AS BEGIN UPDATE employees SET salary = new_salary WHERE id = emp_id; END;` |
| **Parameters**     | Procedures can accept input parameters and return output | `IN` (input), `OUT` (output), or `IN OUT` (input and output) |

#### Usage Example:
```sql
CREATE PROCEDURE update_salary (emp_id NUMBER, new_salary NUMBER) AS
BEGIN
   UPDATE employees
   SET salary = new_salary
   WHERE id = emp_id;
END;
```

### 8. **Functions**
A function is similar to a procedure but must return a value. Functions can be used within SQL queries.

| **Property**       | **Description**                                        | **Usage Example**                                         |
|--------------------|--------------------------------------------------------|-----------------------------------------------------------|
| **Return Value**   | A function must return a value of a specific data type  | `CREATE FUNCTION get_bonus (emp_id NUMBER) RETURN NUMBER AS BEGIN SELECT salary * 0.1 INTO bonus FROM employees WHERE id = emp_id; RETURN bonus; END;` |
| **Use in SQL**     | Functions can be used directly in SQL statements       | `SELECT get_bonus(101) FROM dual;`                        |

#### Usage Example:
```sql
CREATE FUNCTION get_bonus (emp_id NUMBER) RETURN NUMBER AS
   bonus NUMBER;
BEGIN
   SELECT salary * 0.1 INTO bonus
   FROM employees
   WHERE id = emp_id;
   RETURN bonus;
END;
```

### 9. **Clusters**
A cluster is a group of tables that share a common column and store their data together, improving performance when queried together.

| **Property**       | **Description**                                        | **Usage Example**                                         |
|--------------------|--------------------------------------------------------|-----------------------------------------------------------|
| **Clustered Tables** | Tables in the same cluster share storage space         | `CREATE CLUSTER emp_cluster (department_id NUMBER) SIZE 512;` |
| **Shared Data**     | Data from multiple tables can be stored together for optimization | `CREATE TABLE employees (id NUMBER, department_id NUMBER) CLUSTER emp_cluster(department_id);` |

#### Usage Example:
```sql
CREATE CLUSTER emp_cluster (department_id NUMBER) SIZE 512;
```

### 10. **Schemas**
A schema is a collection of database objects (tables, views, indexes, etc.) that belong to a specific user.

| **Property**       | **Description**                                        | **Usage Example**                                         |
|--------------------|--------------------------------------------------------|-----------------------------------------------------------|
| **Owned by User**  | Schema objects belong to the user who owns the schema  | `CREATE SCHEMA hr AUTHORIZATION hr_user;`                 |
| **Contains Objects** | A schema can contain multiple objects such as tables and views | `CREATE TABLE hr.employees (...);`                        |

#### Usage Example:
```sql
CREATE SCHEMA hr AUTHORIZATION hr_user;
```

---

### Notes:
- **Data Integrity**: Many of these objects, such as constraints, triggers, and views, are essential for maintaining data integrity and consistency in a database.
- **Storage Efficiency**: Objects like indexes, clusters, and views help improve query performance and storage management in large databases.
