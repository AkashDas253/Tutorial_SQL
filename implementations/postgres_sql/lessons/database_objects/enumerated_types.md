## PostgreSQL – Enumerated Types (ENUM)

### Overview

An **enumerated type (ENUM)** in PostgreSQL is a **data type consisting of a static, ordered set of values**. ENUMs provide **readability, consistency, and constraint enforcement** for columns that should only hold a limited set of predefined values.

### Key Concepts

* **Purpose**

  * Restrict a column to a **specific set of valid values**.
  * Improve **data integrity and clarity** for categorical data.
  * Provide a more **efficient and semantically meaningful alternative** to text or numeric codes.

* **Creation**

  * `CREATE TYPE enum_name AS ENUM ('value1', 'value2', 'value3', ...);`
  * Example:

    ```sql
    CREATE TYPE mood AS ENUM ('happy', 'sad', 'neutral');
    ```

* **Usage**

  * Columns can use the ENUM type:

    ```sql
    CREATE TABLE employees (
      id serial PRIMARY KEY,
      name text NOT NULL,
      mood mood
    );
    ```
  * Only the defined ENUM values can be inserted into the column.

* **Modifying ENUM Types**

  * `ALTER TYPE enum_name ADD VALUE 'new_value' [ BEFORE | AFTER existing_value ]`
  * Values cannot be removed or reordered in earlier PostgreSQL versions (some newer versions allow limited modifications).

* **Advantages**

  * Ensures **data consistency** by restricting values.
  * Improves **query readability** and understanding.
  * ENUM values are stored as **integers internally**, saving storage space compared to text.

* **Considerations**

  * ENUMs are **static**; adding new values requires `ALTER TYPE`.
  * Not suitable for frequently changing sets of values.
  * Comparison follows **declaration order**, not alphabetical order.

* **Best Practices**

  * Use ENUMs for **stable, finite sets of options** (e.g., status flags, categories).
  * For dynamic sets, consider a **lookup table with foreign key** instead.

### Summary

Enumerated types (ENUMs) in PostgreSQL provide a **controlled set of categorical values**:

* Improve data integrity and readability
* Efficiently store and compare predefined values
* Suitable for static, finite sets where order matters

---
