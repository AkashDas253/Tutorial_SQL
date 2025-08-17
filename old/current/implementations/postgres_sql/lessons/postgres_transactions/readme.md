### **PostgreSQL Transactions**  

#### **Overview**  
A **transaction** in PostgreSQL is a sequence of operations executed as a single unit. It ensures **atomicity**, **consistency**, **isolation**, and **durability** (**ACID** properties).  

---

### **1. Starting a Transaction**  

- **BEGIN**: Starts a transaction block.  
  ```sql
  BEGIN;
  ```
  
---

### **2. Committing a Transaction**  
- **COMMIT**: Saves all changes made within the transaction.  
  ```sql
  COMMIT;
  ```

---

### **3. Rolling Back a Transaction**  
- **ROLLBACK**: Cancels all changes if an error occurs.  
  ```sql
  ROLLBACK;
  ```

---

### **4. Example: Using Transactions**  

```sql
BEGIN;

UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;

COMMIT;
```
✅ Ensures money is deducted and added together.

---

### **5. Rollback Example**  
If an error occurs, use `ROLLBACK` to cancel all changes:  

```sql
BEGIN;

UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;

ROLLBACK;
```
❌ No changes will be saved.

---

### **6. Savepoints in Transactions**  
A **SAVEPOINT** allows partial rollback within a transaction.  

```sql
BEGIN;

UPDATE accounts SET balance = balance - 500 WHERE id = 1;
SAVEPOINT sp1;

UPDATE accounts SET balance = balance + 500 WHERE id = 2;
ROLLBACK TO sp1;

COMMIT;
```
- Rolls back to `sp1` without affecting the first update.

---

### **7. Transaction Isolation Levels**  
PostgreSQL supports different levels to control concurrency.  

| Isolation Level | Description |
|----------------|-------------|
| **READ COMMITTED (Default)** | Sees only committed changes. |
| **REPEATABLE READ** | Prevents reading uncommitted changes. |
| **SERIALIZABLE** | Ensures full isolation (highest level). |

- **Setting an Isolation Level**  
  ```sql
  BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;
  ```

---

### **8. Autocommit Mode**  
By default, PostgreSQL commits every statement.  
To use transactions, disable **autocommit** and use `BEGIN` explicitly.

```sql
SET AUTOCOMMIT = OFF;
```

---

### **9. Benefits of Transactions**  

✅ Ensures **data consistency** and **atomicity**.  
✅ Prevents **partial updates** in case of failure.  
✅ Provides **concurrency control** through isolation levels.  

---
