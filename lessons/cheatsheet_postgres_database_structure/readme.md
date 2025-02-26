## **PostgreSQL Database Structure Cheatsheet**  

#### **1. Database Components**  
| Component | Description |
|-----------|------------|
| **Database** | Collection of schemas, tables, and other objects. |
| **Schema** | Logical namespace containing tables, views, indexes, etc. Default schema is `public`. |
| **Table** | Structured data storage consisting of rows and columns. |
| **Column** | Defines attributes of a table, with a specific data type. |
| **Row** | A single record in a table. |
| **View** | A virtual table based on a query result. |
| **Index** | Data structure to speed up queries. |
| **Sequence** | Auto-incrementing number generator. Used for `serial` and `bigserial`. |
| **Constraint** | Rules enforced on table columns (e.g., `PRIMARY KEY`, `FOREIGN KEY`). |

#### **2. Schema Management**  
| Action | Command |
|--------|---------|
| List Schemas | `SELECT schema_name FROM information_schema.schemata;` |
| Create Schema | `CREATE SCHEMA schema_name;` |
| Drop Schema | `DROP SCHEMA schema_name CASCADE;` |
| Set Default Schema | `SET search_path TO schema_name;` |

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
| Drop Column | `ALTER TABLE table_name DROP COLUMN column_name;` |

#### **5. Constraints**  
| Constraint | Description |
|------------|------------|
| `PRIMARY KEY` | Uniquely identifies each row. |
| `FOREIGN KEY` | Enforces referential integrity between tables. |
| `UNIQUE` | Ensures values in a column are unique. |
| `CHECK` | Ensures column values meet a condition. |
| `NOT NULL` | Prevents `NULL` values in a column. |

#### **6. Indexes**  
| Action | Command |
|--------|---------|
| Create Index | `CREATE INDEX idx_name ON table_name (column_name);` |
| List Indexes | `SELECT indexname FROM pg_indexes WHERE tablename = 'table_name';` |
| Drop Index | `DROP INDEX idx_name;` |
