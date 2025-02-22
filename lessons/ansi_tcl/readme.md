## ANSI Transaction Control Language (TCL)

TCL is a subset of SQL used to manage the changes made by DML statements. It ensures that database operations are executed in a reliable and consistent manner, enabling control over transaction handling. TCL helps in managing the execution and rollback of transactions, ensuring the integrity of the database.

### TCL Commands

| **Command**            | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `COMMIT`               | Permanently saves all changes made during the current transaction.                                       | `COMMIT;`                                                           |  
| `ROLLBACK`             | Reverts the changes made during the current transaction.                                                 | `ROLLBACK;`                                                         |  
| `SAVEPOINT`            | Sets a point within a transaction to which you can later roll back.                                       | `SAVEPOINT save1;`                                                  |  
| `RELEASE SAVEPOINT`    | Removes a savepoint, making it unavailable for rollback.                                                  | `RELEASE SAVEPOINT save1;`                                          |  
| `SET TRANSACTION`      | Sets properties for the current transaction (e.g., isolation level, access mode, read/write mode).       | `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;`                     |  

---

### `COMMIT` Command

The `COMMIT` command is used to save all the changes made during the current transaction to the database permanently. Once a `COMMIT` is issued, the changes cannot be rolled back.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `COMMIT`               | Saves all changes made in the transaction permanently.                                                    | `COMMIT;`                                                           |  

**Usage Example**:  
```sql
BEGIN;
UPDATE employees SET age = 29 WHERE name = 'John Doe';
COMMIT;
```

---

### `ROLLBACK` Command

The `ROLLBACK` command is used to undo all the changes made during the current transaction. This is particularly useful when an error occurs, and the transaction must be aborted to maintain data consistency.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `ROLLBACK`             | Reverts all changes made in the current transaction.                                                     | `ROLLBACK;`                                                         |  

**Usage Example**:  
```sql
BEGIN;
UPDATE employees SET age = 29 WHERE name = 'John Doe';
ROLLBACK;
```

---

### `SAVEPOINT` Command

The `SAVEPOINT` command is used to set a point within a transaction to which you can later roll back, instead of rolling back the entire transaction. This allows for partial rollbacks.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `SAVEPOINT`            | Defines a savepoint within the transaction.                                                              | `SAVEPOINT save1;`                                                  |  

**Usage Example**:  
```sql
BEGIN;
UPDATE employees SET age = 29 WHERE name = 'John Doe';
SAVEPOINT save1;
UPDATE employees SET age = 30 WHERE name = 'Jane Doe';
ROLLBACK TO SAVEPOINT save1;  -- Rolls back to savepoint, undoing second update
COMMIT;
```

---

### `RELEASE SAVEPOINT` Command

The `RELEASE SAVEPOINT` command removes a previously set savepoint, making it no longer available for rollback.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                         |  
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `RELEASE SAVEPOINT`    | Removes a savepoint from the transaction.                                                                | `RELEASE SAVEPOINT save1;`                                          |  

**Usage Example**:  
```sql
BEGIN;
UPDATE employees SET age = 29 WHERE name = 'John Doe';
SAVEPOINT save1;
UPDATE employees SET age = 30 WHERE name = 'Jane Doe';
RELEASE SAVEPOINT save1;  -- Removes savepoint after it is no longer needed
COMMIT;
```

---

### `SET TRANSACTION` Command

The `SET TRANSACTION` command allows you to configure the properties of a transaction, such as setting the isolation level, access mode, or read/write mode. This helps control how transactions interact with each other.

#### Syntax Overview

| **Clause**                    | **Description**                                                                                         | **Example**                                                         |  
|--------------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|  
| `ISOLATION LEVEL`              | Defines how transactions interact with other concurrent transactions.                                    | `SET TRANSACTION ISOLATION LEVEL READ COMMITTED;`                   |  
| `READ ONLY / READ WRITE`       | Specifies whether the transaction can modify data.                                                      | `SET TRANSACTION READ ONLY;`                                         |  
| `DEFERRABLE / NOT DEFERRABLE`  | Determines whether the transaction can be delayed for better performance in some cases.                  | `SET TRANSACTION DEFERRABLE;`                                        |  

**Usage Example**:  
```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE READ WRITE;
BEGIN;
UPDATE employees SET age = 29 WHERE name = 'John Doe';
COMMIT;
```

---

### Transaction Properties

Transactions can be set to different isolation levels to control concurrency. Common isolation levels include:

| **Isolation Level**               | **Description**                                                                                                                                           |  
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|  
| `READ UNCOMMITTED`               | Allows transactions to read data that has not yet been committed by other transactions (dirty reads).                                                     |  
| `READ COMMITTED`                 | Ensures that transactions can only read committed data, preventing dirty reads.                                                                          |  
| `REPEATABLE READ`                | Prevents other transactions from modifying or inserting data that the current transaction is reading (phantom reads).                                      |  
| `SERIALIZABLE`                   | The strictest isolation level, ensuring no other transactions can access the same data until the current transaction is complete.                          |  

---

### Access Modes in `SET TRANSACTION`

Access modes define whether a transaction can modify data.

| **Access Mode**  | **Description**                                  |  
|------------------|--------------------------------------------------|  
| `READ ONLY`      | The transaction is restricted to read operations only. |  
| `READ WRITE`     | The transaction can perform both read and write operations. |  

---

### Deferrable Transactions

Some databases allow transactions to be deferred for optimization.

| **Mode**            | **Description**                                                                                          |  
|---------------------|---------------------------------------------------------------------------------------------------------|  
| `DEFERRABLE`       | Allows the database to defer checking certain constraints until the transaction commits.                 |  
| `NOT DEFERRABLE`   | Enforces all constraints immediately.                                                                    |  

**Usage Example**:  
```sql
SET TRANSACTION DEFERRABLE;
BEGIN;
UPDATE employees SET salary = salary * 1.10;
COMMIT;
```

---

### Conclusion

TCL commands are crucial for ensuring data consistency and integrity within a database. `COMMIT` and `ROLLBACK` are used to finalize or undo transactions, while `SAVEPOINT` allows for partial rollbacks. `SET TRANSACTION` enables the configuration of transaction properties, such as isolation levels, access modes, and deferrable constraints, to manage concurrent operations effectively.
