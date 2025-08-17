## PostgreSQL – Functions

### Overview

A **function** in PostgreSQL is a **stored block of code** that can be executed repeatedly to perform operations such as data processing, calculations, or returning values. Functions provide **reusability, modularity, and performance optimization** in database operations.

### Key Concepts

* **Purpose**

  * Encapsulate reusable logic.
  * Reduce repetitive code in queries or applications.
  * Enable procedural programming inside the database.
  * Can return single values, sets, or complex types.

* **Function Types**

  * **SQL Functions**

    * Written in standard SQL.
    * Can return scalar values or sets of rows.
  * **PL/pgSQL Functions**

    * Procedural language native to PostgreSQL.
    * Supports variables, loops, conditional statements, and exception handling.
  * **Other Procedural Languages**

    * PL/Python, PL/Perl, PL/Tcl, PL/Java, etc.
  * **Aggregate Functions**

    * Custom aggregation over sets of rows.
  * **Window Functions**

    * Operate over a set of rows related to the current row.

* **Return Types**

  * Scalar types (integer, text, boolean, etc.)
  * Composite types (row types or user-defined types)
  * Set of values (`SETOF type`)
  * Void (no return value)

* **Function Parameters**

  * **IN**: Input parameter (default)
  * **OUT**: Output parameter, used for returning multiple values
  * **INOUT**: Acts as both input and output
  * **VARIADIC**: Accepts variable number of arguments

* **Creation & Management**

  * `CREATE FUNCTION function_name (parameters) RETURNS return_type AS $$ ... $$ LANGUAGE language_name`
  * `ALTER FUNCTION` – Modify properties, ownership, or security.
  * `DROP FUNCTION` – Remove a function permanently.
  * `SECURITY DEFINER / SECURITY INVOKER` – Controls execution privileges.

* **Execution**

  * Invoked in SQL queries, triggers, or other functions.
  * Supports both **direct execution** and usage within expressions.

* **Advantages**

  * Encapsulation of business logic inside the database.
  * Improved performance for repetitive operations.
  * Enables complex computations, validations, and transformations.

* **Considerations**

  * Functions can impact transaction behavior; some languages support **side effects**, others must be immutable or stable.
  * Proper indexing and caching may enhance performance when functions are used in queries.

### Summary

Functions in PostgreSQL provide a **modular, reusable, and powerful mechanism** for implementing business logic:

* SQL, PL/pgSQL, and other language support
* Can return scalar, composite, or set values
* Used in queries, triggers, and procedural workflows
* Supports security, exception handling, and advanced parameterization

---
