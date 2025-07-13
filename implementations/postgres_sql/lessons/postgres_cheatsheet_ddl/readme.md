# **Data Definition Language (DDL) in PostgreSQL**

## **Overview**
Data Definition Language (DDL) in PostgreSQL consists of SQL statements used to define, modify, and manage database objects such as databases, tables, indexes, schemas, and constraints.

---

## **DDL Statements**

### **Database Management**
| **Statement** | **Description** |
|--------------|---------------|
| `CREATE DATABASE db_name;` | Creates a new database. |
| `DROP DATABASE db_name;` | Deletes an existing database. |
| `ALTER DATABASE db_name RENAME TO new_name;` | Renames an existing database. |
| `ALTER DATABASE db_name SET param = value;` | Changes database configuration settings. |

---

### **Schema Management**
| **Statement** | **Description** |
|--------------|---------------|
| `CREATE SCHEMA schema_name;` | Creates a new schema. |
| `DROP SCHEMA schema_name;` | Deletes a schema. |
| `DROP SCHEMA schema_name CASCADE;` | Deletes a schema along with all objects inside it. |
| `ALTER SCHEMA schema_name RENAME TO new_name;` | Renames a schema. |

---

### **Table Management**
| **Statement** | **Description** |
|--------------|---------------|
| `CREATE TABLE table_name (col1 type, col2 type, ...);` | Creates a new table. |
| `DROP TABLE table_name;` | Deletes an existing table. |
| `DROP TABLE table_name CASCADE;` | Deletes a table and all dependent objects. |
| `ALTER TABLE table_name RENAME TO new_name;` | Renames a table. |
| `ALTER TABLE table_name ADD COLUMN col_name data_type;` | Adds a new column to a table. |
| `ALTER TABLE table_name DROP COLUMN col_name;` | Removes a column from a table. |
| `ALTER TABLE table_name ALTER COLUMN col_name SET DEFAULT value;` | Sets a default value for a column. |
| `ALTER TABLE table_name ALTER COLUMN col_name DROP DEFAULT;` | Removes a default value from a column. |

---

### **Index Management**
| **Statement** | **Description** |
|--------------|---------------|
| `CREATE INDEX index_name ON table_name (column_name);` | Creates an index to speed up queries. |
| `DROP INDEX index_name;` | Deletes an index. |
| `ALTER INDEX index_name RENAME TO new_name;` | Renames an index. |
| `CREATE UNIQUE INDEX index_name ON table_name (column_name);` | Creates a unique index to prevent duplicate values. |

---

### **Constraints**
Constraints enforce rules on data in tables.

| **Constraint** | **Description** |
|--------------|---------------|
| `PRIMARY KEY (col_name);` | Ensures unique and non-null values for a column. |
| `UNIQUE (col_name);` | Ensures all values in a column are unique. |
| `CHECK (condition);` | Ensures column values meet a specific condition. |
| `FOREIGN KEY (col_name) REFERENCES other_table(col_name);` | Enforces referential integrity between tables. |
| `NOT NULL;` | Ensures a column cannot have NULL values. |

#### **Adding Constraints**
```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY (col_name);
```

#### **Removing Constraints**
```sql
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```

---

### **View Management**
| **Statement** | **Description** |
|--------------|---------------|
| `CREATE VIEW view_name AS SELECT col1, col2 FROM table_name;` | Creates a virtual table based on a query. |
| `DROP VIEW view_name;` | Deletes a view. |
| `ALTER VIEW view_name RENAME TO new_name;` | Renames a view. |

---

### **Materialized Views**
Materialized views store query results and can be refreshed.

| **Statement** | **Description** |
|--------------|---------------|
| `CREATE MATERIALIZED VIEW mv_name AS SELECT * FROM table_name;` | Creates a materialized view. |
| `REFRESH MATERIALIZED VIEW mv_name;` | Updates the materialized view with fresh data. |
| `DROP MATERIALIZED VIEW mv_name;` | Deletes a materialized view. |

---

### **Sequences (Auto-Increment)**
Sequences generate unique numbers for primary keys.

| **Statement** | **Description** |
|--------------|---------------|
| `CREATE SEQUENCE seq_name;` | Creates a sequence. |
| `DROP SEQUENCE seq_name;` | Deletes a sequence. |
| `SELECT nextval('seq_name');` | Gets the next sequence value. |
| `ALTER SEQUENCE seq_name RESTART WITH 1;` | Resets the sequence value. |

---

### **Tablespace Management**
Tablespaces define storage locations.

| **Statement** | **Description** |
|--------------|---------------|
| `CREATE TABLESPACE ts_name LOCATION 'path';` | Creates a tablespace. |
| `DROP TABLESPACE ts_name;` | Deletes a tablespace. |

---

## **Key Takeaways**
- **DDL defines the structure** of databases, schemas, tables, indexes, constraints, views, and sequences.
- **DDL changes are auto-committed**, meaning they **cannot be rolled back**.
- **Indexes speed up queries**, but require maintenance.
- **Views store query logic**, while **materialized views store actual data**.
- **Constraints enforce rules**, ensuring data integrity.
- **Sequences generate unique values** for primary keys.
- **Tablespaces manage storage locations** for database objects.
