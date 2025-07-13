## Procedures and Functions in PL/SQL

PL/SQL procedures and functions are two types of stored program units in Oracle databases that allow for modular code development. Both can be stored and executed in the database, but they differ in purpose and how they are called.

### **Differences Between Procedures and Functions**

| **Aspect**           | **Procedure**                                                    | **Function**                                                       |
|----------------------|-------------------------------------------------------------------|--------------------------------------------------------------------|
| **Return Type**      | Does not return a value.                                           | Must return a value (usually using the `RETURN` keyword).           |
| **Purpose**          | Designed to perform an action or a series of actions.             | Designed to calculate and return a value.                          |
| **Invocation**       | Called by a `CALL` statement or within another program unit.      | Called as part of an expression (e.g., in SQL statements, `SELECT` queries). |
| **Use Case**         | Suitable for operations like data modification or complex logic. | Suitable for operations that return values like calculations or data transformations. |

---

### **Procedure Structure**

A procedure is a PL/SQL block that can accept input parameters and perform tasks like modifying database tables, performing calculations, or sending data to other systems. 

#### **Syntax for Creating a Procedure**

```plsql
CREATE [OR REPLACE] PROCEDURE procedure_name
  [parameter_name datatype [IN | OUT | IN OUT], ...]
IS
BEGIN
  -- PL/SQL statements to execute
END procedure_name;
```

- **parameter_name**: Name of the input/output parameter.
- **datatype**: The data type of the parameter (e.g., `NUMBER`, `VARCHAR2`).
- **IN**: The default parameter mode; the value of the parameter cannot be modified.
- **OUT**: The parameter is used to return a value.
- **IN OUT**: The parameter can both accept and return a value.

---

### **Example of a Procedure**

This example demonstrates how to create a procedure to add a new employee to the `employees` table.

```plsql
CREATE OR REPLACE PROCEDURE add_employee(
    p_employee_id IN NUMBER,
    p_first_name IN VARCHAR2,
    p_last_name IN VARCHAR2,
    p_salary IN NUMBER)
IS
BEGIN
    INSERT INTO employees (employee_id, first_name, last_name, salary)
    VALUES (p_employee_id, p_first_name, p_last_name, p_salary);
    COMMIT;
END add_employee;
```

- **`p_employee_id`, `p_first_name`, `p_last_name`, `p_salary`** are input parameters that are used in the `INSERT` statement.
- **`COMMIT`** ensures the changes are saved to the database.

---

### **Function Structure**

A function is similar to a procedure but is designed to return a value. Functions are often used for calculations or data transformations and can be called from SQL queries.

#### **Syntax for Creating a Function**

```plsql
CREATE [OR REPLACE] FUNCTION function_name
  (parameter_name datatype [IN | OUT | IN OUT], ...)
  RETURN return_type
IS
BEGIN
  -- PL/SQL statements to execute
  RETURN value;  -- The function must return a value
END function_name;
```

- **parameter_name**: Name of the input/output parameter.
- **datatype**: The data type of the parameter.
- **return_type**: The data type of the value that the function will return.

---

### **Example of a Function**

The following example shows a function that calculates the annual salary based on a monthly salary.

```plsql
CREATE OR REPLACE FUNCTION calculate_annual_salary(
    p_monthly_salary IN NUMBER)
  RETURN NUMBER
IS
BEGIN
    RETURN p_monthly_salary * 12;
END calculate_annual_salary;
```

- **`p_monthly_salary`** is the input parameter.
- The function returns the calculated annual salary (monthly salary * 12).

#### **Calling a Function in SQL**

You can use the function in a `SELECT` statement to calculate the annual salary for an employee:

```sql
SELECT employee_id, calculate_annual_salary(salary) AS annual_salary
FROM employees;
```

---

### **Procedures vs Functions: Use Cases**

