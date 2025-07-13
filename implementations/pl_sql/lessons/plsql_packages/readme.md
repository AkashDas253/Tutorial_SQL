## Packages in PL/SQL

A **package** in PL/SQL is a collection of related procedures, functions, variables, and other PL/SQL constructs grouped together to provide a modular approach to managing database logic. Packages help organize and encapsulate code, improve reusability, and enhance performance by reducing the number of calls to the database.

---

### **Structure of a Package**

A package is divided into two parts:

1. **Package Specification**: This is the interface to the package, containing the declaration of all public elements like procedures, functions, types, constants, and variables. It defines what is accessible from outside the package.
   
2. **Package Body**: This contains the implementation of the procedures and functions defined in the package specification. It includes the actual code that runs when these elements are invoked.

---

### **Package Specification Syntax**

```plsql
CREATE OR REPLACE PACKAGE package_name IS
  -- Declarations of public variables, types, constants
  -- Declarations of public procedures and functions
END package_name;
```

- **package_name**: The name of the package.
- The package specification contains all the declarations, but no executable code.

---

### **Package Body Syntax**

```plsql
CREATE OR REPLACE PACKAGE BODY package_name IS
  -- Implementations of the procedures and functions
END package_name;
```

- **package_name**: The name of the package body (same as the package specification).
- The package body contains the code for the procedures and functions defined in the specification.

---

### **Example of a Package**

#### **Package Specification**

```plsql
CREATE OR REPLACE PACKAGE emp_pkg IS
  -- Declaration of a constant
  c_tax_rate CONSTANT NUMBER := 0.1;

  -- Declaration of a procedure
  PROCEDURE add_employee(p_emp_id IN NUMBER, p_name IN VARCHAR2, p_salary IN NUMBER);
  
  -- Declaration of a function
  FUNCTION calculate_annual_salary(p_monthly_salary IN NUMBER) RETURN NUMBER;
  
END emp_pkg;
```

- **`c_tax_rate`** is a constant defined within the package.
- **`add_employee`** is a procedure to insert an employee.
- **`calculate_annual_salary`** is a function that calculates the annual salary.

#### **Package Body**

```plsql
CREATE OR REPLACE PACKAGE BODY emp_pkg IS
  -- Implementation of the add_employee procedure
  PROCEDURE add_employee(p_emp_id IN NUMBER, p_name IN VARCHAR2, p_salary IN NUMBER) IS
  BEGIN
    INSERT INTO employees (employee_id, employee_name, salary)
    VALUES (p_emp_id, p_name, p_salary);
  END add_employee;

  -- Implementation of the calculate_annual_salary function
  FUNCTION calculate_annual_salary(p_monthly_salary IN NUMBER) RETURN NUMBER IS
  BEGIN
    RETURN p_monthly_salary * 12;
  END calculate_annual_salary;

END emp_pkg;
```

- **`add_employee`**: Inserts an employee into the `employees` table.
- **`calculate_annual_salary`**: Returns the annual salary based on the monthly salary.

---

### **Using a Package**

After defining the package, its procedures and functions can be invoked just like any standalone procedure or function.

#### **Calling a Procedure from a Package**

```plsql
BEGIN
  emp_pkg.add_employee(1001, 'John Doe', 5000);
END;
```

#### **Calling a Function from a Package**

```sql
SELECT emp_pkg.calculate_annual_salary(salary) AS annual_salary
FROM employees;
```

---

### **Advantages of Using Packages**

1. **Modularization**: Packages allow developers to group related procedures and functions together, making the code more organized and manageable.
   
2. **Encapsulation**: Packages hide the implementation details. The package specification serves as an interface, while the body contains the details.
   
3. **Performance**: PL/SQL packages are loaded into memory once and remain in memory for the duration of the session. This reduces the need for recompilation, improving performance.

4. **Code Reusability**: Once defined, procedures and functions within a package can be reused across multiple programs.

5. **Security**: The package specification exposes only the necessary elements, ensuring sensitive code within the body is not exposed to the user.

---

### **Package Variables**

