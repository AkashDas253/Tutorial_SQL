## PostgreSQL – Transaction Control

### Overview

**Transaction Control** in PostgreSQL manages **groups of SQL statements as a single unit of work**. Transactions ensure **data integrity and consistency** using **ACID (Atomicity, Consistency, Isolation, Durability)** principles.

### Key Concepts

* **Purpose**

  * Ensure that multiple operations **succeed or fail together**.
  * Maintain database **consistency** even in case of errors or system failures.
  * Control **concurrency and isolation** between transactions.

* **Transaction Commands**

  * **BEGIN / START TRANSACTION**

    * Starts a new transaction block.

      ```sql
      BEGIN;
      ```
  * **COMMIT**

    * Makes all changes in the transaction **permanent**.

      ```sql
      COMMIT;
      ```
  * **ROLLBACK**

    * Reverts all changes in the transaction.

      ```sql
      ROLLBACK;
      ```
  * **SAVEPOINT**

    * Sets a **named point** within a transaction to allow partial rollback.

      ```sql
      SAVEPOINT sp1;
      ROLLBACK TO SAVEPOINT sp1;
      ```
  * **RELEASE SAVEPOINT**

    * Removes a savepoint once it is no longer needed.

      ```sql
      RELEASE SAVEPOINT sp1;
      ```
  * **SET TRANSACTION**

    * Sets properties for the current transaction, like **isolation level or read/write mode**.

* **Transaction Properties (ACID)**

  * **Atomicity**

    * Ensures all operations in a transaction **succeed or fail together**.
  * **Consistency**

    * Database remains in a **valid state** before and after the transaction.
  * **Isolation**

    * Concurrent transactions **do not interfere** with each other.
    * Controlled via **isolation levels**:

      * **READ UNCOMMITTED** – Allows dirty reads.
      * **READ COMMITTED** – Default; sees only committed changes.
      * **REPEATABLE READ** – Prevents non-repeatable reads.
      * **SERIALIZABLE** – Highest isolation; prevents phantom reads.
  * **Durability**

    * Once committed, changes are **permanent even after crashes**.

* **Transaction Modes**

  * **Read-Only**

    * Transaction cannot modify data.

      ```sql
      SET TRANSACTION READ ONLY;
      ```
  * **Read-Write**

    * Default; transaction can modify data.

      ```sql
      SET TRANSACTION READ WRITE;
      ```

* **Nested Transactions**

  * PostgreSQL supports nested transactions using **SAVEPOINTS**.
  * True nested transactions are not supported; savepoints allow **partial rollbacks**.

* **Considerations**

  * Long-running transactions may **lock rows or tables**, affecting concurrency.
  * Deadlocks can occur when multiple transactions wait on each other.
  * Proper transaction management ensures **performance, integrity, and isolation**.

### Summary

Transaction Control in PostgreSQL ensures **data integrity and consistency** through **ACID-compliant transactions**:

* BEGIN, COMMIT, ROLLBACK, SAVEPOINT, RELEASE SAVEPOINT
* Supports isolation levels and read/write modes
* Nested operations handled via savepoints
* Essential for **concurrent and reliable database operations**

---
