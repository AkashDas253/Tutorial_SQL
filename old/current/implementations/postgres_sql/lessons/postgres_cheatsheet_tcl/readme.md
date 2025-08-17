## **PostgreSQL TCL (Transaction Control Language) Cheatsheet**  
 
### **1. Transactions**  
| Action | Command | Description |
|--------|---------|-------------|
| Start a Transaction | `BEGIN;` or `START TRANSACTION;` | Begins a new transaction block. |
| Commit a Transaction | `COMMIT;` | Saves all changes made in the current transaction. |
| Rollback a Transaction | `ROLLBACK;` | Reverts all changes made in the current transaction. |
| Commit and Chain | `COMMIT AND CHAIN;` | Commits the transaction and immediately starts a new one. |
| Rollback and Chain | `ROLLBACK AND CHAIN;` | Rolls back the transaction and immediately starts a new one. |

---

### **2. Savepoints (Partial Rollback)**  
| Action | Command | Description |
|--------|---------|-------------|
| Create Savepoint | `SAVEPOINT savepoint_name;` | Creates a checkpoint within a transaction. |
| Rollback to Savepoint | `ROLLBACK TO SAVEPOINT savepoint_name;` | Reverts changes to a specific savepoint without rolling back the entire transaction. |
| Release Savepoint | `RELEASE SAVEPOINT savepoint_name;` | Deletes a savepoint so it can no longer be used for rollback. |

---

### **3. Transaction Modes**  
| Mode | Command | Description |
|------|---------|-------------|
| Read-Only Transaction | `SET TRANSACTION READ ONLY;` | Ensures that no data modifications occur within the transaction. |
| Read-Write Transaction | `SET TRANSACTION READ WRITE;` | Allows data modifications (default mode). |
| Deferrable Transaction | `SET TRANSACTION DEFERRABLE;` | Delays transaction execution until it is safe to commit. |
| Non-Deferrable Transaction | `SET TRANSACTION NOT DEFERRABLE;` | Executes the transaction immediately. |

---

### **4. Transaction Isolation Levels**  
| Isolation Level | Command | Description |
|----------------|---------|-------------|
| Read Uncommitted | `SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;` | Allows dirty reads (uncommitted data), but PostgreSQL treats it as Read Committed. |
| Read Committed (Default) | `SET TRANSACTION ISOLATION LEVEL READ COMMITTED;` | Prevents dirty reads but allows non-repeatable reads. |
| Repeatable Read | `SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;` | Prevents dirty and non-repeatable reads but allows phantom reads. |
| Serializable | `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;` | Ensures full transaction isolation, preventing dirty, non-repeatable, and phantom reads. |

---

### **5. Two-Phase Commit (Distributed Transactions)**  
| Action | Command | Description |
|--------|---------|-------------|
| Prepare a Transaction | `PREPARE TRANSACTION 'txn_name';` | Prepares a transaction for a two-phase commit. |
| Commit a Prepared Transaction | `COMMIT PREPARED 'txn_name';` | Commits a previously prepared transaction. |
| Rollback a Prepared Transaction | `ROLLBACK PREPARED 'txn_name';` | Rolls back a previously prepared transaction. |

---

### **6. Setting Session-Level Transaction Properties**  
| Property | Command | Description |
|----------|---------|-------------|
| Default Isolation Level | `SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL level;` | Sets the default isolation level for all transactions in the session. |
| Default Transaction Mode | `SET SESSION CHARACTERISTICS AS TRANSACTION READ ONLY;` | Sets the default transaction mode for the session. |

---

### **7. Viewing and Managing Transactions**  
| Action | Command | Description |
|--------|---------|-------------|
| View Active Transactions | `SELECT * FROM pg_stat_activity WHERE state = 'active';` | Shows active transactions in the database. |
| View Running Transactions | `SELECT * FROM pg_stat_activity;` | Lists all currently running queries and transactions. |
| Cancel a Transaction | `SELECT pg_cancel_backend(pid);` | Cancels a transaction based on the process ID (PID). |
| Terminate a Transaction | `SELECT pg_terminate_backend(pid);` | Forces termination of a transaction. |

---
