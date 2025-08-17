## PostgreSQL – Data Definition (DDL)

### Overview

**Data Definition Language (DDL)** in PostgreSQL consists of SQL commands used to **define, modify, and manage database objects** such as tables, schemas, views, indexes, and sequences. DDL commands **affect the structure** of the database rather than its content.

### Key Concepts

* **Purpose**

  * Create and maintain database objects.
  * Define **structure, constraints, and relationships**.
  * Enable database schema versioning and management.

* **Main DDL Commands**

  * **CREATE**

    * Creates database objects: tables, schemas, views, indexes, sequences, functions, triggers, etc.
    * Examples:

      ```sql
      CREATE TABLE employees (
        id serial PRIMARY KEY,
        name text NOT NULL,
        salary numeric
      );

      CREATE SCHEMA hr;
      CREATE INDEX idx_salary ON employees(salary);
      ```
    * Supports **IF NOT EXISTS** to avoid errors if object exists.

  * **ALTER**

    * Modifies existing database objects.
    * Examples:

      ```sql
      ALTER TABLE employees ADD COLUMN department text;
      ALTER TABLE employees ALTER COLUMN salary SET NOT NULL;
      ALTER INDEX idx_salary RENAME TO idx_emp_salary;
      ```
    * Can rename objects, modify columns, add/drop constraints, or change object ownership.

  * **DROP**

    * Removes database objects permanently.
    * Examples:

      ```sql
      DROP TABLE employees;
      DROP INDEX idx_emp_salary;
      DROP SCHEMA hr CASCADE;
      ```
    * **CASCADE** removes dependent objects automatically.
    * **RESTRICT** prevents dropping if dependencies exist.

  * **TRUNCATE**

    * Removes all rows from a table quickly without affecting its structure.
    * Supports `CASCADE` to truncate dependent tables.
    * Faster than `DELETE` for large tables as it avoids row-by-row operations.

* **Object Types Managed by DDL**

  * **Databases**: CREATE DATABASE, DROP DATABASE
  * **Schemas**: CREATE SCHEMA, DROP SCHEMA, ALTER SCHEMA
  * **Tables**: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE
  * **Views & Materialized Views**: CREATE VIEW, CREATE MATERIALIZED VIEW, DROP, REFRESH
  * **Indexes**: CREATE INDEX, ALTER INDEX, DROP INDEX
  * **Sequences**: CREATE SEQUENCE, ALTER SEQUENCE, DROP SEQUENCE
  * **Functions / Procedures**: CREATE FUNCTION/PROCEDURE, ALTER, DROP
  * **Triggers**: CREATE TRIGGER, ALTER TRIGGER, DROP TRIGGER
  * **Extensions**: CREATE EXTENSION, DROP EXTENSION

* **Transactions**

  * DDL commands are **transactional** in PostgreSQL.
  * `BEGIN` … `COMMIT` / `ROLLBACK` can include DDL, unlike some other RDBMS.

* **Considerations**

  * Dropping or altering objects may **affect dependent objects**.
  * Proper permissions are required: usually **superuser or owner**.
  * Use **IF EXISTS / IF NOT EXISTS** to prevent errors in scripts.

### Summary

Data Definition (DDL) in PostgreSQL allows **managing the structure of the database**:

* CREATE, ALTER, DROP, TRUNCATE objects
* Manages tables, schemas, views, indexes, sequences, functions, triggers, and extensions
* Transactional support ensures **atomic structural changes**
* Essential for **schema design, maintenance, and version control**

---
