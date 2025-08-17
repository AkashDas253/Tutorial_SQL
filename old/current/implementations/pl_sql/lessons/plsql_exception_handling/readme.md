## Exception Handling in PL/SQL

**Exception handling** in PL/SQL is the process of managing runtime errors that occur during the execution of a program. When an error occurs, it is raised as an exception, which can be handled using `EXCEPTION` blocks. PL/SQL provides robust exception handling mechanisms that allow you to capture and respond to errors, ensuring that the program does not terminate abruptly.

---

### **Types of Exceptions**

1. **Predefined Exceptions**: These are standard exceptions that are automatically defined in PL/SQL.
2. **User-Defined Exceptions**: These exceptions are explicitly declared by the programmer to handle custom error conditions.
3. **Others**: General exceptions that are not explicitly named can also be handled.

---

### **Predefined Exceptions**

PL/SQL provides several **predefined exceptions** for common error conditions. Some of the most frequently used ones are:

| **Exception**              | **Description**                                              |
|----------------------------|--------------------------------------------------------------|
| `NO_DATA_FOUND`            | Raised when a `SELECT INTO` query returns no rows.           |
| `TOO_MANY_ROWS`            | Raised when a `SELECT INTO` query returns more than one row. |
| `ZERO_DIVIDE`              | Raised when dividing by zero.                                |
| `DUP_VAL_ON_INDEX`         | Raised when trying to insert duplicate values into a unique index or primary key column. |
| `INVALID_CURSOR`           | Raised when an invalid cursor operation occurs.              |
| `VALUE_ERROR`              | Raised when a numeric or value conversion error occurs.      |
| `TIMEOUT_ON_RESOURCE`      | Raised when a resource request exceeds the allowed timeout period. |
| `LOGIN_DENIED`             | Raised when a login attempt fails due to invalid credentials. |

---

### **User-Defined Exceptions**

You can declare your own exceptions in PL/SQL and raise them in specific conditions using the `RAISE` statement. To define a user-defined exception, you must declare it in the **declaration section** of a block.

#### **Declaring and Raising a User-Defined Exception**

```plsql
DECLARE
  -- Declare a user-defined exception
  my_exception EXCEPTION;

BEGIN
  -- Some logic
  IF some_condition THEN
    -- Raise the user-defined exception
    RAISE my_exception;
  END IF;

EXCEPTION
  WHEN my_exception THEN
    -- Handle the exception
    DBMS_OUTPUT.PUT_LINE('Custom error occurred!');
END;
```

---

### **Exception Handling Block**

The general structure of exception handling in PL/SQL is as follows:

```plsql
BEGIN
  -- Main code block
  -- SQL or PL/SQL operations
EXCEPTION
  WHEN predefined_exception_name THEN
    -- Handle specific exception
  WHEN others THEN
    -- Handle all other exceptions
END;
```

- **BEGIN...END**: Contains the main block of PL/SQL code.
- **EXCEPTION**: Block where exceptions are caught.
- **WHEN exception_name THEN**: Specifies the action to take when a specific exception occurs.
- **WHEN OTHERS THEN**: Catches any exceptions that are not specifically handled.

---

### **Example of Exception Handling**

```plsql
DECLARE
  v_salary NUMBER := 0;
BEGIN
  -- Attempt to divide by zero
  v_salary := 100 / 0;
EXCEPTION
  WHEN ZERO_DIVIDE THEN
    DBMS_OUTPUT.PUT_LINE('Error: Division by zero!');
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('An unexpected error occurred.');
END;
```

In this example:
- The `ZERO_DIVIDE` exception is caught when trying to divide by zero.
- The `OTHERS` exception handler catches all other errors that are not explicitly handled.

---

### **Exception Propagation**

PL/SQL supports **exception propagation**, which means that when an exception is raised in a block, it can be passed to the calling program or block for handling.

- If an exception is raised and not handled within the current block, it propagates to the enclosing block or program.
- You can use **`RAISE`** to re-raise an exception.

#### **Example of Propagating Exceptions**

