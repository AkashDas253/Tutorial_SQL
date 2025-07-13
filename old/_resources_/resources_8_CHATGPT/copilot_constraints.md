### **Query and Schema Constraints**

Constraints are rules enforced on database columns to maintain data integrity and ensure consistency. They can be applied at the table creation or modification stage.

---

#### **Types of Constraints**

1. **Primary Key**  
   - Ensures that each row in a table is uniquely identifiable.  
   - A table can have only one primary key, which can consist of one or multiple columns (composite primary key).  

   **Syntax:**  
   ```sql
   CREATE TABLE table_name (
       column_name data_type PRIMARY KEY
   );

   -- Composite Primary Key
   CREATE TABLE table_name (
       column1 data_type,
       column2 data_type,
       PRIMARY KEY (column1, column2)
   );
   ```

   **Alter Table Syntax:**  
   ```sql
   ALTER TABLE table_name
   ADD PRIMARY KEY (column_name);
   ```

---

2. **Foreign Key**  
   - Establishes a relationship between two tables by referencing the primary key of another table.  
   - Ensures referential integrity by restricting actions like delete/update on parent rows.

   **Syntax:**  
   ```sql
   CREATE TABLE child_table (
       column_name data_type,
       FOREIGN KEY (column_name) REFERENCES parent_table (primary_key_column)
   );
   ```

   **Alter Table Syntax:**  
   ```sql
   ALTER TABLE child_table
   ADD CONSTRAINT fk_name
   FOREIGN KEY (column_name) REFERENCES parent_table (primary_key_column);
   ```

---

3. **UNIQUE**  
   - Ensures all values in a column or combination of columns are distinct.  
   - A table can have multiple unique constraints.  

   **Syntax:**  
   ```sql
   CREATE TABLE table_name (
       column_name data_type UNIQUE
   );

   -- Multiple Columns
   CREATE TABLE table_name (
       column1 data_type,
       column2 data_type,
       UNIQUE (column1, column2)
   );
   ```

   **Alter Table Syntax:**  
   ```sql
   ALTER TABLE table_name
   ADD UNIQUE (column_name);
   ```

---

4. **NOT NULL**  
   - Ensures that a column cannot have `NULL` values.  

   **Syntax:**  
   ```sql
   CREATE TABLE table_name (
       column_name data_type NOT NULL
   );
   ```

   **Alter Table Syntax:**  
   ```sql
   ALTER TABLE table_name
   MODIFY column_name data_type NOT NULL;
   ```

---

5. **CHECK**  
   - Ensures that all values in a column satisfy a specified condition.  

   **Syntax:**  
   ```sql
   CREATE TABLE table_name (
       column_name data_type,
       CONSTRAINT check_name CHECK (column_name condition)
   );
   ```

   **Alter Table Syntax:**  
   ```sql
   ALTER TABLE table_name
   ADD CONSTRAINT check_name CHECK (column_name condition);
   ```

---

6. **DEFAULT**  
   - Specifies a default value for a column if no value is provided during insertion.  

   **Syntax:**  
   ```sql
   CREATE TABLE table_name (
       column_name data_type DEFAULT default_value
   );
   ```

   **Alter Table Syntax:**  
   ```sql
   ALTER TABLE table_name
   ALTER COLUMN column_name SET DEFAULT default_value;
   ```

---

### **Constraint Categories**

| **Constraint** | **Purpose**                          | **Key Feature**                          |
|-----------------|--------------------------------------|------------------------------------------|
| **Primary Key** | Uniquely identifies rows in a table  | Single per table; composite allowed.     |
| **Foreign Key** | Establishes relationships           | Enforces referential integrity.          |
| **UNIQUE**      | Ensures distinct column values       | Multiple allowed per table.              |
| **NOT NULL**    | Restricts null values               | Applied at the column level.             |
| **CHECK**       | Validates column value conditions   | Customizable for flexible constraints.   |
| **DEFAULT**     | Sets default values                 | Simplifies data insertion.               |

---

### **Diagram: Constraint Relationships**

```mermaid
erDiagram
    Table1 {
        PK id INT
        UNIQUE column1
        NOT NULL column2
    }
    Table2 {
        PK foreign_id INT
        FK column3 REFERENCES Table1(id)
    }
    Table1 ||--o{ Table2 : "One-to-Many Relationship"
```

---

#### **Additional Points**

1. **Enabling/Disabling Constraints:**  
   Some databases allow toggling constraints without dropping them.  
   ```sql
   ALTER TABLE table_name DISABLE CONSTRAINT constraint_name;
   ALTER TABLE table_name ENABLE CONSTRAINT constraint_name;
   ```

2. **Deferred Constraints (PostgreSQL, Oracle SQL):**  
   - Constraints can be enforced at the end of a transaction rather than at statement execution.  
   ```sql
   SET CONSTRAINTS constraint_name DEFERRED;
   ```

3. **Cascading Actions (Foreign Key):**  
   - **ON DELETE CASCADE:** Deletes child rows when the parent is deleted.  
   - **ON UPDATE CASCADE:** Updates child rows when the parent key changes.  
   ```sql
   FOREIGN KEY (column_name) REFERENCES parent_table (primary_key) ON DELETE CASCADE;
   ```

Would you like me to elaborate on indexing with constraints or compatibility across specific databases?