## PostgreSQL – Constraints

### Overview

A **constraint** in PostgreSQL is a **rule applied to a table or column** to enforce **data integrity and correctness**. Constraints ensure that only valid data can be inserted or updated in the database.

### Key Concepts

* **Purpose**

  * Enforce **business rules** at the database level.
  * Prevent invalid or inconsistent data.
  * Reduce errors and maintain referential integrity.

* **Types of Constraints**

  * **NOT NULL**

    * Ensures a column cannot contain NULL values.
    * Applied at column level.
  * **UNIQUE**

    * Ensures all values in a column or combination of columns are distinct.
    * Can be applied at column or table level.
  * **PRIMARY KEY**

    * Uniquely identifies each row in a table.
    * Combination of **UNIQUE + NOT NULL**.
    * Only one primary key allowed per table.
  * **FOREIGN KEY**

    * Enforces referential integrity between two tables.
    * References a **primary key or unique key** in another table.
    * Can specify `ON DELETE` / `ON UPDATE` actions: `CASCADE`, `SET NULL`, `RESTRICT`, `NO ACTION`.
  * **CHECK**

    * Ensures column values satisfy a specific **condition or expression**.
    * Can reference multiple columns.
  * **EXCLUSION CONSTRAINT**

    * Ensures **no two rows conflict** on specified operators.
    * Often used for ranges or spatial data.

* **Constraint Creation**

  * Column-level:

    ```sql
    CREATE TABLE employees (
      id serial PRIMARY KEY,
      age integer NOT NULL CHECK (age > 0)
    );
    ```
  * Table-level:

    ```sql
    CREATE TABLE orders (
      order_id serial,
      product_id integer,
      quantity integer,
      CONSTRAINT unique_order UNIQUE (order_id, product_id)
    );
    ```

* **Constraint Management**

  * `ALTER TABLE ... ADD CONSTRAINT` – Add a new constraint.
  * `ALTER TABLE ... DROP CONSTRAINT` – Remove a constraint.
  * `DEFERRABLE` / `INITIALLY DEFERRED` – Delay constraint checking until transaction commit.
  * Constraints are enforced **immediately by default**.

* **Advantages**

  * Ensures **data accuracy and consistency** automatically.
  * Reduces the need for application-level validation.
  * Supports **referential integrity and relational modeling**.

* **Considerations**

  * Constraints can affect **insert/update performance**.
  * Complex `CHECK` or `EXCLUSION` constraints may slow down operations.
  * Proper indexing is recommended for **PRIMARY KEY, UNIQUE, and FOREIGN KEY** constraints.

### Summary

Constraints in PostgreSQL are **rules that enforce data integrity**:

* NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, EXCLUSION
* Applied at column or table level
* Can be immediate or deferrable
* Essential for maintaining **correct and reliable data**

---
