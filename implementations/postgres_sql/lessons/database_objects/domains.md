## PostgreSQL – Domains

### Overview

A **domain** in PostgreSQL is a **user-defined data type** that encapsulates a **base type with optional constraints**. Domains provide **reusability, consistency, and improved data integrity** across multiple tables.

### Key Concepts

* **Purpose**

  * Enforce consistent data types and constraints across multiple columns or tables.
  * Simplify schema design by reusing common rules.
  * Centralize validation logic to reduce errors.

* **Domain Creation**

  * `CREATE DOMAIN domain_name AS base_type [ DEFAULT default_value ] [ CONSTRAINT constraint_name constraint ]`
  * Example:

    ```sql
    CREATE DOMAIN positive_int AS integer
    CHECK (VALUE > 0);
    ```

* **Base Types**

  * Domains are based on existing PostgreSQL types such as:

    * Numeric: `integer`, `bigint`, `numeric`, `decimal`
    * Character: `text`, `varchar`, `char`
    * Date/Time: `date`, `timestamp`, `time`
    * Boolean: `boolean`
    * Custom or user-defined types

* **Constraints**

  * Domains can include constraints similar to table columns:

    * **NOT NULL**
    * **CHECK** (custom validation rules)
    * **DEFAULT** values
  * Constraints are automatically applied to any column using the domain.

* **Usage**

  * Use domain as the data type for table columns:

    ```sql
    CREATE TABLE employees (
      emp_id serial PRIMARY KEY,
      age positive_int,
      salary numeric(10,2)
    );
    ```
  * Columns using the domain inherit its constraints automatically.

* **Advantages**

  * Reusability: Apply the same rules across multiple tables.
  * Centralized maintenance: Changing a domain updates all dependent columns.
  * Enhanced data integrity: Reduces repetition and ensures consistency.

* **Management**

  * `ALTER DOMAIN` – Modify default value or add/drop constraints.
  * `DROP DOMAIN` – Remove the domain (must not be in use by any column).

* **Considerations**

  * Cannot directly store values; only used as a column type.
  * Constraints in domains are applied **before column-level constraints**.
  * Useful for enforcing **business rules consistently**.

### Summary

Domains in PostgreSQL are **user-defined types with constraints**:

* Based on existing types but enforce reusable rules
* Simplify schema design and maintain data integrity
* Centralize validation logic for consistent application across tables

---
