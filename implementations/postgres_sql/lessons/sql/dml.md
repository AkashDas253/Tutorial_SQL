## PostgreSQL – Data Manipulation (DML)

### Overview

**Data Manipulation Language (DML)** in PostgreSQL consists of SQL commands used to **insert, update, delete, and retrieve data** in database tables. DML operations work within the context of **transactions** and enforce constraints and integrity rules.

### Key Concepts

* **Purpose**

  * Modify and retrieve table data.
  * Support transactional operations with rollback and commit.
  * Enable controlled interaction with relational data.

* **Main DML Commands**

  * **INSERT**

    * Adds new rows to a table.
    * Syntax:

      ```sql
      INSERT INTO table_name (column1, column2, ...)
      VALUES (value1, value2, ...);
      ```
    * Supports multiple rows and `DEFAULT` values.
    * Can use `RETURNING` to get inserted values.
  * **UPDATE**

    * Modifies existing rows.
    * Syntax:

      ```sql
      UPDATE table_name
      SET column1 = value1, column2 = value2
      WHERE condition;
      ```
    * Can update multiple rows based on conditions.
    * Supports expressions and subqueries.
  * **DELETE**

    * Removes rows from a table.
    * Syntax:

      ```sql
      DELETE FROM table_name
      WHERE condition;
      ```
    * Without `WHERE`, deletes all rows.
    * Can use `RETURNING` to fetch deleted rows.
  * **SELECT**

    * Retrieves data from one or more tables.
    * Syntax:

      ```sql
      SELECT column1, column2
      FROM table_name
      WHERE condition
      ORDER BY column
      LIMIT n;
      ```
    * Supports joins, aggregations, filtering, ordering, and grouping.

* **Advanced DML Features**

  * **UPSERT / ON CONFLICT**

    * Combines INSERT and UPDATE to handle conflicts.

      ```sql
      INSERT INTO table_name (id, value)
      VALUES (1, 'x')
      ON CONFLICT (id)
      DO UPDATE SET value = EXCLUDED.value;
      ```
  * **RETURNING Clause**

    * Fetches values from affected rows (INSERT, UPDATE, DELETE).
  * **CTEs (Common Table Expressions)**

    * Use `WITH` to structure complex DML operations.
  * **Subqueries**

    * Nested queries for conditional updates or inserts.

* **Transactions**

  * DML statements are **transactional** by default.
  * Commands: `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`.
  * Ensures **atomicity, consistency, isolation, and durability (ACID)**.

* **Considerations**

  * Triggers, constraints, and rules may affect DML operations.
  * Performance can be impacted by indexes, foreign keys, and large datasets.
  * Batch operations should consider **locking and concurrency**.

### Summary

Data Manipulation (DML) in PostgreSQL provides **essential tools to interact with table data**:

* INSERT, UPDATE, DELETE, and SELECT
* Supports transactions, CTEs, subqueries, and UPSERT
* Works with constraints, triggers, and indexes to maintain data integrity
* Critical for implementing **CRUD (Create, Read, Update, Delete) operations**

---
