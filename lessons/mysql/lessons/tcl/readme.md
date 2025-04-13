## Transaction Control Language (TCL) in MySQL

---

### ▪️ Overview

**Transaction Control Language (TCL)** in MySQL refers to the set of SQL commands used to manage transactions within a database. A **transaction** is a sequence of operations performed as a single unit, which ensures data integrity and consistency.

TCL commands are primarily used to:
- Control the behavior of transactions.
- Ensure that operations are completed successfully or rolled back to a consistent state if any part of the transaction fails.

The most commonly used TCL commands are:
- **`COMMIT`**: Makes all changes made in the current transaction permanent.
- **`ROLLBACK`**: Undoes all changes made in the current transaction.
- **`SAVEPOINT`**: Creates a point within a transaction to which you can later roll back.
- **`SET TRANSACTION`**: Defines the characteristics of the transaction.

---

### ▪️ Key TCL Commands

| Command        | Purpose                                          |
|----------------|--------------------------------------------------|
| `COMMIT`       | Commits the current transaction, making all changes permanent |
| `ROLLBACK`     | Rolls back the current transaction to the last committed state |
| `SAVEPOINT`    | Creates a point within a transaction to roll back to |
| `SET TRANSACTION` | Sets the isolation level or other transaction characteristics |

---

### ▪️ Syntax and Usage

#### 🔹 `COMMIT`
```sql
-- Commits the current transaction
COMMIT;
```
- **Usage**: This command commits all changes made during the current transaction, making them permanent in the database.

#### 🔹 `ROLLBACK`
```sql
-- Rolls back the current transaction
ROLLBACK;
```
- **Usage**: If an error occurs during the transaction or you need to cancel the transaction, this command undoes all changes since the last `COMMIT` or `SAVEPOINT`.

#### 🔹 `SAVEPOINT`
```sql
-- Creates a savepoint within the transaction
SAVEPOINT savepoint_name;
```
- **Usage**: Sets a specific point within a transaction to which you can later roll back, allowing partial rollbacks.

#### 🔹 `ROLLBACK TO SAVEPOINT`
```sql
-- Rolls back to a specific savepoint
ROLLBACK TO SAVEPOINT savepoint_name;
```
- **Usage**: This command undoes the work done after the specified savepoint without affecting the preceding operations.

#### 🔹 `SET TRANSACTION`
```sql
-- Sets the transaction characteristics
SET TRANSACTION ISOLATION LEVEL level;
```
- **Usage**: Defines the isolation level for the transaction, which controls how changes made by the transaction are visible to other transactions.

---

### ▪️ Transaction Properties (ACID)

TCL commands help ensure that transactions meet the **ACID** properties:

| Property        | Description                                      |
|-----------------|--------------------------------------------------|
| **Atomicity**   | A transaction is all or nothing. If one part fails, the entire transaction fails. |
| **Consistency** | The database is left in a consistent state after the transaction, with all rules and constraints upheld. |
| **Isolation**   | Transactions are isolated from each other, so intermediate states of a transaction are not visible to other transactions. |
| **Durability**  | Once a transaction is committed, its changes are permanent, even in the case of a system failure. |

---

### ▪️ Isolation Levels in MySQL

Isolation levels control the visibility of uncommitted changes to other transactions. MySQL supports several isolation levels:

| Isolation Level        | Description                                             |
|------------------------|---------------------------------------------------------|
| `READ UNCOMMITTED`     | Allows transactions to see uncommitted changes from other transactions (lowest isolation). |
| `READ COMMITTED`       | Ensures that only committed changes are visible, but allows non-repeatable reads. |
| `REPEATABLE READ`      | Guarantees that once a value is read, it cannot be changed by other transactions until the transaction is complete (default in MySQL). |
| `SERIALIZABLE`         | Provides the highest isolation by ensuring that transactions are executed in a serial manner (one after the other). |

---

### ▪️ Usage Scenarios

| Scenario                                   | TCL Command Used        |
|--------------------------------------------|-------------------------|
| Commit changes after all operations are successful | `COMMIT`              |
| Undo all changes due to an error           | `ROLLBACK`             |
| Save a point in the middle of a transaction for partial rollback | `SAVEPOINT`           |
| Roll back to a previous savepoint after encountering an issue | `ROLLBACK TO SAVEPOINT` |
| Set the isolation level for a transaction | `SET TRANSACTION`      |

---

### ▪️ Example Workflow

1. **Starting a Transaction**:
```sql
START TRANSACTION;
```
- Begins a new transaction, marking the start of the operations.

2. **Performing Operations**:
```sql
UPDATE account SET balance = balance - 100 WHERE account_id = 1;
UPDATE account SET balance = balance + 100 WHERE account_id = 2;
```
- These operations modify the data.

3. **Committing the Transaction**:
```sql
COMMIT;
```
- After the changes are verified to be correct, the `COMMIT` command makes the changes permanent.

4. **Rolling Back in Case of Error**:
```sql
ROLLBACK;
```
- If an error occurs during the transaction, `ROLLBACK` undoes all changes made since the last commit or savepoint.

5. **Using SAVEPOINT for Partial Rollback**:
```sql
SAVEPOINT point1;
UPDATE account SET balance = balance - 50 WHERE account_id = 1;
-- Oops! An error occurred.
ROLLBACK TO SAVEPOINT point1;
```
- The operations after the savepoint are undone, but the previous changes remain intact.

---

### ▪️ Best Practices for Transaction Management

| Best Practice                           | Benefit                                       |
|-----------------------------------------|-----------------------------------------------|
| Use transactions for critical data modifications | Ensures data integrity and consistency       |
| Keep transactions short and efficient   | Reduces lock contention and improves performance |
| Roll back transactions in case of errors | Avoids inconsistent or partial changes       |
| Use `SAVEPOINT` for complex transactions | Allows partial rollbacks without undoing everything |
| Choose an appropriate isolation level   | Balances performance and consistency needs   |

---

### ▪️ TCL vs DCL vs DML vs DDL

| Feature         | TCL                                    | DCL                             | DML                             | DDL                             |
|-----------------|----------------------------------------|---------------------------------|---------------------------------|----------------------------------|
| Purpose         | Manage transactions                    | Control access and permissions  | Manipulate data                 | Define schema                   |
| Transactional   | Yes                                    | No                              | Yes                             | No                               |
| Rollback Support| Yes                                    | No                              | Yes                             | No                               |
| Affects         | Data (commit, rollback)                | Security and user privileges    | Data (modified)                 | Structure (database/table)       |

---
