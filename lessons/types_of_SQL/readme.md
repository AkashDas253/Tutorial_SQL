# SQL Basics

## Types of SQL Commands

```mermaid
graph TD
    A[SQL Commands] --> B[DDL (Data Definition Language)]
    A --> C[DML (Data Manipulation Language)]
    A --> D[DCL (Data Control Language)]
    A --> E[TCL (Transaction Control Language)]
    A --> F[DQL (Data Query Language)]

    B --> B1[CREATE]
    B --> B2[ALTER]
    B --> B3[DROP]
    B --> B4[TRUNCATE]
    B --> B5[RENAME]

    C --> C1[SELECT]
    C --> C2[INSERT]
    C --> C3[UPDATE]
    C --> C4[DELETE]
    C --> C5[MERGE]

    D --> D1[GRANT]
    D --> D2[REVOKE]

    E --> E1[COMMIT]
    E --> E2[ROLLBACK]
    E --> E3[SAVEPOINT]
    E --> E4[SET TRANSACTION]

    F --> F1[SELECT]

    ```

### **1. DDL (Data Definition Language)**

### **Key Commands:**

  - **CREATE TABLE**: Create a new table in the database.
    
    `CREATE TABLE table_name (column1 datatype, column2 datatype);`

  - **ALTER TABLE**: Modify the structure of an existing table.
    
    `ALTER TABLE table_name ADD column_name datatype;`

  - **DROP TABLE**: Delete an existing table from the database.
    
    `DROP TABLE table_name;`

  - **TRUNCATE**: Remove all records from a table, but keep the table structure.
    
    `TRUNCATE TABLE table_name;`

  - **RENAME**: Rename an existing table in the database.
    
    `RENAME TABLE old_table_name TO new_table_name;`

### **Types of Constraints:**

  - PRIMARY KEY: `PRIMARY KEY (column_name)`
  - FOREIGN KEY: `FOREIGN KEY (column_name) REFERENCES other_table(column_name)`
  - UNIQUE: `UNIQUE (column_name)`
  - CHECK: `CHECK (condition)`
  - NOT NULL: `column_name datatype NOT NULL`

### **2. DQL (Data Query Language)**

- **Key Command:**
  - **SELECT**: It is used to retrieve data from the database.
    
    `SELECT column1, column2, ... FROM table_name WHERE condition;`

### **3. DML (Data Manipulation Language)**

### **Key Commands:**

  - **INSERT**: Insert data into a table.
      
      `INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);`

  - **UPDATE**: Update existing data within a table.
      
      `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;`

  - **DELETE**: Delete records from a database table.
      
      `DELETE FROM table_name WHERE condition;`

  - **LOCK**: Control table concurrency.
      
      `LOCK TABLE table_name IN lock_mode;`

  - **CALL**: Call a PL/SQL or JAVA subprogram.
      
      `CALL procedure_name(arguments);`

  - **EXPLAIN PLAN**: Describe the access path to data.
      
      `EXPLAIN PLAN FOR SELECT * FROM table_name;`

### **4. DCL (Data Control Language)**

### **Key Commands:**

  - **GRANT**: Assigns new privileges to a user account, allowing access to specific database objects, actions, or functions.
      
      `GRANT privilege_type [(column_list)] ON [object_type] object_name TO user [WITH GRANT OPTION];`

  - **REVOKE**: Removes previously granted privileges from a user account, taking away their access to certain database objects or actions.
      
      `REVOKE [GRANT OPTION FOR] privilege_type [(column_list)] ON [object_type] object_name FROM user [CASCADE];`

### **Possible Permissions:**
  - `SELECT`
  - `INSERT`
  - `UPDATE`
  - `DELETE`
  - `EXECUTE`

### **5. TCL (Transaction Control Language)**

