## **PostgreSQL Database Structure Cheatsheet**  

### **Database Components**  
| Component | Description |
|-----------|------------|
| **Database** | Collection of schemas, tables, and other objects. |
| **Schema** | Logical namespace containing tables, views, indexes, etc. Default schema is `public`. |
| **Table** | Structured data storage consisting of rows and columns. |
| **Column** | Defines attributes of a table, with a specific data type. |
| **Row** | A single record in a table. |
| **View** | A virtual table based on a query result. |
| **Materialized View** | A physical snapshot of query results that can be refreshed. |
| **Index** | Data structure to speed up queries. |
| **Sequence** | Auto-incrementing number generator. Used for `serial` and `bigserial`. |
| **Constraint** | Rules enforced on table columns (e.g., `PRIMARY KEY`, `FOREIGN KEY`). |
| **Function** | A stored procedure that returns a value or executes logic. |
| **Trigger** | A function executed automatically before or after an event on a table. |

### **Schema Management**  
| Action | Command |
|--------|---------|
| List Schemas | `SELECT schema_name FROM information_schema.schemata;` |
| Create Schema | `CREATE SCHEMA schema_name;` |
| Drop Schema | `DROP SCHEMA schema_name CASCADE;` |
| Set Default Schema | `SET search_path TO schema_name;` |

### **Table Management**  
| Action | Command |
|--------|---------|
| Create Table | `CREATE TABLE table_name (id SERIAL PRIMARY KEY, name TEXT);` |
| List Tables | `SELECT tablename FROM pg_tables WHERE schemaname = 'public';` |
| Describe Table | `SELECT column_name, data_type FROM information_schema.columns WHERE table_name = 'table_name';` |
| Rename Table | `ALTER TABLE table_name RENAME TO new_name;` |
| Drop Table | `DROP TABLE table_name;` |

### **Column Management**  
| Action | Command |
|--------|---------|
| Add Column | `ALTER TABLE table_name ADD COLUMN column_name TYPE;` |
| Rename Column | `ALTER TABLE table_name RENAME COLUMN old_name TO new_name;` |
| Change Data Type | `ALTER TABLE table_name ALTER COLUMN column_name TYPE new_type;` |
| Drop Column | `ALTER TABLE table_name DROP COLUMN column_name;` |

### **Constraints**  
| Constraint | Description |
|------------|------------|
| `PRIMARY KEY` | Uniquely identifies each row. |
| `FOREIGN KEY` | Enforces referential integrity between tables. |
| `UNIQUE` | Ensures values in a column are unique. |
| `CHECK` | Ensures column values meet a condition. |
| `NOT NULL` | Prevents `NULL` values in a column. |

### **Indexes**  
| Action | Command |
|--------|---------|
| Create Index | `CREATE INDEX idx_name ON table_name (column_name);` |
| Create Unique Index | `CREATE UNIQUE INDEX idx_name ON table_name (column_name);` |
| Create Partial Index | `CREATE INDEX idx_name ON table_name (column_name) WHERE condition;` |
| List Indexes | `SELECT indexname FROM pg_indexes WHERE tablename = 'table_name';` |
| Drop Index | `DROP INDEX idx_name;` |

### **Views**  
| Action | Command |
|--------|---------|
| Create View | `CREATE VIEW view_name AS SELECT column1, column2 FROM table_name;` |
| List Views | `SELECT table_name FROM information_schema.views WHERE table_schema = 'public';` |
| Drop View | `DROP VIEW view_name;` |

### **Materialized Views**  
| Action | Command |
|--------|---------|
| Create Materialized View | `CREATE MATERIALIZED VIEW mv_name AS SELECT * FROM table_name;` |
| Refresh Materialized View | `REFRESH MATERIALIZED VIEW mv_name;` |
| Drop Materialized View | `DROP MATERIALIZED VIEW mv_name;` |

### **Sequences**  
| Action | Command |
|--------|---------|
| Create Sequence | `CREATE SEQUENCE seq_name START 1 INCREMENT 1;` |
| Get Next Value | `SELECT nextval('seq_name');` |
| Set Sequence Value | `SELECT setval('seq_name', new_value, true);` |
| Drop Sequence | `DROP SEQUENCE seq_name;` |

### **Relationships & Foreign Keys**  
| Action | Command |
|--------|---------|
| Add Foreign Key | `ALTER TABLE child_table ADD CONSTRAINT fk_name FOREIGN KEY (column_name) REFERENCES parent_table (column_name);` |
| Drop Foreign Key | `ALTER TABLE child_table DROP CONSTRAINT fk_name;` |
| List Foreign Keys | `SELECT conname FROM pg_constraint WHERE contype = 'f' AND conrelid = 'child_table'::regclass;` |

### **Triggers**  
| Action | Command |
|--------|---------|
| Create Trigger | `CREATE TRIGGER trigger_name BEFORE INSERT ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();` |
| Drop Trigger | `DROP TRIGGER trigger_name ON table_name;` |
| List Triggers | `SELECT tgname FROM pg_trigger WHERE tgrelid = 'table_name'::regclass;` |

### **Tablespace Management**  
| Action | Command |
|--------|---------|
| Create Tablespace | `CREATE TABLESPACE tablespace_name LOCATION '/var/lib/pgsql/data/tablespace';` |
| Assign Tablespace to Table | `CREATE TABLE table_name (...) TABLESPACE tablespace_name;` |
| Drop Tablespace | `DROP TABLESPACE tablespace_name;` |

### **Partitioning**  
| Action | Command |
|--------|---------|
| Create Partitioned Table | `CREATE TABLE table_name (id SERIAL, name TEXT, created_at DATE) PARTITION BY RANGE (created_at);` |
| Create Partition | `CREATE TABLE table_partitioned_2025 PARTITION OF table_name FOR VALUES FROM ('2025-01-01') TO ('2025-12-31');` |
| List Partitions | `SELECT relname FROM pg_class WHERE relkind = 'p';` |

### **Functions**  
| Action | Command |
|--------|---------|
| Create Function | `CREATE FUNCTION func_name() RETURNS return_type AS $$ BEGIN RETURN value; END; $$ LANGUAGE plpgsql;` |
| Drop Function | `DROP FUNCTION func_name();` |

### **User & Role Management**  
| Action | Command |
|--------|---------|
| Create User | `CREATE USER user_name WITH PASSWORD 'password';` |
| Grant Privileges | `GRANT ALL PRIVILEGES ON database_name TO user_name;` |
| Revoke Privileges | `REVOKE ALL PRIVILEGES ON database_name FROM user_name;` |
| Drop User | `DROP USER user_name;` |

### **Transactions**  
| Action | Command |
|--------|---------|
| Start Transaction | `BEGIN;` |
| Commit Transaction | `COMMIT;` |
| Rollback Transaction | `ROLLBACK;` |
