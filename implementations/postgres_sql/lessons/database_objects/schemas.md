## PostgreSQL – Schemas

### Overview

A **schema** in PostgreSQL is a **logical namespace** within a database that organizes and groups database objects such as tables, views, indexes, functions, and sequences. Schemas help **avoid name collisions**, improve **organization**, and control **access privileges**.

### Key Concepts

* **Namespace Management**

  * Each schema provides a **separate namespace** for objects.
  * Objects with the same name can exist in different schemas within the same database.

* **Default Schemas**

  * **public**: Default schema for objects created without specifying a schema.
  * **pg\_catalog**: System schema containing system tables, functions, and types.
  * **information\_schema**: Standard SQL schema exposing metadata about the database.

* **Schema Creation and Management**

  * `CREATE SCHEMA` – Create a new schema.
  * `ALTER SCHEMA` – Modify schema properties, such as ownership.
  * `DROP SCHEMA` – Remove a schema; can optionally cascade to drop all objects within it.
  * `SET search_path` – Defines schema search order for object resolution.

* **Object Organization**

  * Tables, views, sequences, indexes, functions, types, and operators can all reside within a schema.
  * Supports modular database design and easier maintenance.

* **Access Control**

  * Permissions can be granted per schema:

    * `USAGE` – Allows access to schema.
    * `CREATE` – Allows creation of objects in schema.
  * Combined with role-based access control for fine-grained security.

* **Cross-Schema References**

  * Objects can reference others in **different schemas** using `schema_name.object_name`.
  * Enables modular design and code reuse.

* **Schema Usage in Queries**

  * Search path determines which schema is used when **object name is unqualified**.
  * Allows overriding default object resolution order.

### Summary

Schemas in PostgreSQL provide a **logical organizational layer** within databases. They:

* Prevent name collisions
* Organize objects for clarity and maintainability
* Control access via privileges
* Support modular and multi-tenant database designs

---
