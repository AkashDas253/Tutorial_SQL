## Transactions in PL/SQL

A **transaction** is a sequence of one or more SQL operations executed as a single unit of work. It ensures that either all operations are successfully completed (commit) or none are (rollback). Transactions are essential for maintaining data integrity, especially in multi-step processes.

In PL/SQL, transactions are controlled using SQL statements and PL/SQL control structures. These ensure that the database operations are atomic, consistent, isolated, and durable, which are the key properties of **ACID** transactions.

---

### **Transaction Control Statements**

PL/SQL provides the following key statements to manage transactions:

| **Statement**  | **Description**                                                                  |
|----------------|----------------------------------------------------------------------------------|
| `COMMIT`       | Permanently saves all changes made during the current transaction to the database. |
| `ROLLBACK`     | Undoes all changes made during the current transaction, restoring the database to its previous state. |
| `SAVEPOINT`    | Creates a point in the transaction to which you can later roll back.             |
| `SET TRANSACTION` | Sets properties for the current transaction, such as isolation level.          |

---

### **COMMIT Statement**

The `COMMIT` statement is used to **finalize** the transaction, making all changes made during the transaction permanent.

- **Usage**: When you issue a `COMMIT`, all changes made to the database are saved, and the transaction ends.
- **Syntax**:

```sql
COMMIT;
```

- **Example**:

```plsql
BEGIN
  INSERT INTO employees (employee_id, first_name, last_name, salary)
  VALUES (1001, 'John', 'Doe', 5000);
  COMMIT;  -- Saves the changes permanently
END;
```

---

### **ROLLBACK Statement**

The `ROLLBACK` statement is used to **undo** all changes made during the current transaction, returning the database to its state before the transaction began.

- **Usage**: A rollback is issued when you need to cancel a transaction, for example, due to an error or unwanted outcome.
- **Syntax**:

```sql
ROLLBACK;
```

- **Example**:

```plsql
BEGIN
  INSERT INTO employees (employee_id, first_name, last_name, salary)
  VALUES (1001, 'John', 'Doe', 5000);
  ROLLBACK;  -- Undoes the changes made so far
END;
```

---

### **SAVEPOINT Statement**

The `SAVEPOINT` statement creates a **named savepoint** within a transaction. It allows partial rollback to this savepoint instead of rolling back the entire transaction.

- **Usage**: Useful when you want to commit some changes but be able to undo others without losing everything.
- **Syntax**:

```sql
SAVEPOINT savepoint_name;
```

- **Example**:

```plsql
BEGIN
  INSERT INTO employees (employee_id, first_name, last_name, salary)
  VALUES (1001, 'John', 'Doe', 5000);
  SAVEPOINT after_insert;  -- Set a savepoint
  INSERT INTO employees (employee_id, first_name, last_name, salary)
  VALUES (1002, 'Jane', 'Smith', 6000);
  ROLLBACK TO after_insert;  -- Undo only the second insert
  COMMIT;  -- Commit the first insert
END;
```

---

### **SET TRANSACTION Statement**

The `SET TRANSACTION` statement is used to set properties for the current transaction, such as its **isolation level**.

- **Usage**: This is useful for controlling concurrency and locking behavior in multi-user environments.
- **Syntax**:

```sql
SET TRANSACTION [ISOLATION LEVEL level] [READ WRITE | READ ONLY];
```

Where:
- `ISOLATION LEVEL` specifies the transaction's isolation level, such as `READ COMMITTED` or `SERIALIZABLE`.
- `READ WRITE` or `READ ONLY` specifies whether the transaction is allowed to modify data.

- **Example**:

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN
  -- Transaction logic here
  COMMIT;
END;
```

---

### **Transaction Isolation Levels**

Transaction isolation levels determine how transactions interact with each other, particularly regarding **locking** and **visibility** of data. The most common levels are:

| **Isolation Level**         | **Description**                                                                |
|-----------------------------|--------------------------------------------------------------------------------|
| **READ UNCOMMITTED**         | Allows transactions to read uncommitted changes made by other transactions.    |
| **READ COMMITTED**           | Allows reading only committed data, but other transactions can still modify the data. |
| **REPEATABLE READ**          | Prevents other transactions from modifying the data that has been read.       |
| **SERIALIZABLE**             | Ensures transactions execute in a way that results in a consistent state, preventing any other transactions from modifying data. |

---

### **Transaction Example**

Here is an example that demonstrates how to manage a transaction with `COMMIT`, `ROLLBACK`, and `SAVEPOINT`:

```plsql
DECLARE
  v_balance NUMBER;
BEGIN
  -- Start of transaction
  SELECT balance INTO v_balance FROM accounts WHERE account_id = 1001;

  IF v_balance >= 500 THEN
    -- Transaction logic
    UPDATE accounts SET balance = balance - 500 WHERE account_id = 1001;
    SAVEPOINT after_withdrawal;  -- Set savepoint after withdrawal

    -- Simulating a failure
    ROLLBACK TO after_withdrawal;  -- Undo the withdrawal but retain other changes

    -- Commit the transaction if all goes well
    COMMIT;
  ELSE
    ROLLBACK;  -- Insufficient funds, undo the entire transaction
  END IF;
END;
```

---

### **Key Considerations**

- **Atomicity**: A transaction is atomic, meaning it is all-or-nothing. Either all operations are successfully committed, or none are applied.
- **Consistency**: A transaction brings the database from one consistent state to another, maintaining all integrity constraints.
- **Isolation**: A transaction's operations are isolated from other transactions. This can be controlled with isolation levels.
- **Durability**: Once committed, a transaction's changes are permanent and will survive system crashes.

---

### **Conclusion**

Transactions in PL/SQL are essential for ensuring data integrity and consistency. By using **COMMIT**, **ROLLBACK**, **SAVEPOINT**, and **SET TRANSACTION**, developers can manage and control the execution of multiple SQL statements, ensuring that data changes are handled safely and correctly. Understanding transaction control is crucial for working in multi-user environments and building reliable applications.
