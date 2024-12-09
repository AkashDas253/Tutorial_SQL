# SQL Basics

## Types of SQL Commands

```mermaid
graph TD
    A[SQL Commands] --> B[DDL (Data Definition Language)];
    A --> C[DML (Data Manipulation Language)];
    A --> D[DCL (Data Control Language)];
    A --> E[TCL (Transaction Control Language)];
    A --> F[DQL (Data Query Language)];

    B --> B1[CREATE];
    B --> B2[ALTER];
    B --> B3[DROP];
    B --> B4[TRUNCATE];
    B --> B5[RENAME];

    C --> C1[SELECT];
    C --> C2[INSERT];
    C --> C3[UPDATE];
    C --> C4[DELETE];
    C --> C5[MERGE];

    D --> D1[GRANT];
    D --> D2[REVOKE];

    E --> E1[COMMIT];
    E --> E2[ROLLBACK];
    E --> E3[SAVEPOINT];
    E --> E4[SET TRANSACTION];

    F --> F1[SELECT];
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

