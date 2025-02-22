## **PostgreSQL Foreign Data Wrappers (FDW) - Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **Foreign Data Wrapper (FDW)** | Allows PostgreSQL to access external data sources. |
| **Foreign Server** | Defines the external database/server. |
| **User Mapping** | Maps PostgreSQL users to foreign server users. |
| **Foreign Table** | Represents external data within PostgreSQL. |
| **FDW Handlers** | Custom extensions that manage data retrieval. |

---

## **2. Key FDW Extensions**  
| FDW | Purpose |
|-----|---------|
| `postgres_fdw` | Connects to remote PostgreSQL databases. |
| `file_fdw` | Reads from external CSV and text files. |
| `mysql_fdw` | Connects to MySQL databases. |
| `oracle_fdw` | Connects to Oracle databases. |
| `mongodb_fdw` | Connects to MongoDB. |
| `odbc_fdw` | Connects to any ODBC-compatible database. |

---

## **3. Installing FDW**  
| Task | Command |
|------|---------|
| Install PostgreSQL FDW | `CREATE EXTENSION postgres_fdw;` |
| Install File FDW | `CREATE EXTENSION file_fdw;` |
| Check Installed FDWs | `SELECT * FROM pg_foreign_data_wrapper;` |

---

## **4. Creating a Foreign Server**  
```sql
CREATE SERVER foreign_pg_server  
FOREIGN DATA WRAPPER postgres_fdw  
OPTIONS (host 'remote_host', dbname 'remote_db', port '5432');
```
- Defines a foreign PostgreSQL server connection.

---

## **5. Creating User Mapping**  
```sql
CREATE USER MAPPING FOR current_user  
SERVER foreign_pg_server  
OPTIONS (user 'remote_user', password 'remote_pass');
```
- Maps the PostgreSQL user to a remote database user.

---

## **6. Creating a Foreign Table**  
```sql
CREATE FOREIGN TABLE foreign_table (
    id SERIAL,
    name TEXT,
    age INT
) SERVER foreign_pg_server  
OPTIONS (schema_name 'public', table_name 'remote_table');
```
- Maps a remote table to PostgreSQL.

---

## **7. Querying a Foreign Table**  
```sql
SELECT * FROM foreign_table;
```
- Queries remote data as if it's local.

---

## **8. Modifying Foreign Data**  
| Operation | Command |
|-----------|---------|
| **Insert** | `INSERT INTO foreign_table VALUES (1, 'Alice', 25);` |
| **Update** | `UPDATE foreign_table SET age = 26 WHERE id = 1;` |
| **Delete** | `DELETE FROM foreign_table WHERE id = 1;` |

---

## **9. Dropping FDW Components**  
| Task | Command |
|------|---------|
| Drop Foreign Table | `DROP FOREIGN TABLE foreign_table;` |
| Drop User Mapping | `DROP USER MAPPING FOR current_user SERVER foreign_pg_server;` |
| Drop Foreign Server | `DROP SERVER foreign_pg_server CASCADE;` |

---

## **10. Performance Considerations**  
| Optimization | Description |
|-------------|-------------|
| **Use `IMPORT FOREIGN SCHEMA`** | Automatically imports tables from the foreign server. |
| **Enable `JOIN PUSH-DOWN`** | Allows remote joins instead of fetching all data. |
| **Use `EXPLAIN ANALYZE`** | Identifies performance bottlenecks in foreign queries. |
