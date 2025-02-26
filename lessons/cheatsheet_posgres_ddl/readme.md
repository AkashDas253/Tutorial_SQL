## **PostgreSQL DDL (Data Definition Language) Cheatsheet**  

#### **1. Database Management**  
| Action | Command |
|--------|---------|
| Create Database | `CREATE DATABASE dbname;` |
| List Databases | `SELECT datname FROM pg_database;` |
| Connect to Database | `\c dbname` (in `psql`) |
| Rename Database | `ALTER DATABASE dbname RENAME TO new_dbname;` |
| Drop Database | `DROP DATABASE dbname;` |

#### **2. Schema Management**  
| Action | Command |
|--------|---------|
| Create Schema | `CREATE SCHEMA schema_name;` |
| List Schemas | `SELECT schema_name FROM information_schema.schemata;` |
| Set Default Schema | `SET search_path TO schema_name;` |
| Drop Schema | `DROP SCHEMA schema_name CASCADE;` |

#### **3. Table Management**  
| Action | Command |
|--------|---------|
| Create Table | `CREATE TABLE table_name (id SERIAL PRIMARY KEY, name TEXT);` |
| List Tables | `SELECT tablename FROM pg_tables WHERE schemaname = 'public';` |
| Describe Table | `SELECT column_name, data_type FROM information_schema.columns WHERE table_name = 'table_name';` |
| Rename Table | `ALTER TABLE table_name RENAME TO new_name;` |
| Drop Table | `DROP TABLE table_name;` |

#### **4. Column Management**  
| Action | Command |
|--------|---------|
| Add Column | `ALTER TABLE table_name ADD COLUMN column_name TYPE;` |
| Rename Column | `ALTER TABLE table_name RENAME COLUMN old_name TO new_name;` |
| Change Data Type | `ALTER TABLE table_name ALTER COLUMN column_name TYPE new_type;` |
| Set Default Value | `ALTER TABLE table_name ALTER COLUMN column_name SET DEFAULT value;` |
| Drop Column | `ALTER TABLE table_name DROP COLUMN column_name;` |

#### **5. Constraints**  
| Constraint | Command Example |
|------------|----------------|
| `PRIMARY KEY` | `CREATE TABLE t(id SERIAL PRIMARY KEY, name TEXT);` |
| `FOREIGN KEY` | `CREATE TABLE orders(id SERIAL, user_id INT REFERENCES users(id));` |
| `UNIQUE` | `CREATE TABLE t(id SERIAL, name TEXT UNIQUE);` |
| `CHECK` | `CREATE TABLE t(id SERIAL, age INT CHECK (age > 18));` |
| `NOT NULL` | `CREATE TABLE t(id SERIAL, name TEXT NOT NULL);` |
| Add Constraint | `ALTER TABLE t ADD CONSTRAINT chk_age CHECK (age > 18);` |
| Drop Constraint | `ALTER TABLE t DROP CONSTRAINT chk_age;` |

#### **6. Indexes**  
| Action | Command |
|--------|---------|
| Create Index | `CREATE INDEX idx_name ON table_name (column_name);` |
| Create Unique Index | `CREATE UNIQUE INDEX idx_unique ON table_name (column_name);` |
| Drop Index | `DROP INDEX idx_name;` |

#### **7. Views**  
| Action | Command |
|--------|---------|
| Create View | `CREATE VIEW view_name AS SELECT column1, column2 FROM table_name;` |
| Drop View | `DROP VIEW view_name;` |
