## **Transaction Control Language (TCL) in PostgreSQL**  

TCL manages transactions in a database, ensuring **atomicity, consistency, isolation, and durability (ACID)** properties. It includes commands to **commit**, **rollback**, and **control transactions**.  

---

### **1. COMMIT – Save Changes**  
The `COMMIT` command permanently saves all changes made in the current transaction.

#### **Syntax**  
```sql
COMMIT;
```

#### **Example**  
```sql
BEGIN;
UPDATE employees SET salary = salary * 1.1 WHERE department = 'HR';
COMMIT;
```
> This increases salaries by 10% for employees in HR and **saves the changes permanently**.

---

### **2. ROLLBACK – Undo Changes**  
The `ROLLBACK` command cancels all changes made in the current transaction.

#### **Syntax**  
```sql
ROLLBACK;
```

#### **Example**  
```sql
BEGIN;
DELETE FROM employees WHERE id = 10;
ROLLBACK;
```
> The `DELETE` operation is **canceled**, and `id = 10` remains in the `employees` table.

---

### **3. SAVEPOINT – Set a Save State**  
A `SAVEPOINT` allows partial rollbacks by marking a specific point within a transaction.

#### **Syntax**  
```sql
SAVEPOINT savepoint_name;
```

#### **Example**  
```sql
BEGIN;
UPDATE employees SET salary = salary * 1.1 WHERE department = 'HR';
SAVEPOINT before_bonus;
UPDATE employees SET salary = salary + 500 WHERE department = 'HR';
ROLLBACK TO before_bonus;
COMMIT;
```
> The **bonus increase is undone**, but the **10% salary raise remains**.

---

### **4. RELEASE SAVEPOINT – Remove a Savepoint**  
Deletes a `SAVEPOINT` so it **can’t be rolled back** anymore.

#### **Syntax**  
```sql
RELEASE SAVEPOINT savepoint_name;
```

#### **Example**  
```sql
SAVEPOINT before_bonus;
UPDATE employees SET salary = salary + 500 WHERE department = 'HR';
RELEASE SAVEPOINT before_bonus;
```
> The **savepoint is removed**, making rollback to `before_bonus` **impossible**.

---

### **5. ROLLBACK TO SAVEPOINT – Undo Partial Changes**  
Restores the state of the transaction to a savepoint.

#### **Syntax**  
```sql
ROLLBACK TO SAVEPOINT savepoint_name;
```

#### **Example**  
```sql
BEGIN;
UPDATE employees SET salary = salary * 1.1 WHERE department = 'HR';
SAVEPOINT before_bonus;
UPDATE employees SET salary = salary + 500 WHERE department = 'HR';
ROLLBACK TO before_bonus;
COMMIT;
```
> **Bonus rollbacked**, but **10% salary increase remains**.

---

### **6. AUTOCOMMIT in PostgreSQL**  
- PostgreSQL **executes each statement as a transaction by default**.  
- To disable **autocommit** and manage transactions manually:  
```sql
SET AUTOCOMMIT = OFF;
```

---

### **7. Transaction Isolation Levels**  
PostgreSQL supports **isolation levels** to control transaction visibility.

| **Level**         | **Effect** |
|-------------------|-----------|
| `READ UNCOMMITTED` | Allows dirty reads (not implemented in PostgreSQL, defaults to `READ COMMITTED`). |
| `READ COMMITTED` | Default. Reads only committed data, no dirty reads. |
| `REPEATABLE READ` | Ensures same results for the transaction duration. |
| `SERIALIZABLE` | Strictest. Transactions appear as executing in sequence. |

#### **Set Isolation Level Example**  
```sql
BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;
UPDATE employees SET salary = salary * 1.1;
COMMIT;
```

---

### **Notes**  
- **`COMMIT` makes changes permanent.**  
- **`ROLLBACK` cancels all uncommitted changes.**  
- **`SAVEPOINT` allows partial rollbacks.**  
- **PostgreSQL uses `READ COMMITTED` as the default isolation level.**  

---
