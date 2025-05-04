## PL/SQL Block Structure  

PL/SQL programs are organized into logical blocks that form the foundation of PL/SQL. A block consists of three main sections: **Declaration**, **Execution**, and **Exception Handling**. Each block may be anonymous or named and can be nested within other blocks.  

---

### Structure of a PL/SQL Block  

| **Section**          | **Purpose**                                                                 | **Optional/Required**         |
|-----------------------|-----------------------------------------------------------------------------|--------------------------------|
| **Declaration Section** | Declares variables, constants, cursors, and other data structures used in the block. | Optional                      |
| **Execution Section**   | Contains the main logic and SQL statements to manipulate data.            | Required                      |
| **Exception Handling Section** | Handles runtime errors and exceptions during execution.              | Optional                      |

---

### Syntax of a PL/SQL Block  

```sql
DECLARE
   -- Declaration Section: Define variables, constants, cursors, etc.
   variable_name datatype;
   constant_name CONSTANT datatype := value;
BEGIN
   -- Execution Section: Write the logic and SQL operations.
   statement_1;
   statement_2;
EXCEPTION
   -- Exception Handling Section: Handle runtime errors.
   WHEN exception_name THEN
      statement_3;
END;
```

---

### Detailed Breakdown  

#### **Declaration Section**  
- **Purpose**: Define data structures to be used in the block.  
- **Components**:  
  - Variables  
  - Constants  
  - Cursors  
  - User-defined types  

| **Declaration Type** | **Syntax**                               | **Example**                              |
|-----------------------|-------------------------------------------|------------------------------------------|
| **Variable**          | `variable_name datatype;`                | `v_salary NUMBER(8,2);`                 |
| **Constant**          | `constant_name CONSTANT datatype := value;` | `c_bonus CONSTANT NUMBER := 1000;`      |
| **Cursor**            | `CURSOR cursor_name IS query;`           | `CURSOR emp_cursor IS SELECT * FROM employees;` |

---

#### **Execution Section**  
- **Purpose**: Execute SQL statements and procedural logic.  
- **Features**:  
  - SQL Operations (`SELECT`, `INSERT`, `UPDATE`, `DELETE`)  
  - Procedural Constructs (`IF`, `LOOP`, `CASE`)  
  - Calling Procedures and Functions  

| **Statement Type**    | **Example**                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **SQL Operation**      | `SELECT salary INTO v_salary FROM employees WHERE employee_id = 101;`      |
| **Conditional Logic**  | `IF v_salary > 5000 THEN v_bonus := v_salary * 0.10; END IF;`              |
| **Looping Constructs** | `FOR i IN 1..10 LOOP DBMS_OUTPUT.PUT_LINE(i); END LOOP;`                   |

---

#### **Exception Handling Section**  
- **Purpose**: Handle runtime errors gracefully to ensure smooth execution.  
- **Types of Exceptions**:  
  - Predefined Exceptions (e.g., `NO_DATA_FOUND`, `TOO_MANY_ROWS`)  
  - User-Defined Exceptions  

| **Exception Type**      | **Syntax**                                   | **Example**                      |
|--------------------------|---------------------------------------------|-----------------------------------|
| **Predefined Exception** | `WHEN exception_name THEN statement;`       | `WHEN NO_DATA_FOUND THEN ...`    |
| **User-Defined Exception**| Declare an exception and use `RAISE` statement. | `EXCEPTION my_error; ... RAISE my_error;` |

---

### Example of a Complete PL/SQL Block  

```sql
DECLARE
   v_salary NUMBER(8,2);
   v_bonus NUMBER(8,2);
BEGIN
   -- Fetch the salary of an employee
   SELECT salary INTO v_salary FROM employees WHERE employee_id = 101;
   
   -- Calculate bonus
   IF v_salary > 5000 THEN
      v_bonus := v_salary * 0.10;
   ELSE
      v_bonus := 500;
   END IF;
   
   -- Output the result
   DBMS_OUTPUT.PUT_LINE('Bonus: ' || v_bonus);
EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('Employee not found.');
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END;
```

---

### Key Points  

- **Nesting**: PL/SQL blocks can be nested within one another.  
- **Flexibility**: Declaration and Exception Handling sections are optional, but the Execution section is mandatory.  
- **Scope**: Variables declared in the Declaration section are local to the block unless passed explicitly.  
