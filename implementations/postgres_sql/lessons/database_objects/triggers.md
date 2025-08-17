## PostgreSQL – Triggers

### Overview

A **trigger** in PostgreSQL is a **special kind of stored procedure** that is automatically executed in response to **certain events on a table or view**. Triggers help **enforce data integrity, automate tasks, and implement business logic** at the database level.

### Key Concepts

* **Purpose**

  * Automatically execute actions in response to **INSERT, UPDATE, DELETE, or TRUNCATE** events.
  * Enforce complex constraints not supported by standard constraints.
  * Maintain audit logs, derived data, or replicate changes.

* **Trigger Types**

  * **Row-Level Triggers**

    * Fired **once per affected row**.
    * Can access the old and new values of each row.
  * **Statement-Level Triggers**

    * Fired **once per SQL statement**, regardless of how many rows are affected.
  * **BEFORE Trigger**

    * Executes **before the event**.
    * Can modify input values or prevent the operation.
  * **AFTER Trigger**

    * Executes **after the event**.
    * Used for logging, auditing, or cascading operations.
  * **INSTEAD OF Trigger**

    * Used on **views**.
    * Replaces the standard action with custom logic.

* **Trigger Functions**

  * Triggers call **special functions** (usually written in PL/pgSQL or another procedural language).
  * Functions define the logic executed by the trigger.
  * Must return **`TRIGGER`** type.

* **Creating Triggers**

  * `CREATE TRIGGER trigger_name`

    * Specifies timing (`BEFORE` / `AFTER` / `INSTEAD OF`)
    * Specifies event (`INSERT`, `UPDATE`, `DELETE`, `TRUNCATE`)
    * Associates with a table or view
    * References the trigger function
  * Example syntax:

    ```sql
    CREATE TRIGGER audit_trigger
    BEFORE INSERT ON employees
    FOR EACH ROW
    EXECUTE FUNCTION log_audit();
    ```

* **Managing Triggers**

  * `ALTER TABLE ... ENABLE/DISABLE TRIGGER` – Temporarily enable or disable triggers.
  * `DROP TRIGGER trigger_name ON table_name` – Delete a trigger permanently.

* **Usage Scenarios**

  * Maintain **audit trails** of data changes.
  * Enforce **complex validation rules**.
  * Synchronize **derived tables or materialized views**.
  * Implement **replication or notifications**.

* **Considerations**

  * Overuse of triggers can **impact performance** due to additional operations per event.
  * Logic in triggers should be **deterministic and efficient**.
  * Triggers fire **per transaction**, not per session.

### Summary

Triggers in PostgreSQL are **automatic procedures tied to table or view events**:

* Row-level or statement-level execution
* BEFORE, AFTER, or INSTEAD OF timing
* Invoke trigger functions to enforce logic, auditing, or cascading operations
* Powerful tool for maintaining **data integrity and automation**

---
