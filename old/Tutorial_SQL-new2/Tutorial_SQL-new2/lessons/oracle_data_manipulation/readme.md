## Data Manipulation in Oracle SQL

### 1. **INSERT**
The `INSERT` statement is used to add new records to a table.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic Insert**      | Inserts a new row into a table                           | `INSERT INTO employees (id, name, department_id) VALUES (1, 'John Doe', 10);` |
| **Insert with Select**| Inserts data from another table or query                 | `INSERT INTO employees (id, name) SELECT id, name FROM temp_employees;` |
| **Insert Default Values**| Insert a new row with default column values (if defined) | `INSERT INTO employees (id, name) VALUES (emp_seq.NEXTVAL, 'Jane Doe');` |

#### Usage Example:
```sql
-- Insert a single record
INSERT INTO employees (id, name, department_id) VALUES (1, 'John Doe', 10);

-- Insert multiple records
INSERT ALL
    INTO employees (id, name, department_id) VALUES (2, 'Jane Doe', 20)
    INTO employees (id, name, department_id) VALUES (3, 'Mark Smith', 30)
SELECT * FROM dual;
```

### 2. **UPDATE**
The `UPDATE` statement is used to modify existing records in a table.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic Update**      | Updates specified columns for existing rows              | `UPDATE employees SET salary = 5000 WHERE id = 1;`         |
| **Conditional Update**| Updates records based on conditions                       | `UPDATE employees SET salary = salary + 500 WHERE department_id = 10;` |
| **Multiple Columns**  | Updates multiple columns at once                         | `UPDATE employees SET salary = 6000, name = 'John Smith' WHERE id = 1;` |

#### Usage Example:
```sql
-- Update a single column
UPDATE employees SET salary = 5500 WHERE id = 1;

-- Update multiple columns
UPDATE employees SET salary = 6000, name = 'Jane Smith' WHERE id = 2;
```

### 3. **DELETE**
The `DELETE` statement is used to remove one or more records from a table.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic Delete**      | Deletes specific rows from a table                       | `DELETE FROM employees WHERE id = 1;`                      |
| **Delete All Records**| Deletes all records from a table                         | `DELETE FROM employees;`                                  |
| **Conditional Delete**| Deletes records based on conditions                       | `DELETE FROM employees WHERE salary < 3000;`              |

#### Usage Example:
```sql
-- Delete specific record
DELETE FROM employees WHERE id = 1;

-- Delete all records from the table (without removing the table structure)
DELETE FROM employees;
```

### 4. **MERGE (Upsert)**
The `MERGE` statement is used to insert, update, or delete records in a target table based on a source table or query, often used for upsert operations (inserting or updating based on condition).

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Basic Merge**       | Combines `INSERT`, `UPDATE`, and `DELETE` in one statement | `MERGE INTO employees e USING temp_employees t ON (e.id = t.id) WHEN MATCHED THEN UPDATE SET e.salary = t.salary WHEN NOT MATCHED THEN INSERT (id, name, salary) VALUES (t.id, t.name, t.salary);` |

#### Usage Example:
```sql
MERGE INTO employees e
USING temp_employees t
ON (e.id = t.id)
WHEN MATCHED THEN
    UPDATE SET e.salary = t.salary
WHEN NOT MATCHED THEN
    INSERT (id, name, salary) VALUES (t.id, t.name, t.salary);
```

### 5. **TRUNCATE**
The `TRUNCATE` statement is used to remove all rows from a table, but it does not remove the table structure. It is faster than `DELETE` because it does not log individual row deletions.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Fast Delete**       | Removes all rows from the table                          | `TRUNCATE TABLE employees;`                               |
| **Cannot Rollback**   | Data cannot be rolled back after truncation               | `TRUNCATE TABLE employees;`                               |

#### Usage Example:
```sql
-- Truncate the table (removes all records but not the table)
TRUNCATE TABLE employees;
```

### 6. **SELECT INTO**
The `SELECT INTO` statement is used to create a new table by selecting data from an existing table or query. It is similar to a `CREATE TABLE` combined with an `INSERT`.

| **Property**         | **Description**                                          | **Usage Example**                                         |
|----------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Create New Table**  | Creates a new table based on the result of a select query | `SELECT * INTO new_employees FROM employees WHERE salary > 5000;` |
| **Insert Data**       | Creates a new table with data from another table         | `SELECT id, name, salary INTO high_salary_employees FROM employees WHERE salary > 7000;` |

#### Usage Example:
```sql
SELECT id, name, salary
INTO high_salary_employees
FROM employees
WHERE salary > 7000;
```

---

### Summary of Data Manipulation Operations:

| **Operation** | **Description**                                           | **Syntax Example**                                        |
|---------------|-----------------------------------------------------------|-----------------------------------------------------------|
| **INSERT**    | Adds new records to a table                                | `INSERT INTO employees (id, name) VALUES (1, 'John Doe');` |
| **UPDATE**    | Modifies existing records                                  | `UPDATE employees SET salary = 5500 WHERE id = 1;`         |
| **DELETE**    | Removes records from a table                               | `DELETE FROM employees WHERE id = 1;`                      |
| **MERGE**     | Combines insert, update, and delete operations             | `MERGE INTO employees e USING temp_employees t ON (e.id = t.id) ...` |
| **TRUNCATE**  | Removes all rows from a table (faster than DELETE)         | `TRUNCATE TABLE employees;`                               |
| **SELECT INTO**| Creates a new table and inserts data from a query result   | `SELECT id, name INTO new_employees FROM employees;`      |

---