```plsql
DECLARE
  v_amount NUMBER := 100;
  
  -- Declare user-defined exception
  insufficient_funds EXCEPTION;

  PROCEDURE check_balance IS
  BEGIN
    IF v_amount < 500 THEN
      RAISE insufficient_funds;
    END IF;
  END;
  
BEGIN
  -- Call procedure that may raise exception
  check_balance;
EXCEPTION
  WHEN insufficient_funds THEN
    DBMS_OUTPUT.PUT_LINE('Insufficient funds in account.');
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('An unexpected error occurred.');
END;
```

In this example:
- The exception `insufficient_funds` is raised in the `check_balance` procedure.
- The exception is propagated to the main block where it is caught and handled.

---

### **Handling Multiple Exceptions**

You can handle multiple exceptions in a single block using multiple `WHEN` clauses.

```plsql
DECLARE
  v_salary NUMBER := 1000;
BEGIN
  -- Simulate different error scenarios
  IF v_salary > 1000 THEN
    RAISE VALUE_ERROR;  -- Raise value error for salary greater than 1000
  END IF;
EXCEPTION
  WHEN VALUE_ERROR THEN
    DBMS_OUTPUT.PUT_LINE('Salary value error!');
  WHEN TOO_MANY_ROWS THEN
    DBMS_OUTPUT.PUT_LINE('Too many rows returned.');
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('An unknown error occurred.');
END;
```

---

### **Logging Exceptions**

PL/SQL allows you to log exceptions for troubleshooting. You can use the `DBMS_OUTPUT.PUT_LINE` to display error messages, or you can use the `DBMS_LOGGING` package to write error details to a log table.

```plsql
BEGIN
  -- Simulate an error
  RAISE VALUE_ERROR;
EXCEPTION
  WHEN VALUE_ERROR THEN
    DBMS_OUTPUT.PUT_LINE('Error: Value error occurred.');
    -- Optionally log to a table
    INSERT INTO error_log (error_message, timestamp)
    VALUES ('Value error occurred', SYSDATE);
END;
```

---

### **Raising Exceptions Explicitly**

You can raise both predefined and user-defined exceptions explicitly using the `RAISE` statement.

```plsql
DECLARE
  v_salary NUMBER := -1000;
  salary_error EXCEPTION;
BEGIN
  IF v_salary < 0 THEN
    RAISE salary_error;  -- Raise user-defined exception
  END IF;
EXCEPTION
  WHEN salary_error THEN
    DBMS_OUTPUT.PUT_LINE('Salary cannot be negative.');
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('An unknown error occurred.');
END;
```

---

### **Exception Handling Best Practices**

- **Handle specific exceptions first**: Catch the most specific exceptions before more general ones.
- **Use `WHEN OTHERS` cautiously**: This can catch all errors, but it is generally best practice to log or raise the exception for further investigation.
- **Use `RAISE` for custom error handling**: Custom exceptions allow you to enforce business logic in your applications.
- **Log exceptions**: Keep a log of exceptions to monitor and troubleshoot errors efficiently.

---

### **Summary of Syntax**

| **Statement**      | **Description**                                                     |
|--------------------|---------------------------------------------------------------------|
| `EXCEPTION`        | The keyword that begins the exception handling section.             |
| `WHEN exception`   | Specifies the exception and the corresponding handler.              |
| `RAISE`            | Used to raise an exception, either predefined or user-defined.      |
| `WHEN OTHERS`      | Catches any exception that has not been explicitly handled.         |

---

### **Summary**

- **PL/SQL exception handling** ensures your programs can gracefully handle runtime errors.
- **Predefined exceptions** are automatically raised by PL/SQL for common errors.
- **User-defined exceptions** allow you to raise and handle custom error conditions.
- The **EXCEPTION block** captures errors, with `WHEN` clauses to handle specific exceptions.
- **Exception propagation** allows errors to be passed up to the calling program or block for handling.
- Use **`RAISE`** to re-raise exceptions or raise custom ones.
- Exception handling promotes **reliability** and **resilience** in database applications.
