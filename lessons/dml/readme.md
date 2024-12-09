## **Data Query Language (DQL)**  
DQL focuses on querying data from the database. The primary command is `SELECT`, which retrieves data based on the criteria specified.

#### **SELECT**  
Used to retrieve data from one or more tables.  

**Syntax:**  
```sql
SELECT [DISTINCT] column1, column2, ...
FROM table_name
[WHERE condition]
[GROUP BY column1, column2, ...]
[HAVING condition]
[ORDER BY column1 [ASC|DESC], column2 [ASC|DESC]]
[LIMIT row_count OFFSET row_skip];
```

##### **Aggregations**  
Used to compute summary statistics.  
- **COUNT:** Counts the number of rows.  
  ```sql
  SELECT COUNT(column_name) FROM table_name;
  ```
- **SUM:** Adds numerical values.  
  ```sql
  SELECT SUM(column_name) FROM table_name;
  ```
- **AVG:** Calculates the average value.  
  ```sql
  SELECT AVG(column_name) FROM table_name;
  ```
- **MAX/MIN:** Finds the maximum/minimum value.  
  ```sql
  SELECT MAX(column_name), MIN(column_name) FROM table_name;
  ```

##### **GROUP BY and HAVING**  
Organizes data into groups for aggregation, with filters on grouped data using `HAVING`.  
**Syntax:**  
```sql
SELECT column1, AGGREGATE_FUNCTION(column2)
FROM table_name
GROUP BY column1
HAVING AGGREGATE_FUNCTION(column2) condition;
```

##### **JOINs**  
Combines rows from multiple tables based on a related column.  
- **INNER JOIN:** Matches rows in both tables.  
  ```sql
  SELECT a.column1, b.column2
  FROM table_a a
  INNER JOIN table_b b
  ON a.common_field = b.common_field;
  ```
- **LEFT JOIN:** Includes unmatched rows from the left table.  
- **RIGHT JOIN:** Includes unmatched rows from the right table.  
- **FULL JOIN:** Includes unmatched rows from both tables.  
- **CROSS JOIN:** Produces a Cartesian product.  

##### **Subqueries**  
Nested queries inside another query.  
- **Correlated Subquery:** Depends on the outer query.  
  ```sql
  SELECT column1
  FROM table1 t1
  WHERE EXISTS (
    SELECT 1
    FROM table2 t2
    WHERE t2.column2 = t1.column1
  );
  ```
- **Uncorrelated Subquery:** Independent of the outer query.  

##### **Common Table Expressions (CTE)** *(SQL Server, PostgreSQL)*  
Defines a temporary result set for use within a query.  
**Syntax:**  
```sql
WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
)
SELECT * FROM cte_name;
```

##### **Window Functions** *(PostgreSQL, SQL Server)*  
Calculates results across a window of rows.  
**Syntax:**  
```sql
SELECT column1,
       ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column3) AS rank
FROM table_name;
```

---

### **Data Manipulation Language (DML)**  
DML commands modify data in the database.

#### **INSERT**  
Adds new rows to a table.  

##### **Single/Multi-row Insert**  
**Syntax:**  
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...), (value3, value4, ...);
```

##### **INSERT INTO SELECT**  
Copies data from one table to another.  
**Syntax:**  
```sql
INSERT INTO target_table (column1, column2, ...)
SELECT column1, column2
FROM source_table
WHERE condition;
```

##### **ON DUPLICATE KEY UPDATE** *(MySQL)*  
Updates existing rows on duplicate key conflict.  
**Syntax:**  
```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2)
ON DUPLICATE KEY UPDATE column1 = value3;
```

---

#### **UPDATE**  
Modifies existing data.  
**Syntax:**  
```sql
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;
```

---

#### **DELETE**  
Removes rows based on a condition.  
**Syntax:**  
```sql
DELETE FROM table_name
WHERE condition;
```

---

#### **MERGE** *(SQL Server, Oracle SQL)*  
Combines `INSERT`, `UPDATE`, and `DELETE` in a single operation.  
**Syntax:**  
```sql
MERGE INTO target_table USING source_table
ON target_table.key = source_table.key
WHEN MATCHED THEN
  UPDATE SET column1 = value1
WHEN NOT MATCHED THEN
  INSERT (column1, column2) VALUES (value1, value2)
WHEN NOT MATCHED BY SOURCE THEN
  DELETE;
```

---

### **Additional Enhancements**  

#### **EXPLAIN**  
Analyzes and displays query execution plans.  
**Syntax:**  
```sql
EXPLAIN SELECT column1 FROM table_name;
```

#### **SET Operators**  
Combine results of multiple queries.  
- **UNION/UNION ALL:** Combines results with or without duplicates.  
- **INTERSECT:** Finds common rows.  
- **EXCEPT/MINUS:** Finds rows in the first query but not the second.  

#### **Transaction Management** *(for DML)*  
Ensures atomicity of operations.  
- **START TRANSACTION:** Begins a new transaction.  
- **COMMIT:** Saves changes.  
- **ROLLBACK:** Undoes changes.  

---

### **Comparison Table: SELECT, INSERT, UPDATE, DELETE, MERGE**  

| **Operation** | **Purpose**                           | **Supports Subqueries?** | **Impact**              |  
|---------------|---------------------------------------|--------------------------|-------------------------|  
| **SELECT**    | Retrieves data from one or more tables | Yes                      | Read-only               |  
| **INSERT**    | Adds new rows to a table              | Yes                      | Data addition           |  
| **UPDATE**    | Modifies existing rows                | Yes                      | Data modification       |  
| **DELETE**    | Removes rows from a table             | Yes                      | Data deletion           |  
| **MERGE**     | Combines multiple DML operations      | Yes                      | Data insertion/updation |  


