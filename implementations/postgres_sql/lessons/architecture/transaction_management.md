## PostgreSQL – Transaction Management

### Overview

Transaction management in PostgreSQL ensures **data consistency, reliability, and isolation** during concurrent access. It follows **ACID principles** and uses **Multi-Version Concurrency Control (MVCC)** to handle multiple transactions simultaneously without conflicts.

### ACID Properties

* **Atomicity**

  * Ensures a transaction is **all-or-nothing**.
  * Either all operations succeed, or none are applied.
* **Consistency**

  * Database remains in a **valid state** before and after a transaction.
  * Enforces constraints, triggers, and rules.
* **Isolation**

  * Concurrent transactions do not interfere with each other.
  * Implemented through **transaction isolation levels**.
* **Durability**

  * Once a transaction is committed, its changes are **permanent**, even in case of system crash.
  * Achieved via **Write-Ahead Logging (WAL)**.

### Multi-Version Concurrency Control (MVCC)

* **Concept**:

  * Each row stores **multiple versions** of data.
  * Transactions see a **consistent snapshot** of the database.
* **Benefits**:

  * Readers don’t block writers, and writers don’t block readers.
  * Reduces lock contention and improves concurrency.
* **Mechanism**:

  * Each tuple stores:

    * **Transaction ID (xmin)** – creator of the tuple.
    * **Transaction ID (xmax)** – transaction that deleted/updated the tuple.
    * Visibility rules determine which version a transaction sees.

### Transaction Commands

* **BEGIN / START TRANSACTION**

  * Starts a new transaction block.
* **COMMIT**

  * Saves all changes made in the transaction.
* **ROLLBACK**

  * Undoes all changes in the transaction block.
* **SAVEPOINT**

  * Creates a sub-transaction point for partial rollback.
* **RELEASE SAVEPOINT**

  * Removes a savepoint without affecting the transaction.
* **ROLLBACK TO SAVEPOINT**

  * Rolls back to a specific savepoint without aborting the entire transaction.

### Isolation Levels

* **Read Uncommitted**

  * Rarely used; allows reading uncommitted changes.
* **Read Committed (default)**

  * Each query sees **data committed before it started**.
  * Non-repeatable reads possible.
* **Repeatable Read**

  * Ensures **all queries in a transaction see the same snapshot**.
  * Prevents non-repeatable reads; phantom reads still possible.
* **Serializable**

  * Strictest level.
  * Ensures **transactions appear to run sequentially**.
  * Prevents dirty reads, non-repeatable reads, and phantoms.

### Locking and Concurrency

* **Row-Level Locks**

  * Automatically acquired by UPDATE, DELETE, SELECT FOR UPDATE.
* **Table-Level Locks**

  * Acquired during schema changes or explicit lock commands.
* **Advisory Locks**

  * User-defined locks for application-level concurrency control.

### Summary

PostgreSQL transaction management is **robust, ACID-compliant, and optimized for high concurrency** through MVCC. Understanding isolation levels, savepoints, and locking mechanisms is essential for maintaining **data integrity and performance**.

---