Variables declared in the package specification are global to the package and can be used across all procedures and functions within the package.

#### **Example: Package with Global Variables**

```plsql
CREATE OR REPLACE PACKAGE global_pkg IS
  -- Global variable
  g_employee_count NUMBER := 0;
  
  -- Procedure to increment employee count
  PROCEDURE increment_employee_count;
END global_pkg;
```

```plsql
CREATE OR REPLACE PACKAGE BODY global_pkg IS
  PROCEDURE increment_employee_count IS
  BEGIN
    g_employee_count := g_employee_count + 1;
  END increment_employee_count;
END global_pkg;
```

- **`g_employee_count`** is a global variable that is accessible throughout the package and is incremented each time the procedure is called.

---

### **Package Overloading**

In PL/SQL, you can overload procedures and functions within a package. This means defining multiple procedures or functions with the same name but different parameter lists.

#### **Example: Overloaded Functions**

```plsql
CREATE OR REPLACE PACKAGE emp_pkg IS
  FUNCTION calculate_salary(p_monthly_salary IN NUMBER) RETURN NUMBER;
  FUNCTION calculate_salary(p_hourly_rate IN NUMBER, p_hours_worked IN NUMBER) RETURN NUMBER;
END emp_pkg;
```

```plsql
CREATE OR REPLACE PACKAGE BODY emp_pkg IS
  FUNCTION calculate_salary(p_monthly_salary IN NUMBER) RETURN NUMBER IS
  BEGIN
    RETURN p_monthly_salary * 12;
  END calculate_salary;

  FUNCTION calculate_salary(p_hourly_rate IN NUMBER, p_hours_worked IN NUMBER) RETURN NUMBER IS
  BEGIN
    RETURN p_hourly_rate * p_hours_worked * 12;
  END calculate_salary;
END emp_pkg;
```

- There are two `calculate_salary` functions: one that calculates salary based on a monthly salary and one based on an hourly rate and hours worked.

---

### **Dynamic SQL in Packages**

You can use dynamic SQL within a package by utilizing the `EXECUTE IMMEDIATE` statement, allowing you to execute SQL queries dynamically.

#### **Example: Using Dynamic SQL in a Package**

```plsql
CREATE OR REPLACE PACKAGE emp_pkg IS
  PROCEDURE execute_dynamic_query(p_query IN VARCHAR2);
END emp_pkg;
```

```plsql
CREATE OR REPLACE PACKAGE BODY emp_pkg IS
  PROCEDURE execute_dynamic_query(p_query IN VARCHAR2) IS
  BEGIN
    EXECUTE IMMEDIATE p_query;
  END execute_dynamic_query;
END emp_pkg;
```

- **`execute_dynamic_query`** executes a SQL query that is passed as a parameter.

---

### **Package vs Procedure/Function**

| **Aspect**               | **Package**                                                     | **Procedure/Function**                                           |
|--------------------------|-----------------------------------------------------------------|------------------------------------------------------------------|
| **Structure**            | Consists of a specification and a body.                         | A single block of code (procedure) or a function with a return value. |
| **Modularity**           | Helps group related procedures, functions, and variables together. | A single operation or calculation, without grouping.             |
| **Performance**          | Loaded once per session, enhancing performance.                 | Compiled every time it is executed.                             |
| **Usage**                | Can contain multiple procedures, functions, variables, etc.     | A specific action (procedure) or calculation (function).         |

---

### **Dropping a Package**

To remove a package from the database, you can use the `DROP PACKAGE` statement.

```sql
DROP PACKAGE emp_pkg;
```

This will remove both the package specification and body from the database.

---

### **Summary**

- **Packages** are used to group related procedures, functions, and variables.
- They consist of two parts: **Specification** (interface) and **Body** (implementation).
- Packages provide **modularization**, **encapsulation**, **performance improvements**, and **security**.
- **Package variables** are globally accessible within the package.
- **Package overloading** allows defining multiple procedures or functions with the same name but different parameters.
- **Dynamic SQL** can be used within packages to execute SQL queries dynamically.
