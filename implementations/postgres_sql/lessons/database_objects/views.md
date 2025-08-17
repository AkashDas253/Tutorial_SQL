## PostgreSQL – Views

### Overview

A **view** in PostgreSQL is a **virtual table** that presents the result of a query as a named object. Views do not store data physically (except for **materialized views**) and provide a **simplified or customized representation** of one or more tables.

### Key Concepts

* **Purpose**

  * Simplify complex queries.
  * Provide a layer of abstraction for users.
  * Enhance security by restricting access to specific columns or rows.
  * Enable modular and reusable query logic.

* **Types of Views**

  * **Simple View**

    * Defined by a single SELECT statement without joins, aggregates, or subqueries.
    * Can allow updates if it references only one base table.
  * **Complex View**

    * Defined by SELECT with joins, aggregates, grouping, or subqueries.
    * Typically **read-only**, cannot be updated directly.
  * **Materialized View**

    * Stores the **query result physically** on disk.
    * Improves performance for expensive queries.
    * Must be refreshed manually (`REFRESH MATERIALIZED VIEW`) or on schedule.

* **View Creation & Management**

  * `CREATE VIEW view_name AS SELECT ...`
  * `CREATE MATERIALIZED VIEW view_name AS SELECT ...`
  * `ALTER VIEW` – Rename or change security options.
  * `DROP VIEW` / `DROP MATERIALIZED VIEW` – Delete the view.

* **Querying Views**

  * Treated like a regular table in SELECT statements.
  * Supports filtering, ordering, and joining with other tables or views.
  * Materialized views can be indexed for faster access.

* **Updatable Views**

  * Views can be **updatable** if they map clearly to a single base table.
  * Rules or **INSTEAD OF triggers** can be used to allow updates on complex views.

* **Security and Access Control**

  * Grant privileges on views separately from underlying tables.
  * Helps enforce **row-level or column-level security**.

* **Performance Considerations**

  * Regular views are **computed at query time**, so complex views can be expensive.
  * Materialized views trade **storage for faster query execution**.

### Summary

Views in PostgreSQL are **virtual tables** that:

* Simplify query complexity
* Enhance security and abstraction
* Support materialized storage for performance optimization
* Can be read-only or updatable depending on their complexity

---
