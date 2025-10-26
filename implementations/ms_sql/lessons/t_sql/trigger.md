## **Triggers in MS SQL Server**

---

### **Overview**

A **Trigger** in SQL Server is a **special type of stored procedure** that automatically executes in response to specific **events** (INSERT, UPDATE, DELETE, or DDL operations). Triggers enforce complex business rules, maintain data integrity, and enable audit tracking.

---

### **Types of Triggers**

#### **1. DML Triggers (Data Manipulation Language)**

Executed automatically in response to data modification statements.

* **AFTER Triggers**

  * Fired **after** the triggering DML statement completes successfully.
  * Used to **enforce referential integrity** or **log changes**.
  * Example:

    ```sql
    CREATE TRIGGER trgAfterInsert
    ON Employees
    AFTER INSERT
    AS
    BEGIN
        PRINT 'New employee record added.'
    END;
    ```

* **INSTEAD OF Triggers**

  * Fired **in place of** the triggering DML operation.
  * Useful for **complex views** where direct modifications are restricted.
  * Example:

    ```sql
    CREATE TRIGGER trgInsteadOfDelete
    ON Employees
    INSTEAD OF DELETE
    AS
    BEGIN
        PRINT 'Delete not allowed.'
    END;
    ```

---

#### **2. DDL Triggers (Data Definition Language)**

Fired in response to **schema changes** such as CREATE, ALTER, DROP statements.

* Used for **auditing database changes** or **preventing unauthorized modifications**.
* Example:

  ```sql
  CREATE TRIGGER trgPreventTableDrop
  ON DATABASE
  FOR DROP_TABLE
  AS
  BEGIN
      PRINT 'Dropping tables is not allowed.'
      ROLLBACK;
  END;
  ```

---

#### **3. Logon Triggers**

Fired **when a user session is established**.

* Used for **security control**, such as restricting logins during maintenance.
* Example:

  ```sql
  CREATE TRIGGER trgLogonLimit
  ON ALL SERVER
  FOR LOGON
  AS
  BEGIN
      IF ORIGINAL_LOGIN() = 'guest'
          ROLLBACK;
  END;
  ```

---

### **Special Tables**

* **`inserted`**: Holds new rows affected by INSERT or UPDATE.
* **`deleted`**: Holds old rows affected by DELETE or UPDATE.

Used to **compare before-and-after states** of data.

---

### **Trigger Order and Nesting**

* You can define **execution order** for multiple triggers using:

  ```sql
  sp_settriggerorder;
  ```
* SQL Server supports **nested triggers** up to **32 levels** deep.

---

### **Advantages**

* Enforces **business rules** automatically.
* Ensures **data consistency** and **audit tracking**.
* Enables **automated responses** to critical database events.

---

### **Disadvantages**

* Can **reduce performance** due to hidden execution.
* May cause **recursive or unexpected behaviors**.
* Harder to **debug and maintain** than explicit logic.

---

### **Best Practices**

* Use only when **business logic must be automatic**.
* Avoid **complex logic** inside triggers.
* Always **test thoroughly** to prevent unwanted recursion.
* Prefer **stored procedures or constraints** when possible.

---
