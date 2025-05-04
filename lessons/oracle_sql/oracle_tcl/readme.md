# **Transaction Control Language (TCL) in Oracle SQL**  

TCL (Transaction Control Language) in Oracle SQL is used to manage transactions in a database. Transactions ensure **data integrity** and **consistency** by grouping multiple SQL operations into a single logical unit.  

## **1. Transaction Concepts**  
- A **transaction** is a sequence of one or more SQL statements executed as a unit of work.  
- A transaction **starts automatically** when a DML statement (`INSERT`, `UPDATE`, `DELETE`) is executed.  
- Transactions **end** when a `COMMIT` or `ROLLBACK` is executed.  
- Transactions follow **ACID properties** (Atomicity, Consistency, Isolation, Durability).  

---

## **2. TCL Commands**  

| **Command**  | **Description** |
|-------------|---------------|
| `COMMIT`    | Saves all changes made by the transaction permanently in the database. |
| `ROLLBACK`  | Undoes all changes made by the transaction since the last `COMMIT`. |
| `SAVEPOINT` | Creates a checkpoint within a transaction to which a rollback can be performed. |
| `SET TRANSACTION` | Defines transaction properties like isolation level. |

---

## **3. Command Details and Usage**  

### **3.1 COMMIT**  
- Used to **permanently save** changes made by the current transaction.  
- Once a `COMMIT` is issued, changes cannot be undone.  

#### **Syntax:**  
```sql
COMMIT;
```

#### **Example:**  
```sql
UPDATE employees SET salary = salary * 1.1 WHERE department_id = 10;
COMMIT;
```

---

### **3.2 ROLLBACK**  
- Used to **undo changes** made by the current transaction.  
- If a transaction is **not committed**, it can be rolled back.  

#### **Syntax:**  
```sql
ROLLBACK;
```

#### **Example:**  
```sql
DELETE FROM employees WHERE department_id = 20;
ROLLBACK;  -- Cancels the deletion
```

---

### **3.3 SAVEPOINT**  
- Used to create a **checkpoint** in a transaction.  
- Allows rolling back to a specific point instead of the entire transaction.  

#### **Syntax:**  
```sql
SAVEPOINT savepoint_name;
```

#### **Example:**  
```sql
UPDATE employees SET salary = salary * 1.05 WHERE department_id = 30;
SAVEPOINT sp1;

UPDATE employees SET salary = salary * 1.10 WHERE department_id = 40;
SAVEPOINT sp2;

ROLLBACK TO sp1;  -- Rolls back changes made after sp1, but keeps those before it
COMMIT;
```

---

### **3.4 SET TRANSACTION**  
- Used to **set properties** for a transaction, such as isolation levels.  

#### **Syntax:**  
```sql
SET TRANSACTION READ ONLY;
```

#### **Example:**  
```sql
SET TRANSACTION READ WRITE;
INSERT INTO employees (emp_id, name, salary) VALUES (101, 'John Doe', 5000);
COMMIT;
```

---

## **4. Summary of TCL Commands**  

| **Command** | **Function** | **Reversible?** |
|------------|------------|---------------|
| `COMMIT` | Saves all changes permanently | ❌ No |
| `ROLLBACK` | Undoes all uncommitted changes | ✅ Yes |
| `SAVEPOINT` | Creates a checkpoint in a transaction | ✅ Yes |
| `SET TRANSACTION` | Defines transaction properties | ✅ Yes |