### **Key Commands:**

  - **BEGIN TRANSACTION**: Starts a new transaction.
      
      `BEGIN TRANSACTION [transaction_name];`

  - **COMMIT**: Saves all changes made during the transaction.
      
      `COMMIT;`

  - **ROLLBACK**: Undoes all changes made during the transaction.
      
      `ROLLBACK;`

  - **SAVEPOINT**: Creates a savepoint within the current transaction.
      
      `SAVEPOINT savepoint_name;`

## SQL Operators

### 1. Comparison Operators

- `=`: Equal to
- `!=` or `<>`: Not equal to
- `>`: Greater than
- `<`: Less than
- `>=`: Greater than or equal to
- `<=`: Less than or equal to

### 2. Logical Operators

- `AND`: Returns true if both conditions are true.
- `OR`: Returns true if at least one condition is true.
- `NOT`: Reverses the result of a condition.

### 3. Arithmetic Operators

- `+`: Addition
- `-`: Subtraction
- `*`: Multiplication
- `/`: Division
- `%`: Modulus (remainder)

### 4. Bitwise Operators

- `&`: Bitwise AND
- `|`: Bitwise OR
- `^`: Bitwise XOR
- `~`: Bitwise NOT
- `<<`: Bitwise left shift
- `>>`: Bitwise right shift

### 5. String Operators

- `||`: Concatenation operator (some SQL dialects use `+`)
- `LIKE`: Used to search for a specified pattern in a column.
- `IN`: Checks if a value exists in a set of values.

## SQL Functions

SQL functions are built-in routines that perform operations on data and return a value. They can be categorized into different types based on their functionality, such as aggregate functions, scalar functions, and more. Understanding these functions is essential for effective data manipulation and analysis.

### 1. Aggregate Functions

Aggregate functions perform calculations on multiple rows of a table and return a single value. They are commonly used in conjunction with the `GROUP BY` clause.

- `COUNT()`: Returns the number of rows that match a specified condition.
- `SUM()`: Returns the total sum of a numeric column.
- `AVG()`: Returns the average value of a numeric column.
- `MIN()`: Returns the smallest value in a set.
- `MAX()`: Returns the largest value in a set.

### 2. Scalar Functions

Scalar functions operate on a single value and return a single value. They can be used for string manipulation, date calculations, and mathematical operations.

- String Functions

  - `UPPER()`: Converts a string to uppercase.
  - `LOWER()`: Converts a string to lowercase.
  - `SUBSTRING()`: Extracts a substring from a string.
  - `LENGTH()`: Returns the length of a string.

- Date Functions

  - `NOW()`: Returns the current date and time.
  - `CURDATE()`: Returns the current date.
  - `DATEDIFF()`: Returns the difference between two dates.

- Mathematical Functions

  - `ROUND()`: Rounds a number to a specified number of decimal places.
  - `FLOOR()`: Returns the largest integer value less than or equal to a number.
  - `CEIL()`: Returns the smallest integer value greater than or equal to a number.

- **Syntax:**
  
  ```sql
  -- String Functions
  SELECT function_name(column_name) AS alias_name FROM table_name;
  SELECT function_name(column_name, additional_parameters) AS alias_name FROM table_name;

  -- Date Functions
  SELECT function_name() AS alias_name;
  SELECT function_name(date1, date2) AS alias_name FROM table_name;

  -- Mathematical Functions
  SELECT function_name(column_name) AS alias_name FROM table_name;
  SELECT function_name(column_name, additional_parameters) AS alias_name FROM table_name;```


### 3. Conditional Functions

Conditional functions evaluate conditions and return specific values based on the evaluation.

- `IF()`: Returns one value if a condition is true and another value if it is false.
- `CASE`: A more complex conditional function that allows multiple conditions to be evaluated.

**Syntax:**

```sql
SELECT column_name,
       IF(condition, value_if_true, value_if_false) AS alias_name
FROM table_name;

SELECT column_name,
       CASE 
           WHEN condition1 THEN result1
           WHEN condition2 THEN result2
           ELSE result_else
       END AS alias_name
FROM table_name;