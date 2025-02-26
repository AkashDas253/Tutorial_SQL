## **PostgreSQL DML (Data Manipulation Language) Cheatsheet**  

#### **1. Insert Data**  
| Action | Command |
|--------|---------|
| Insert Single Row | `INSERT INTO table_name (column1, column2) VALUES (value1, value2);` |
| Insert Multiple Rows | `INSERT INTO table_name (column1, column2) VALUES (value1, value2), (value3, value4);` |
| Insert from Another Table | `INSERT INTO table_name (column1, column2) SELECT column1, column2 FROM another_table;` |

#### **2. Update Data**  
| Action | Command |
|--------|---------|
| Update Specific Rows | `UPDATE table_name SET column1 = value WHERE condition;` |
| Update Multiple Columns | `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;` |
| Update All Rows | `UPDATE table_name SET column1 = value;` |

#### **3. Delete Data**  
| Action | Command |
|--------|---------|
| Delete Specific Rows | `DELETE FROM table_name WHERE condition;` |
| Delete All Rows | `DELETE FROM table_name;` (without `WHERE`) |
| Truncate Table (Faster) | `TRUNCATE TABLE table_name;` |

#### **4. Select Data**  
| Action | Command |
|--------|---------|
| Select All Columns | `SELECT * FROM table_name;` |
| Select Specific Columns | `SELECT column1, column2 FROM table_name;` |
| Select with Condition | `SELECT * FROM table_name WHERE condition;` |
| Select Distinct Values | `SELECT DISTINCT column FROM table_name;` |
| Select with Sorting | `SELECT * FROM table_name ORDER BY column ASC/DESC;` |
| Select with Limit | `SELECT * FROM table_name LIMIT n;` |

#### **5. Joins**  
| Type | Command Example |
|------|----------------|
| Inner Join | `SELECT * FROM t1 INNER JOIN t2 ON t1.id = t2.id;` |
| Left Join | `SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id;` |
| Right Join | `SELECT * FROM t1 RIGHT JOIN t2 ON t1.id = t2.id;` |
| Full Join | `SELECT * FROM t1 FULL JOIN t2 ON t1.id = t2.id;` |

#### **6. Aggregate Functions**  
| Function | Usage |
|----------|-------|
| `COUNT(*)` | `SELECT COUNT(*) FROM table_name;` |
| `SUM(column)` | `SELECT SUM(column) FROM table_name;` |
| `AVG(column)` | `SELECT AVG(column) FROM table_name;` |
| `MIN(column)` | `SELECT MIN(column) FROM table_name;` |
| `MAX(column)` | `SELECT MAX(column) FROM table_name;` |
