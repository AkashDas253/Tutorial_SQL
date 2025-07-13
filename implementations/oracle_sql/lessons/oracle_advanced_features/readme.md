## Oracle Advanced Features

### 1. **PL/SQL Integration**

PL/SQL is Oracle's procedural extension to SQL, allowing you to combine SQL with procedural constructs like loops, conditions, and exceptions.

#### 1.1 **Anonymous Blocks**
An anonymous block is a PL/SQL program that does not have a name and is typically used for one-time operations or simple tasks.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Executes a PL/SQL block without storing it                     | `BEGIN ... END;`                                                |

#### Example:
```sql
BEGIN
   DBMS_OUTPUT.PUT_LINE('Hello, World!');
END;
```

#### 1.2 **Stored Procedures**
A stored procedure is a named PL/SQL block that performs a specific action and can be reused.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | A procedure is a set of SQL statements stored in the database | `CREATE PROCEDURE procedure_name AS BEGIN ... END;`            |

#### Example:
```sql
CREATE PROCEDURE greet_user AS
BEGIN
   DBMS_OUTPUT.PUT_LINE('Hello, User!');
END;
```

#### 1.3 **Functions**
A function is similar to a procedure but returns a value. It can be called in SQL queries or other PL/SQL blocks.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | A function returns a value after performing an operation      | `CREATE FUNCTION function_name RETURN data_type AS BEGIN ... END;` |

#### Example:
```sql
CREATE FUNCTION get_employee_name (emp_id NUMBER) RETURN VARCHAR2 AS
   emp_name VARCHAR2(50);
BEGIN
   SELECT name INTO emp_name FROM employees WHERE id = emp_id;
   RETURN emp_name;
END;
```

#### 1.4 **Triggers**
A trigger is a PL/SQL block that is automatically executed in response to certain events (e.g., insert, update, delete) on a specified table or view.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Executes automatically when a specified event occurs         | `CREATE TRIGGER trigger_name BEFORE/AFTER INSERT ON table_name FOR EACH ROW BEGIN ... END;` |

#### Example:
```sql
CREATE TRIGGER update_salary
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
   DBMS_OUTPUT.PUT_LINE('Salary updated for employee ' || :OLD.id);
END;
```

#### 1.5 **Packages**
A package is a collection of related procedures, functions, variables, and cursors. It allows better organization of PL/SQL code.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Organizes related PL/SQL components                           | `CREATE PACKAGE package_name AS ... END;`                      |

#### Example:
```sql
CREATE PACKAGE emp_package AS
   PROCEDURE update_salary (emp_id NUMBER, new_salary NUMBER);
END emp_package;
```

---

### 2. **Advanced Query Features**

#### 2.1 **Hierarchical Queries (`CONNECT BY`)**
Hierarchical queries allow you to query data in a tree-like structure, such as organizational charts.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Retrieves hierarchical data using `CONNECT BY` clause        | `SELECT column FROM table START WITH condition CONNECT BY condition;` |

#### Example:
```sql
SELECT employee_id, manager_id, name
FROM employees
START WITH manager_id IS NULL
CONNECT BY PRIOR employee_id = manager_id;
```

#### 2.2 **Pivot and Unpivot Queries**
Pivoting transforms rows into columns, while unpivoting turns columns into rows.

| **Operation**           | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Pivot**               | Converts rows into columns based on aggregation              | `SELECT * FROM (SELECT column1, column2 FROM table) PIVOT (aggregation(column2) FOR column1 IN (value1, value2));` |
| **Unpivot**             | Converts columns into rows                                    | `SELECT * FROM (SELECT column1, column2, column3 FROM table) UNPIVOT (value FOR column IN (column1, column2));` |

#### Example:
```sql
SELECT * FROM 
(SELECT employee_id, department_id, salary FROM employees) 
PIVOT (SUM(salary) FOR department_id IN (10, 20, 30));
```

#### Example (Unpivot):
```sql
SELECT * FROM 
(SELECT employee_id, department_1, department_2 FROM employees) 
UNPIVOT (salary FOR department IN (department_1, department_2));
```

#### 2.3 **JSON Functions (`JSON_OBJECT`, `JSON_TABLE`)**
Oracle provides functions to work with JSON data, allowing you to parse and query JSON objects.

| **Function**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **`JSON_OBJECT`**       | Converts data to a JSON object                                | `SELECT JSON_OBJECT('name' VALUE name, 'salary' VALUE salary) FROM employees;` |
| **`JSON_TABLE`**        | Converts JSON data into relational tables                     | `SELECT * FROM JSON_TABLE(json_column, '$.employees[*]' COLUMNS (name VARCHAR2(100) PATH '$.name')) AS jt;` |

#### Example (`JSON_OBJECT`):
```sql
SELECT JSON_OBJECT('id' VALUE employee_id, 'name' VALUE name) AS employee_json
FROM employees;
```

#### Example (`JSON_TABLE`):
```sql
SELECT * FROM JSON_TABLE(
    '{"employees":[{"name":"John","salary":5000},{"name":"Doe","salary":6000}]}',
    '$.employees[*]' COLUMNS (name VARCHAR2(100) PATH '$.name', salary NUMBER PATH '$.salary')
) AS jt;
```

---

### 3. **Database Links**

#### 3.1 **Creating Database Links**
A database link is used to connect one Oracle database to another. This allows querying data from a remote database.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Allows querying remote databases using a link                 | `CREATE DATABASE LINK link_name CONNECT TO username IDENTIFIED BY password USING 'tns_service_name';` |

#### Example:
```sql
CREATE DATABASE LINK remote_db CONNECT TO remote_user IDENTIFIED BY password USING 'remote_tns';
```

#### 3.2 **Querying Remote Databases**
Once a database link is created, you can query a remote database as if it were local.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Queries data from a remote database via a database link       | `SELECT * FROM remote_table@link_name;`                        |

#### Example:
```sql
SELECT * FROM employees@remote_db;
```

---

### 4. **User-Defined Data Types**

#### 4.1 **Object Types**
Object types in Oracle SQL allow you to define custom data types that model real-world objects.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Defines a custom object with attributes and methods           | `CREATE TYPE object_type_name AS OBJECT (attribute_name data_type, ...);` |

#### Example:
```sql
CREATE TYPE employee_type AS OBJECT (
   id NUMBER,
   name VARCHAR2(100),
   salary NUMBER
);
```

#### 4.2 **Collections (`VARRAY`, Nested Tables)**

Collections allow you to store multiple values of the same type in a single variable.

| **Type**                | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **VARRAY**              | A variable-size array of elements                            | `CREATE TYPE array_type AS VARRAY(10) OF VARCHAR2(100);`       |
| **Nested Tables**       | A table-like collection that can store an unlimited number of elements | `CREATE TYPE nested_table_type AS TABLE OF VARCHAR2(100);`    |

#### Example (`VARRAY`):
```sql
CREATE TYPE phone_numbers AS VARRAY(5) OF VARCHAR2(15);
```

#### Example (Nested Table):
```sql
CREATE TYPE employees_table AS TABLE OF VARCHAR2(100);
```

---