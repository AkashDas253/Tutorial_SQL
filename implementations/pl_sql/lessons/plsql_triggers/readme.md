## Triggers in PL/SQL

A **trigger** is a stored procedure that is automatically invoked or "fired" when a certain event occurs on a table or view in a database. Triggers are used to enforce business rules, perform validation, maintain audit trails, or automate certain database operations.

Triggers in PL/SQL are associated with a **DML (Data Manipulation Language)** event like **INSERT**, **UPDATE**, or **DELETE** on a table or view. They can be defined to run either **BEFORE** or **AFTER** the event occurs, depending on the requirement.

### **Types of Triggers**

| **Trigger Type**        | **Description**                                                                      | **When Triggered**                                                      |
|-------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **BEFORE Trigger**       | Fired before the DML operation is performed.                                         | Before an `INSERT`, `UPDATE`, or `DELETE` operation on a table.         |
| **AFTER Trigger**        | Fired after the DML operation is completed.                                          | After an `INSERT`, `UPDATE`, or `DELETE` operation on a table.          |
| **INSTEAD OF Trigger**   | Used to perform an action instead of the DML operation. Typically used with views.   | Instead of an `INSERT`, `UPDATE`, or `DELETE` operation on a view.      |

---

### **Trigger Structure**

Triggers in PL/SQL are composed of several sections:

| **Section**             | **Description**                                              |
|-------------------------|--------------------------------------------------------------|
| **Trigger Name**         | The name of the trigger, which is unique within the schema.   |
| **Trigger Timing**       | Specifies when the trigger will be fired: `BEFORE`, `AFTER`, or `INSTEAD OF`. |
| **Trigger Event**        | Specifies the DML event that fires the trigger (`INSERT`, `UPDATE`, `DELETE`). |
| **Trigger Body**         | Contains the PL/SQL code that is executed when the trigger is fired. |

#### **Syntax for Creating a Trigger**

```plsql
CREATE [OR REPLACE] TRIGGER trigger_name
{BEFORE | AFTER | INSTEAD OF} 
{INSERT | UPDATE | DELETE} 
ON table_name
[FOR EACH ROW]
DECLARE
   -- Optional declarations
BEGIN
   -- PL/SQL statements to execute
END;
```

---

### **Trigger Example**

**1. BEFORE INSERT Trigger**

A `BEFORE INSERT` trigger ensures that no invalid data is inserted into a table. For example, before inserting a new employee record, we ensure that the salary is positive.

```plsql
CREATE OR REPLACE TRIGGER validate_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
   IF :new.salary <= 0 THEN
      RAISE_APPLICATION_ERROR(-20001, 'Salary must be positive.');
   END IF;
END;
```

- **:new.salary** refers to the new value of the `salary` column in the `employees` table.
- **RAISE_APPLICATION_ERROR** is used to generate a custom error message.

**2. AFTER UPDATE Trigger**

An `AFTER UPDATE` trigger can be used to log changes made to the `employees` table.

```plsql
CREATE OR REPLACE TRIGGER log_salary_change
AFTER UPDATE OF salary ON employees
FOR EACH ROW
BEGIN
   INSERT INTO salary_audit(employee_id, old_salary, new_salary, change_date)
   VALUES (:old.employee_id, :old.salary, :new.salary, SYSDATE);
END;
```

- **:old.salary** and **:new.salary** refer to the old and new values of the `salary` column.
- This trigger records changes in the `salary_audit` table whenever an employee's salary is updated.

**3. INSTEAD OF DELETE Trigger**

An `INSTEAD OF DELETE` trigger can be used on views to perform an alternate action, such as soft-deleting records by updating a flag instead of actually deleting a record.

```plsql
CREATE OR REPLACE TRIGGER instead_of_delete_trigger
INSTEAD OF DELETE ON employee_view
FOR EACH ROW
BEGIN
   UPDATE employees
   SET deleted_flag = 'Y'
   WHERE employee_id = :old.employee_id;
END;
```

- The trigger ensures that when a delete operation is performed on the `employee_view`, it updates the `deleted_flag` instead.

---

### **Trigger Special Variables**

Triggers can use special variables to refer to old and new values during the `INSERT`, `UPDATE`, and `DELETE` operations.

| **Variable**   | **Description**                                                    | **Usage Example**                                    |
|----------------|--------------------------------------------------------------------|------------------------------------------------------|
| `:new.column`  | Refers to the new value of a column during an `INSERT` or `UPDATE`. | `:new.salary` – new salary value in an `INSERT` or `UPDATE` |
| `:old.column`  | Refers to the old value of a column during an `UPDATE` or `DELETE`. | `:old.salary` – old salary value in an `UPDATE` or `DELETE` |

---

### **Trigger Firing Order**

- Triggers can be fired in a specific order when multiple triggers are set for the same event. 
- **BEFORE** triggers fire first, followed by **AFTER** triggers. Within each timing type, the order in which they are fired can be controlled using the `FIRE` option.

| **Event Type**   | **Trigger Execution Order**                |
|------------------|--------------------------------------------|
| `BEFORE INSERT`  | All `BEFORE INSERT` triggers are executed before the `INSERT` statement. |
| `AFTER INSERT`   | All `AFTER INSERT` triggers are executed after the `INSERT` statement.  |
| `INSTEAD OF`     | Executes the logic defined in place of the original action. |

---

### **Trigger Limitations**

| **Limitation**                     | **Description**                                                       |
|-------------------------------------|-----------------------------------------------------------------------|
| **Mutating Table Error**           | Triggers cannot modify the table they are triggered by, which would lead to a mutating table error. |
| **Trigger Execution**              | A trigger can only call a procedure or function that does not modify the triggering table. |
| **Performance Impact**             | Triggers, especially those that run on every row, can affect performance. |

---

### **Drop or Disable Triggers**

| **Operation**   | **Syntax**                                                      | **Example**                                                    |
|-----------------|------------------------------------------------------------------|---------------------------------------------------------------|
| **Drop Trigger** | `DROP TRIGGER trigger_name;`                                    | `DROP TRIGGER validate_salary;`                               |
| **Disable Trigger** | `ALTER TRIGGER trigger_name DISABLE;`                          | `ALTER TRIGGER log_salary_change DISABLE;`                    |
| **Enable Trigger**  | `ALTER TRIGGER trigger_name ENABLE;`                           | `ALTER TRIGGER log_salary_change ENABLE;`                     |

---

### **Trigger Summary**

| **Trigger Type**        | **When Triggered**                        | **Example**                                      |
|-------------------------|-------------------------------------------|--------------------------------------------------|
| **BEFORE Trigger**       | Before a DML operation (INSERT, UPDATE, DELETE). | `BEFORE INSERT` trigger to validate data.       |
| **AFTER Trigger**        | After a DML operation.                    | `AFTER UPDATE` trigger to log changes.          |
| **INSTEAD OF Trigger**   | Instead of a DML operation.               | `INSTEAD OF DELETE` trigger to soft-delete.     |

| **Special Variables**   | **Description**                               | **Example Usage**                                      |
|------------------------|---------------------------------------------|--------------------------------------------------------|
| `:new.column`           | Represents new value of the column.         | `:new.salary` for the new salary value in an `INSERT` or `UPDATE` |
| `:old.column`           | Represents old value of the column.         | `:old.salary` for the old salary value in an `UPDATE` or `DELETE` |

---