| **Use Case**                                  | **Procedure**                                             | **Function**                                               |
|-----------------------------------------------|-----------------------------------------------------------|------------------------------------------------------------|
| **Performing DML operations**                 | Ideal for inserting, updating, or deleting data.          | Cannot perform DML directly (used within SQL statements).    |
| **Returning a value**                         | Not designed to return a value.                           | Returns a single value, often used for calculations.        |
| **Modularizing complex logic**                | Suitable for code that involves multiple steps or processes. | Ideal for isolated computations or data transformations.   |
| **Reusability in SQL**                        | Cannot be called in SQL statements directly.              | Can be called within SQL queries (e.g., `SELECT` statements). |

---

### **Procedure and Function Parameters**

| **Parameter Mode**  | **Description**                                                    | **Example**                                  |
|---------------------|--------------------------------------------------------------------|----------------------------------------------|
| **IN**              | Default mode, accepts input values but does not return a value.    | `p_salary IN NUMBER`                        |
| **OUT**             | Used to return a value from the procedure or function.             | `p_total OUT NUMBER`                        |
| **IN OUT**          | Used to both pass a value to and return a value from the procedure or function. | `p_discount IN OUT NUMBER`                |

---

### **Calling Procedures and Functions**

1. **Calling a Procedure**

   A procedure can be invoked using an anonymous PL/SQL block, or from another procedure or function.

   ```plsql
   BEGIN
     add_employee(1001, 'John', 'Doe', 5000);
   END;
   ```

2. **Calling a Function**

   A function can be called in PL/SQL code or SQL queries.

   **In SQL:**
   ```sql
   SELECT calculate_annual_salary(salary) 
   FROM employees;
   ```

   **In PL/SQL:**
   ```plsql
   DECLARE
     annual_salary NUMBER;
   BEGIN
     annual_salary := calculate_annual_salary(5000);
     DBMS_OUTPUT.PUT_LINE('Annual Salary: ' || annual_salary);
   END;
   ```

---

### **Handling Exceptions in Procedures and Functions**

You can handle exceptions in both procedures and functions using the `EXCEPTION` block.

#### **Syntax for Handling Exceptions**

```plsql
BEGIN
  -- Code to execute
EXCEPTION
  WHEN exception_name THEN
    -- Exception handling code
  WHEN OTHERS THEN
    -- Handle any other exceptions
END;
```

#### **Example: Exception Handling in a Procedure**

```plsql
CREATE OR REPLACE PROCEDURE add_employee(
    p_employee_id IN NUMBER,
    p_first_name IN VARCHAR2,
    p_last_name IN VARCHAR2,
    p_salary IN NUMBER)
IS
BEGIN
    INSERT INTO employees (employee_id, first_name, last_name, salary)
    VALUES (p_employee_id, p_first_name, p_last_name, p_salary);
    COMMIT;
EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('Error: Duplicate employee ID.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred.');
END add_employee;
```

---

### **Dropping Procedures and Functions**

To remove a procedure or function, use the `DROP` statement.

| **Operation**   | **Syntax**                          | **Example**                               |
|-----------------|-------------------------------------|-------------------------------------------|
| **Drop Procedure** | `DROP PROCEDURE procedure_name;`    | `DROP PROCEDURE add_employee;`            |
| **Drop Function** | `DROP FUNCTION function_name;`      | `DROP FUNCTION calculate_annual_salary;`  |

---

### **Summary of Procedures and Functions**

| **Aspect**           | **Procedure**                                                    | **Function**                                                       |
|----------------------|-------------------------------------------------------------------|--------------------------------------------------------------------|
| **Return Type**      | No return value.                                                   | Must return a value.                                               |
| **Invocation**       | Invoked via `CALL` or within another PL/SQL block.                | Invoked within an expression (e.g., `SELECT` statement).           |
| **Use Case**         | Performs actions (e.g., modifying database).                      | Performs calculations or transformations.                          |
| **Parameters**       | Accepts `IN`, `OUT`, or `IN OUT` parameters.                      | Accepts `IN`, `OUT`, or `IN OUT` parameters.                       |
