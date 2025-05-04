## **PostgreSQL Transactions: Comprehensive Cheatsheet**  

---

### **1. Overview of Transactions**  
| Feature | Description |
|---------|-------------|
| **Definition** | A transaction is a sequence of SQL statements executed as a single unit. |
| **Purpose** | Ensures data integrity and consistency in the database. |
| **Atomicity** | Either all operations in a transaction succeed or none are applied. |
| **Isolation** | Transactions execute independently of each other. |
| **Durability** | Changes made by committed transactions are permanently saved. |

---

### **2. Key Transaction Commands**  
| Command | Description |
|---------|-------------|
| `BEGIN` | Starts a new transaction. |
| `COMMIT` | Saves all changes made in the transaction. |
| `ROLLBACK` | Reverts all changes made in the transaction. |
| `SAVEPOINT` | Creates a save point within a transaction. |
| `ROLLBACK TO SAVEPOINT` | Rolls back to a specific save point without canceling the entire transaction. |
| `RELEASE SAVEPOINT` | Removes a previously set save point. |

---

### **3. Starting and Committing a Transaction**  
| Feature | Description |
|---------|-------------|
| Ensures that all queries execute as a single unit | If one fails, all changes are discarded. |

**Syntax:**  
```sql
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 500 WHERE account_id = 2;
COMMIT;
```

---

### **4. Rolling Back a Transaction**  
| Feature | Description |
|---------|-------------|
| Reverts all changes since `BEGIN` was executed | Ensures data integrity in case of an error. |

**Syntax:**  
```sql
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 500 WHERE account_id = 2;
ROLLBACK;
```

---

### **5. Using Savepoints in Transactions**  
| Feature | Description |
|---------|-------------|
| Allows partial rollbacks within a transaction | Useful for error handling in multi-step transactions. |

**Syntax:**  
```sql
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE account_id = 1;
SAVEPOINT sp1;
UPDATE accounts SET balance = balance + 500 WHERE account_id = 2;
ROLLBACK TO SAVEPOINT sp1;
COMMIT;
```

---

### **6. Setting Transaction Isolation Levels**  
| Isolation Level | Description |
|---------------|-------------|
| `READ UNCOMMITTED` | Allows dirty reads (rarely used in PostgreSQL). |
| `READ COMMITTED` (Default) | Prevents dirty reads, ensures only committed data is read. |
| `REPEATABLE READ` | Ensures consistent reads within a transaction. |
| `SERIALIZABLE` | Highest isolation, ensures complete transaction isolation. |

**Syntax:**  
```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

---

### **7. Auto-Commit Behavior**  
| Feature | Description |
|---------|-------------|
| PostgreSQL auto-commits transactions by default | Explicitly use `BEGIN` to start a transaction. |

**To disable auto-commit:**  
```sql
BEGIN;
-- Statements go here
COMMIT;
```
