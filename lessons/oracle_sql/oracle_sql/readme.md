## Oracle SQL cheatsheet

- **SQL Basics**  
  - Database & Schema  
  - Data Types  
  - NULL Handling  

- **SQL Statements**  
  - DDL (CREATE, ALTER, DROP, TRUNCATE, RENAME)  
  - DML (INSERT, UPDATE, DELETE, MERGE)  
  - DQL (SELECT)  
  - DCL (GRANT, REVOKE)  
  - TCL (COMMIT, ROLLBACK, SAVEPOINT)  

- **Constraints**  
  - Primary Key  
  - Foreign Key  
  - Unique  
  - Check  
  - Not Null  

- **Joins**  
  - INNER JOIN  
  - LEFT JOIN  
  - RIGHT JOIN  
  - FULL OUTER JOIN  
  - CROSS JOIN  
  - SELF JOIN  
  - NATURAL JOIN  

- **Subqueries**  
  - Scalar Subquery  
  - Correlated Subquery  
  - Inline Views  

- **Set Operations**  
  - UNION  
  - UNION ALL  
  - INTERSECT  
  - MINUS  

- **Aggregations**  
  - COUNT, SUM, AVG, MIN, MAX  
  - GROUP BY  
  - HAVING  

- **Analytical & Window Functions**  
  - ROW_NUMBER()  
  - RANK(), DENSE_RANK()  
  - LEAD(), LAG()  
  - PARTITION BY  

- **Indexes**  
  - B-Tree Index  
  - Bitmap Index  
  - Function-Based Index  

- **Transactions**  
  - ACID Properties  
  - Savepoints  
  - Isolation Levels  

- **Views & Materialized Views**  
  - Creating Views  
  - Updating Views  
  - Refreshing Materialized Views  

- **Common Table Expressions (CTEs)**  
  - Recursive CTEs  
  - Non-Recursive CTEs  

- **PL/SQL**  
  - Anonymous Blocks  
  - Stored Procedures  
  - Functions  
  - Packages  
  - Exception Handling  

- **Triggers**  
  - BEFORE & AFTER Triggers  
  - Row-Level & Statement-Level Triggers  

- **Sequences & Synonyms**  
  - Auto-Increment Using Sequences  
  - Public & Private Synonyms  

- **Performance Optimization**  
  - Query Execution Plan  
  - Index Optimization  
  - Hints  

- **Partitioning**  
  - Range Partitioning  
  - List Partitioning  
  - Hash Partitioning  

- **Flashback & Recovery**  
  - Flashback Query  
  - Undo Management  

- **Security**  
  - Role Management  
  - Virtual Private Database (VPD)  
  - Data Redaction  

---

## Oracle SQL Concepts and Subconcepts  

### Basic Concepts  
- **SQL Syntax**  
  - Keywords  
  - Identifiers (Table Names, Column Names)  
  - Literals  
  - Comments (Single-line, Multi-line)  

- **Data Types**  
  - Character Data Types (`CHAR`, `VARCHAR2`, `CLOB`)  
  - Numeric Data Types (`NUMBER`, `FLOAT`)  
  - Date and Time Data Types (`DATE`, `TIMESTAMP`, `INTERVAL`)  
  - Large Object Data Types (`BLOB`, `BFILE`)  

- **Operators**  
  - Arithmetic Operators (`+`, `-`, `*`, `/`)  
  - Comparison Operators (`=`, `!=`, `<`, `>`, `<=`, `>=`)  
  - Logical Operators (`AND`, `OR`, `NOT`)  
  - Set Operators (`UNION`, `INTERSECT`, `MINUS`)  
  - String Operators (`||`, `CONCAT`)  

### Database Objects  
- **Tables**  
  - Creating Tables  
  - Modifying Tables (`ALTER TABLE`)  
  - Dropping Tables  
  - Temporary Tables  

- **Views**  
  - Creating Views  
  - Updatable Views  
  - Materialized Views  

- **Indexes**  
  - B-Tree Indexes  
  - Bitmap Indexes  
  - Function-Based Indexes  
  - Unique Indexes  

- **Sequences**  
  - Creating Sequences  
  - Using Sequences in Queries  

- **Synonyms**  
  - Public Synonyms  
  - Private Synonyms  

- **Schemas**  
  - User Schemas  
  - Accessing Objects Across Schemas  

### Data Manipulation  
- **DML Commands**  
  - `SELECT` (Basic Queries, Filtering, Sorting, Aggregations)  
  - `INSERT`  
  - `UPDATE`  
  - `DELETE`  
  - `MERGE`  

- **Transaction Control**  
  - `COMMIT`  
  - `ROLLBACK`  
  - `SAVEPOINT`  

### Data Definition  
- **DDL Commands**  
  - `CREATE` (Tables, Views, Indexes)  
  - `ALTER`  
  - `DROP`  
  - `TRUNCATE`  

### Data Control  
- **DCL Commands**  
  - `GRANT`  
  - `REVOKE`  

### Query Features  
- **Joins**  
  - Inner Joins  
  - Outer Joins (Left, Right, Full)  
  - Cross Joins  
  - Self Joins  

- **Subqueries**  
  - Single-Row Subqueries  
  - Multi-Row Subqueries  
  - Correlated Subqueries  
  - Inline Views  

- **Set Operations**  
  - `UNION`, `UNION ALL`  
  - `INTERSECT`  
  - `MINUS`  

- **Group By Features**  
  - `GROUP BY`  
  - `HAVING`  
  - Rollups and Cubes  

- **Analytical Functions**  
  - Ranking Functions (`RANK`, `DENSE_RANK`, `ROW_NUMBER`)  
  - Aggregate Functions (`SUM`, `AVG`, `MAX`, `MIN`, `COUNT`)  
  - Windowing Functions (`OVER`, `PARTITION BY`, `ORDER BY`)  

### Advanced Features  
- **PL/SQL Integration**  
  - Anonymous Blocks  
  - Stored Procedures  
  - Functions  
  - Triggers  
  - Packages  

- **Advanced Query Features**  
  - Hierarchical Queries (`CONNECT BY`)  
  - Pivot and Unpivot Queries  
  - JSON Functions (`JSON_OBJECT`, `JSON_TABLE`)  

- **Database Links**  
  - Creating Database Links  
  - Querying Remote Databases  

- **User-Defined Data Types**  
  - Object Types  
  - Collections (`VARRAY`, Nested Tables)  

### Security and Management  
- **User Management**  
  - Creating Users  
  - Altering Users  
  - Dropping Users  

- **Privileges and Roles**  
  - System Privileges  
  - Object Privileges  
  - Roles  

- **Auditing**  
  - Standard Auditing  
  - Fine-Grained Auditing  

### Performance Optimization  
- **Explain Plan**  
  - Understanding Execution Plans  
  - Using Hints (`/*+ HINT */`)  

- **Partitioning**  
  - Range Partitioning  
  - List Partitioning  
  - Hash Partitioning  

- **Optimizer**  
  - Cost-Based Optimizer (CBO)  
  - Rule-Based Optimizer (RBO)  

### Backup and Recovery  
- **Backup Methods**  
  - Logical Backups (Export/Import)  
  - Physical Backups (RMAN)  

- **Recovery Scenarios**  
  - Instance Recovery  
  - Media Recovery  
