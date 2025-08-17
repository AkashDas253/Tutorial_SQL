## PostgreSQL – Rules

### Overview

A **rule** in PostgreSQL is a **database object that modifies the behavior of queries** on tables or views. Rules provide a way to **rewrite SQL statements** automatically, often used to implement **updatable views or conditional logic**.

### Key Concepts

* **Purpose**

  * Automatically transform or redirect queries (INSERT, UPDATE, DELETE, or SELECT).
  * Support updatable views by rewriting operations to affect underlying tables.
  * Implement custom behavior without changing application queries.

* **Rule Types**

  * **INSTEAD Rules**

    * Replace the original query with one or more alternative queries.
    * Commonly used to make **views updatable**.
  * **DO Rules**

    * Add additional queries to execute **in addition to the original query**.
    * Useful for logging, auditing, or cascading operations.

* **Rule Creation**

  * `CREATE RULE rule_name AS ON event_type TO table_or_view DO [INSTEAD | ALSO] action_query`
  * Example syntax:

    ```sql
    CREATE RULE update_view AS
    ON UPDATE TO employee_view
    DO INSTEAD
    UPDATE employees SET salary = NEW.salary WHERE id = NEW.id;
    ```

* **Events Supported**

  * `SELECT` – Rarely used; modifies how a view or table is queried.
  * `INSERT` – Alters insert behavior.
  * `UPDATE` – Alters update behavior.
  * `DELETE` – Alters delete behavior.

* **Advantages**

  * Allows **transparent query modification**.
  * Supports updatable views and complex conditional actions.
  * Can reduce the need for triggers in simple scenarios.

* **Considerations**

  * Rules are **applied at query rewrite time**, before execution.
  * Complex rules can be **hard to debug**.
  * PostgreSQL **advises using triggers** for most row-level actions because they are more predictable and maintainable.
  * Rules operate at the **statement level**, not per row.

* **Management**

  * `ALTER RULE` – Rename or change ownership.
  * `DROP RULE rule_name ON table_or_view` – Remove a rule permanently.
  * `pg_rules` system catalog – View defined rules.

### Summary

Rules in PostgreSQL provide **query rewrite functionality**:

* Modify behavior of SELECT, INSERT, UPDATE, DELETE statements
* INSTEAD or DO rules control replacement or additional actions
* Useful for updatable views, logging, and custom query handling
* Less flexible than triggers for complex row-level operations

---
