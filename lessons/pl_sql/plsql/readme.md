## PL/SQL cheatsheet

- **PL/SQL Basics**  
  - Anonymous Blocks  
  - Variables & Constants  
  - Data Types  
  - Operators  

- **Control Structures**  
  - Conditional Statements (`IF-THEN-ELSE`)  
  - Loops (`FOR`, `WHILE`, `LOOP`)  
  - CASE Statements  

- **Cursors**  
  - Implicit Cursors  
  - Explicit Cursors  
  - Cursor FOR Loops  
  - Parameterized Cursors  
  - REF Cursors  

- **Exceptions Handling**  
  - Predefined Exceptions  
  - User-Defined Exceptions  
  - `RAISE` Statement  

- **Procedures & Functions**  
  - Stored Procedures  
  - Functions  
  - Parameter Modes (`IN`, `OUT`, `IN OUT`)  

- **Packages**  
  - Package Specification  
  - Package Body  
  - Public vs Private Components  

- **Triggers**  
  - BEFORE & AFTER Triggers  
  - ROW-Level & Statement-Level Triggers  
  - INSTEAD OF Triggers  

- **Collections**  
  - VARRAYs  
  - Nested Tables  
  - Associative Arrays  

- **Bulk Processing**  
  - `BULK COLLECT`  
  - `FORALL`  

- **Dynamic SQL**  
  - `EXECUTE IMMEDIATE`  
  - `DBMS_SQL`  

- **Records & PL/SQL Tables**  
  - %ROWTYPE  
  - %TYPE  

- **DBMS_SCHEDULER**  
  - Creating Jobs  
  - Job Chains  

- **Security & Privileges**  
  - Definer vs Invoker Rights  
  - Granting Execute Privileges  

- **Performance Optimization**  
  - Query Optimization  
  - PL/SQL Compiler Warnings  

- **Advanced PL/SQL**  
  - Autonomous Transactions  
  - Pipelined Functions  

----

## PL/SQL Concepts  

- **PL/SQL Architecture**  
  - PL/SQL Engine  
  - Oracle Server Interaction  
  - Anonymous Blocks  
  - Stored Procedures  

- **PL/SQL Block Structure**  
  - Declaration Section  
  - Execution Section  
  - Exception Handling Section  

- **Data Types in PL/SQL**  
  - Scalar Data Types  
    - `NUMBER`, `CHAR`, `VARCHAR2`, `DATE`, `BOOLEAN`  
  - Composite Data Types  
    - Records  
    - Collections (`INDEX BY TABLE`, `VARRAY`, `NESTED TABLE`)  
  - Reference Data Types  
    - Cursors  
  - LOB Data Types  
    - `BLOB`, `CLOB`, `NCLOB`, `BFILE`  

- **Control Structures**  
  - Conditional Statements  
    - `IF...THEN...ELSE`  
    - `CASE`  
  - Loops  
    - `FOR` Loop  
    - `WHILE` Loop  
    - `LOOP...EXIT WHEN`  

- **Cursors**  
  - Implicit Cursors  
  - Explicit Cursors  
  - Cursor Attributes  
    - `%FOUND`, `%NOTFOUND`, `%ISOPEN`, `%ROWCOUNT`  
  - Parameterized Cursors  
  - Cursor FOR Loop  

- **Triggers**  
  - Types of Triggers  
    - DML Triggers  
    - Instead-of Triggers  
    - System Triggers  
  - Trigger Timing  
    - BEFORE  
    - AFTER  
    - INSTEAD OF  
  - Compound Triggers  

- **Procedures and Functions**  
  - Stored Procedures  
  - Stored Functions  
  - Parameter Modes  
    - `IN`, `OUT`, `IN OUT`  

- **Packages**  
  - Package Specification  
  - Package Body  
  - Advantages of Packages  
  - Overloading Procedures and Functions  

- **Exception Handling**  
  - Predefined Exceptions  
  - User-defined Exceptions  
  - Exception Propagation  
  - RAISE_APPLICATION_ERROR  

- **PL/SQL Collections**  
  - Associative Arrays  
  - Nested Tables  
  - VARRAYs  
  - Collection Methods  
    - `COUNT`, `LIMIT`, `FIRST`, `LAST`, `PRIOR`, `NEXT`, `EXTEND`, `TRIM`, `DELETE`  

- **Dynamic SQL**  
  - `EXECUTE IMMEDIATE`  
  - `DBMS_SQL` Package  

- **Built-in Functions**  
  - String Functions  
    - `CONCAT`, `SUBSTR`, `LENGTH`, `INSTR`  
  - Numeric Functions  
    - `ABS`, `MOD`, `ROUND`, `TRUNC`  
  - Date Functions  
    - `SYSDATE`, `ADD_MONTHS`, `MONTHS_BETWEEN`  
  - Conversion Functions  
    - `TO_CHAR`, `TO_NUMBER`, `TO_DATE`  

- **Transactions in PL/SQL**  
  - COMMIT  
  - ROLLBACK  
  - SAVEPOINT  
  - Autocommit  

- **Advanced Concepts**  
  - Autonomous Transactions  
  - Bulk Processing  
    - `FORALL`  
    - Bulk Collect  
  - Native Dynamic SQL (NDS)  
  - Pipelined Table Functions  
  - Analytical Functions  

- **Security in PL/SQL**  
  - Definer Rights  
  - Invoker Rights  
  - Roles and Privileges  

- **PL/SQL Optimization**  
  - Use of Bind Variables  
  - Optimizing Loops and Queries  
  - PL/SQL Profiler  
  - PL/SQL Compiler Warnings  
