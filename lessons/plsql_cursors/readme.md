## Cursors in PL/SQL

Cursors are used in PL/SQL to handle the results of queries. A cursor is a pointer to a private SQL area that stores the results of a query. Cursors allow row-by-row processing of query results, which is useful when handling large result sets or when performing operations on individual rows.

There are two types of cursors in PL/SQL: **Implicit Cursors** and **Explicit Cursors**.

---

### **Implicit Cursors**

Implicit cursors are automatically created by PL/SQL for SQL statements that return a single result set (like `SELECT INTO`, `INSERT`, `UPDATE`, or `DELETE`). You do not need to declare or manage them explicitly.

| **Operation**                | **Description**                                            | **Example**                                      |
|------------------------------|------------------------------------------------------------|--------------------------------------------------|
| **SELECT INTO**               | Used for retrieving a single row into PL/SQL variables.    | ```SELECT first_name, last_name INTO v_first_name, v_last_name FROM employees WHERE employee_id = 101;``` |
| **INSERT/UPDATE/DELETE**      | Automatically handled by PL/SQL for single-row operations. | ```UPDATE employees SET salary = 5000 WHERE employee_id = 101;``` |
| **Attribute**                 | Implicit cursor attributes like `SQL%FOUND`, `SQL%NOTFOUND`, `SQL%ROWCOUNT`, `SQL%ISOPEN`. | ```IF SQL%FOUND THEN DBMS_OUTPUT.PUT_LINE('Row updated'); END IF;``` |

#### **Implicit Cursor Attributes**

| **Attribute**       | **Description**                                           | **Usage**                                                           |
|---------------------|-----------------------------------------------------------|---------------------------------------------------------------------|
| `SQL%FOUND`         | Returns `TRUE` if the query affected one or more rows.    | `IF SQL%FOUND THEN ...`                                             |
| `SQL%NOTFOUND`      | Returns `TRUE` if the query did not affect any rows.      | `IF SQL%NOTFOUND THEN ...`                                          |
| `SQL%ROWCOUNT`      | Returns the number of rows affected by the last SQL statement. | `DBMS_OUTPUT.PUT_LINE(SQL%ROWCOUNT);`                               |
| `SQL%ISOPEN`        | Returns `TRUE` if the cursor is open (not applicable to implicit cursors). | N/A (not used in implicit cursors)                                   |

---

### **Explicit Cursors**

Explicit cursors are defined by the programmer and are used when dealing with queries that return multiple rows. They give more control over fetching rows and closing the cursor.

#### **Syntax for Declaring an Explicit Cursor**

| **Syntax**                                                    | **Description**                                              |
|---------------------------------------------------------------|--------------------------------------------------------------|
| `CURSOR cursor_name IS <query>;`                               | Declares an explicit cursor that holds the result of a query. |
| **Example**                                                   | ```CURSOR emp_cursor IS SELECT first_name, last_name FROM employees WHERE department_id = 10;``` |

#### **Opening and Fetching from an Explicit Cursor**

| **Operation**         | **Syntax**                                                  | **Description**                                                        |
|-----------------------|-------------------------------------------------------------|------------------------------------------------------------------------|
| **OPEN**              | `OPEN cursor_name;`                                          | Initializes the cursor and prepares it for use.                        |
| **FETCH**             | `FETCH cursor_name INTO variable1, variable2;`              | Retrieves one row at a time from the cursor and stores it in variables. |
| **CLOSE**             | `CLOSE cursor_name;`                                         | Releases the resources allocated for the cursor.                       |



| **Example** | 
|-------------|
| ``` OPEN emp_cursor; ``` |
| ``` FETCH emp_cursor INTO v_first_name, v_last_name; ``` |
| ``` CLOSE emp_cursor; ``` |

---

#### **Example: Using an Explicit Cursor**

```plsql
DECLARE
   CURSOR emp_cursor IS 
      SELECT first_name, last_name 
      FROM employees
      WHERE department_id = 10;
   
   v_first_name employees.first_name%TYPE;
   v_last_name employees.last_name%TYPE;
BEGIN
   OPEN emp_cursor;
   
   LOOP
      FETCH emp_cursor INTO v_first_name, v_last_name;
      EXIT WHEN emp_cursor%NOTFOUND;
      
      DBMS_OUTPUT.PUT_LINE('Employee: ' || v_first_name || ' ' || v_last_name);
   END LOOP;
   
   CLOSE emp_cursor;
END;
```

---

### **Cursor Attributes**

Cursor attributes are used to check the status of the cursor and to fetch additional information about the execution.

| **Attribute**         | **Description**                                             | **Usage**                                                            |
|-----------------------|-------------------------------------------------------------|----------------------------------------------------------------------|
| `cursor_name%ISOPEN`  | Returns `TRUE` if the cursor is open.                       | `IF emp_cursor%ISOPEN THEN ...`                                      |
| `cursor_name%FOUND`   | Returns `TRUE` if the last `FETCH` returned a row.          | `IF emp_cursor%FOUND THEN ...`                                       |
| `cursor_name%NOTFOUND`| Returns `TRUE` if the last `FETCH` did not return any rows. | `IF emp_cursor%NOTFOUND THEN ...`                                    |
| `cursor_name%ROWCOUNT`| Returns the number of rows fetched so far.                  | `DBMS_OUTPUT.PUT_LINE(emp_cursor%ROWCOUNT);`                         |

---

### **Cursor FOR Loop**

A **Cursor FOR Loop** is a shorthand for opening, fetching, and closing an explicit cursor. The loop automatically handles cursor management and simplifies the code.

| **Syntax**                                                   | **Description**                                                                                   |
|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| `FOR record IN cursor_name LOOP`<br> `statements;`<br> `END LOOP;` | Implicitly declares, opens, fetches, and closes the cursor. It iterates over each row in the result set. |



**Example**     
|
``` FOR emp_record IN emp_cursor LOOP<br> DBMS_OUTPUT.PUT_LINE(emp_record.first_name || ' ' || emp_record.last_name);<br> END LOOP;``` 

---

### **Summary of Cursor Operations**

| **Cursor Type**   | **Description**                                    | **Syntax Example**                                                                                   |
|-------------------|----------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Implicit Cursor** | Automatically created for single SQL statements.    | `SELECT INTO v_first_name, v_last_name FROM employees WHERE employee_id = 101;`                       |
| **Explicit Cursor** | Declared explicitly by the user for multi-row queries. | `CURSOR emp_cursor IS SELECT first_name, last_name FROM employees WHERE department_id = 10;`         |
| **Cursor FOR Loop** | Simplified version of cursor usage that handles opening, fetching, and closing automatically. | `FOR emp_record IN emp_cursor LOOP DBMS_OUTPUT.PUT_LINE(emp_record.first_name); END LOOP;`           |
| **Cursor Attributes** | Used to check the state of the cursor.           | `IF emp_cursor%FOUND THEN ...`                                                                       |

---
