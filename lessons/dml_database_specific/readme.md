## Database Specific DML

---

### **Data Query Language (DQL) - Database-Specific Details**  

#### **SELECT - Aggregations (COUNT, SUM, AVG, MAX, MIN)**  
- **MySQL:** Supports all basic aggregation functions. Add `WITH ROLLUP` for cumulative totals in `GROUP BY`.  
  ```sql
  SELECT column1, SUM(column2) AS total
  FROM table_name
  GROUP BY column1 WITH ROLLUP;
  ```
- **Oracle SQL:** Provides `ROLLUP`, `CUBE`, and `GROUPING SETS` for advanced grouping.  
  ```sql
  SELECT column1, column2, SUM(column3)
  FROM table_name
  GROUP BY ROLLUP (column1, column2);
  ```
- **SQL Server:** Similar to Oracle for `ROLLUP` and `CUBE`.  
  ```sql
  SELECT column1, SUM(column2) AS total
  FROM table_name
  GROUP BY GROUPING SETS ((column1), ());
  ```
- **PostgreSQL:** Supports `FILTER` for conditionally applying aggregations.  
  ```sql
  SELECT SUM(column1) FILTER (WHERE column1 > 100) AS large_sum
  FROM table_name;
  ```

---

#### **SELECT - JOINs**  
- **MySQL:** Supports standard joins and `STRAIGHT_JOIN` (for optimizer control).  
  ```sql
  SELECT a.column1, b.column2
  FROM table_a a STRAIGHT_JOIN table_b b
  ON a.id = b.id;
  ```
- **Oracle SQL:** Allows `NATURAL JOIN` and advanced joins like `PARTITION OUTER JOIN`.  
  ```sql
  SELECT *
  FROM table_a
  PARTITION OUTER JOIN table_b
  ON (table_a.id = table_b.id);
  ```
- **SQL Server:** Supports `APPLY` for table-valued functions.  
  ```sql
  SELECT a.column1, b.column2
  FROM table_a a
  OUTER APPLY (SELECT TOP 1 column2 FROM table_b WHERE a.id = b.id) b;
  ```
- **PostgreSQL:** Extends `FULL OUTER JOIN` with `USING` syntax for common columns.  
  ```sql
  SELECT *
  FROM table_a FULL JOIN table_b USING (id);
  ```

---

#### **Subqueries and Common Table Expressions (CTEs)**  
- **MySQL:** Subqueries are allowed, but CTEs were introduced in version 8.0.  
  ```sql
  WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
  )
  SELECT * FROM cte_name;
  ```
- **Oracle SQL:** Subqueries can be inlined, and hierarchical queries use `CONNECT BY`.  
  ```sql
  SELECT column1, column2
  FROM table_name
  CONNECT BY PRIOR parent_id = child_id;
  ```
- **SQL Server:** Supports recursive CTEs for hierarchy handling.  
  ```sql
  WITH cte_name (column1, column2) AS (
    SELECT column1, column2 FROM table_name
    UNION ALL
    SELECT column1, column2 FROM cte_name WHERE condition
  )
  SELECT * FROM cte_name;
  ```
- **PostgreSQL:** Supports advanced `WITH RECURSIVE` for hierarchical data.  
  ```sql
  WITH RECURSIVE cte_name AS (
    SELECT column1 FROM table_name WHERE condition
    UNION ALL
    SELECT column1 FROM cte_name WHERE condition
  )
  SELECT * FROM cte_name;
  ```

---

### **Data Manipulation Language (DML) - Database-Specific Details**  

#### **INSERT**  
- **MySQL:** Supports `REPLACE` for handling duplicate keys.  
  ```sql
  REPLACE INTO table_name (column1, column2) VALUES (value1, value2);
  ```
- **Oracle SQL:** Uses `MERGE` for upsert operations.  
  ```sql
  MERGE INTO target_table USING source_table
  ON (target_table.id = source_table.id)
  WHEN MATCHED THEN
    UPDATE SET column1 = source_table.column1
  WHEN NOT MATCHED THEN
    INSERT (column1, column2) VALUES (source_table.column1, source_table.column2);
  ```
- **SQL Server:** Includes `OUTPUT` to capture inserted rows.  
  ```sql
  INSERT INTO table_name (column1, column2)
  OUTPUT INSERTED.column1, INSERTED.column2
  VALUES (value1, value2);
  ```
- **PostgreSQL:** Supports `ON CONFLICT` for upserts.  
  ```sql
  INSERT INTO table_name (column1, column2)
  VALUES (value1, value2)
  ON CONFLICT (column1) DO UPDATE
  SET column2 = EXCLUDED.column2;
  ```

---

#### **UPDATE**  
- **MySQL:** Allows joins in `UPDATE` statements.  
  ```sql
  UPDATE table_a
  JOIN table_b ON table_a.id = table_b.id
  SET table_a.column1 = table_b.column1;
  ```
- **Oracle SQL:** Supports conditional updates using `CASE`.  
  ```sql
  UPDATE table_name
  SET column1 = CASE WHEN condition THEN value1 ELSE value2 END;
  ```
- **SQL Server:** Includes `OUTPUT` for tracking changes.  
  ```sql
  UPDATE table_name
  SET column1 = value1
  OUTPUT INSERTED.column1, DELETED.column2;
  ```
- **PostgreSQL:** Supports `FROM` for joins in updates.  
  ```sql
  UPDATE table_a
  SET column1 = b.column2
  FROM table_b b
  WHERE table_a.id = b.id;
  ```

---

#### **DELETE**  
- **MySQL:** Deletes with joins for conditional deletions.  
  ```sql
  DELETE table_a
  FROM table_a
  INNER JOIN table_b ON table_a.id = table_b.id
  WHERE condition;
  ```
- **Oracle SQL:** Allows subqueries in deletes.  
  ```sql
  DELETE FROM table_name
  WHERE column1 IN (SELECT column1 FROM another_table);
  ```
- **SQL Server:** Includes `TOP` to limit rows.  
  ```sql
  DELETE TOP (10) FROM table_name WHERE condition;
  ```
- **PostgreSQL:** Includes `RETURNING` for tracking deleted rows.  
  ```sql
  DELETE FROM table_name
  WHERE condition
  RETURNING column1, column2;
  ```

---

#### **MERGE** *(SQL Server, Oracle SQL)*  
- **SQL Server:** Adds `OUTPUT` to capture affected rows.  
  ```sql
  MERGE INTO target_table USING source_table
  ON target_table.key = source_table.key
  WHEN MATCHED THEN
    UPDATE SET column1 = source_table.column1
  WHEN NOT MATCHED THEN
    INSERT (column1, column2) VALUES (source_table.column1, source_table.column2)
  OUTPUT $action, INSERTED.column1;
  ```

---

### **Extra Headings and Advanced Details**  

#### **Transaction Management**  
Supported in all major databases.  
**Syntax:**  
```sql
BEGIN TRANSACTION;
UPDATE table_name SET column1 = value1 WHERE condition;
COMMIT;
ROLLBACK;
```

#### **Locks and Concurrency Control**  
- **MySQL:** Uses `LOCK TABLES` for table-level locks.  
  ```sql
  LOCK TABLES table_name WRITE;
  ```
- **PostgreSQL:** Supports advisory locks.  
  ```sql
  SELECT pg_advisory_lock(key);
  ```

#### **Error Handling**  
- **MySQL:** Uses `DECLARE` for exceptions in stored procedures.  
- **PostgreSQL:** Uses `EXCEPTION` blocks in PL/pgSQL.  

