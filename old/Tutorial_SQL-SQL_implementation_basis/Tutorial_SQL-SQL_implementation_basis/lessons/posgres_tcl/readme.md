## **PostgreSQL TCL (Transaction Control Language) Cheatsheet**  

#### **1. Transactions**  
| Action | Command |
|--------|---------|
| Start a Transaction | `BEGIN;` or `START TRANSACTION;` |
| Commit a Transaction | `COMMIT;` |
| Rollback a Transaction | `ROLLBACK;` |

#### **2. Savepoints** (Partial Rollback)  
| Action | Command |
|--------|---------|
| Create Savepoint | `SAVEPOINT savepoint_name;` |
| Rollback to Savepoint | `ROLLBACK TO SAVEPOINT savepoint_name;` |
| Release Savepoint | `RELEASE SAVEPOINT savepoint_name;` |

#### **3. Transaction Isolation Levels**  
| Isolation Level | Command |
|----------------|---------|
| Read Uncommitted | `SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;` |
| Read Committed (Default) | `SET TRANSACTION ISOLATION LEVEL READ COMMITTED;` |
| Repeatable Read | `SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;` |
| Serializable | `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;` |
