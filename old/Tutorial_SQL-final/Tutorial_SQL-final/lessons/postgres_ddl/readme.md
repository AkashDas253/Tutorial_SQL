
## **Data Definition Language (DDL) in PostgreSQL**  

DDL consists of SQL commands that define and manage database structures such as tables, indexes, and schemas. It includes `CREATE`, `ALTER`, `DROP`, and `TRUNCATE`.

---

### **1. CREATE Statement**  
The `CREATE` statement is used to define new database objects such as tables, indexes, views, and schemas.

#### **1.1 CREATE TABLE**  
Defines a new table with specified columns and constraints.

##### **Syntax**  
```sql
CREATE TABLE table_name (
    column1 data_type constraints,
    column2 data_type constraints,
    ...
);
```

##### **Options**  
| Option         | Description | Example |
|---------------|-------------|---------|
| **PRIMARY KEY** | Defines the primary key | `id SERIAL PRIMARY KEY` |
| **FOREIGN KEY** | Establishes a relationship with another table | `dept_id INT REFERENCES departments(id)` |
| **NOT NULL** | Ensures a column cannot be NULL | `name VARCHAR(100) NOT NULL` |
| **DEFAULT** | Sets a default value | `created_at TIMESTAMP DEFAULT NOW()` |
| **CHECK** | Adds a validation rule | `salary INT CHECK (salary > 0)` |

##### **Example**  
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    salary INT CHECK (salary > 0),
    dept_id INT REFERENCES departments(id)
);
```

---

#### **1.2 CREATE INDEX**  
Creates an index to improve query performance.

##### **Syntax**  
```sql
CREATE INDEX index_name ON table_name (column);
```

##### **Example**  
```sql
CREATE INDEX idx_employee_name ON employees(name);
```

---

#### **1.3 CREATE SCHEMA**  
Defines a new schema to organize tables.

##### **Syntax**  
```sql
CREATE SCHEMA schema_name;
```

##### **Example**  
```sql
CREATE SCHEMA hr;
```

---

### **2. ALTER Statement**  
The `ALTER` statement modifies existing database objects.

#### **2.1 ALTER TABLE**  
Modifies an existing table's structure.

##### **Syntax**  
```sql
ALTER TABLE table_name 
ADD COLUMN column_name data_type;
```

##### **Options**  
| Option | Description | Example |
|--------|-------------|---------|
| **ADD COLUMN** | Adds a new column | `ALTER TABLE employees ADD COLUMN age INT;` |
| **DROP COLUMN** | Removes a column | `ALTER TABLE employees DROP COLUMN age;` |
| **RENAME COLUMN** | Renames a column | `ALTER TABLE employees RENAME COLUMN name TO full_name;` |
| **ALTER COLUMN TYPE** | Changes a column's data type | `ALTER TABLE employees ALTER COLUMN salary TYPE BIGINT;` |
| **SET DEFAULT** | Sets a default value | `ALTER TABLE employees ALTER COLUMN salary SET DEFAULT 30000;` |

##### **Example**  
```sql
ALTER TABLE employees ADD COLUMN address TEXT;
```

---

#### **2.2 ALTER INDEX**  
Modifies an existing index.

##### **Syntax**  
```sql
ALTER INDEX index_name RENAME TO new_index_name;
```

##### **Example**  
```sql
ALTER INDEX idx_employee_name RENAME TO idx_emp_name;
```

---

#### **2.3 ALTER SCHEMA**  
Renames a schema.

##### **Syntax**  
```sql
ALTER SCHEMA schema_name RENAME TO new_schema_name;
```

##### **Example**  
```sql
ALTER SCHEMA hr RENAME TO human_resources;
```

---

### **3. DROP Statement**  
The `DROP` statement permanently removes database objects.

#### **3.1 DROP TABLE**  
Deletes a table and all its data.

##### **Syntax**  
```sql
DROP TABLE table_name;
```

##### **Example**  
```sql
DROP TABLE employees;
```

---

#### **3.2 DROP INDEX**  
Removes an index.

##### **Syntax**  
```sql
DROP INDEX index_name;
```

##### **Example**  
```sql
DROP INDEX idx_employee_name;
```

---

#### **3.3 DROP SCHEMA**  
Deletes a schema and all objects within it.

##### **Syntax**  
```sql
DROP SCHEMA schema_name CASCADE;
```

##### **Example**  
```sql
DROP SCHEMA hr CASCADE;
```
> **Note:** The `CASCADE` option removes all objects in the schema.

---

### **4. TRUNCATE Statement**  
The `TRUNCATE` statement removes all rows from a table but retains its structure.

##### **Syntax**  
```sql
TRUNCATE TABLE table_name;
```

##### **Options**  
| Option | Description | Example |
|--------|-------------|---------|
| **CASCADE** | Removes data from related tables | `TRUNCATE TABLE employees CASCADE;` |
| **RESTART IDENTITY** | Resets identity columns (auto-increment) | `TRUNCATE TABLE employees RESTART IDENTITY;` |

##### **Example**  
```sql
TRUNCATE TABLE employees RESTART IDENTITY;
```

---

### **5. Examples of DDL Usage**  

#### **Create and Modify a Table**  
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    salary INT
);

ALTER TABLE employees ADD COLUMN department VARCHAR(50);
```

#### **Remove a Table and Schema**  
```sql
DROP TABLE employees;
DROP SCHEMA hr CASCADE;
```

#### **Truncate Data**  
```sql
TRUNCATE TABLE employees RESTART IDENTITY;
```

---

### **Notes**  
- **DDL commands are auto-committed**, meaning changes cannot be rolled back.  
- **ALTER is used to modify objects without deleting them.**  
- **DROP permanently deletes objects and their data.**  
- **TRUNCATE is faster than DELETE for removing all rows.**  

---
