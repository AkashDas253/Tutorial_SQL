## Data Types in PL/SQL  

PL/SQL supports various data types, enabling you to work with scalar, composite, reference, and LOB data types. These types allow you to handle different kinds of data, ranging from simple numbers to complex collections.

---

### **Scalar Data Types**

Scalar data types store single values. These types are used to hold fundamental data, such as numbers, characters, and dates.

| **Data Type**    | **Description**                                          | **Example**                            |
|-------------------|----------------------------------------------------------|----------------------------------------|
| **NUMBER**        | Stores numeric values, including integers and decimals.  | `v_salary NUMBER(8,2);`                |
| **CHAR**          | Fixed-length character data (up to 2000 bytes).         | `v_name CHAR(10);`                     |
| **VARCHAR2**      | Variable-length character data (up to 4000 bytes).      | `v_address VARCHAR2(100);`             |
| **DATE**          | Stores date and time values (accurate to seconds).       | `v_hire_date DATE;`                    |
| **BOOLEAN**       | Stores `TRUE`, `FALSE`, or `NULL`.                       | `v_active BOOLEAN := TRUE;`            |

#### Example Usage  
```sql
DECLARE
   v_age NUMBER;
   v_is_active BOOLEAN;
BEGIN
   v_age := 30;
   v_is_active := TRUE;
END;
```

---

### **Composite Data Types**

Composite data types allow you to group multiple values into a single unit. These types include **Records**, **Associative Arrays**, **Nested Tables**, and **VARRAYs**.

| **Data Type**          | **Description**                                                                 | **Example**                                             |
|------------------------|---------------------------------------------------------------------------------|---------------------------------------------------------|
| **Record**             | A collection of different types of data grouped together as one unit.            | `TYPE emp_record IS RECORD (id NUMBER, name VARCHAR2(100));` |
| **Associative Array**  | An array-like structure, indexed by integers or strings.                        | `TYPE emp_array IS TABLE OF employees%ROWTYPE INDEX BY BINARY_INTEGER;` |
| **Nested Table**       | A table-like structure that can store an arbitrary number of elements.          | `TYPE dept_table IS TABLE OF department%ROWTYPE;`         |
| **VARRAY**             | A fixed-size array to store multiple elements of the same data type.            | `TYPE emp_varray IS VARRAY(5) OF NUMBER;`                |

#### Example Usage  
```sql
DECLARE
   TYPE emp_record IS RECORD (id NUMBER, name VARCHAR2(100));
   v_emp emp_record;
BEGIN
   v_emp.id := 101;
   v_emp.name := 'John Doe';
END;
```

---

### **Reference Data Types**

Reference data types are used to store pointers or references to other objects, such as cursors.

| **Data Type**    | **Description**                                                   | **Example**                                    |
|------------------|-------------------------------------------------------------------|------------------------------------------------|
| **Cursor**       | A reference to a SQL query result set, used for fetching rows.     | `CURSOR emp_cursor IS SELECT * FROM employees;` |

#### Example Usage  
```sql
DECLARE
   CURSOR emp_cursor IS SELECT employee_id, employee_name FROM employees;
BEGIN
   FOR emp IN emp_cursor LOOP
      DBMS_OUTPUT.PUT_LINE(emp.employee_name);
   END LOOP;
END;
```

---

### **LOB (Large Object) Data Types**

LOBs are used to store large amounts of data, such as files, images, or long text.

| **Data Type**    | **Description**                                                   | **Example**                                           |
|------------------|-------------------------------------------------------------------|-------------------------------------------------------|
| **BLOB**         | Stores binary large objects (e.g., images, audio files).           | `v_blob BLOB;`                                        |
| **CLOB**         | Stores character large objects (e.g., large text).                | `v_clob CLOB;`                                        |
| **NCLOB**        | Stores National Character Set large objects (for multi-byte text). | `v_nclob NCLOB;`                                      |
| **BFILE**        | Stores large files from external file systems.                     | `v_bfile BFILE;`                                      |

#### Example Usage  
```sql
DECLARE
   v_clob CLOB;
BEGIN
   DBMS_LOB.CREATETEMPORARY(v_clob, TRUE);
   DBMS_LOB.WRITE(v_clob, LENGTH('This is a large text'), 1, 'This is a large text');
END;
```

---

### **Special Data Types in PL/SQL**

| **Data Type**     | **Description**                                                        | **Example**                                      |
|-------------------|------------------------------------------------------------------------|--------------------------------------------------|
| **%ROWTYPE**      | Declares a variable that can hold an entire row of a table or view.    | `v_employee employees%ROWTYPE;`                  |
| **%TYPE**         | Declares a variable that uses the same type as a column in a table.    | `v_salary employees.salary%TYPE;`                |

#### Example Usage  
```sql
DECLARE
   v_employee employees%ROWTYPE;
BEGIN
   SELECT * INTO v_employee FROM employees WHERE employee_id = 101;
END;
```

---

### **Summary Table of Common Data Types**

| **Category**           | **Data Type**    | **Example Usage**                                  |
|------------------------|------------------|----------------------------------------------------|
| **Scalar Types**        | `NUMBER`, `CHAR`, `VARCHAR2`, `BOOLEAN`, `DATE` | `v_age NUMBER(3);`                                |
| **Composite Types**     | `RECORD`, `ARRAY`, `VARRAY`, `NESTED TABLE`     | `TYPE emp_record IS RECORD (id NUMBER, name VARCHAR2(100));` |
| **Reference Types**     | `CURSOR`         | `CURSOR emp_cursor IS SELECT * FROM employees;`   |
| **LOB Types**           | `BLOB`, `CLOB`, `NCLOB`, `BFILE` | `v_blob BLOB;`                                    |
| **Special Types**       | `%ROWTYPE`, `%TYPE` | `v_employee employees%ROWTYPE;`                   |

---
