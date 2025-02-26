## **PostgreSQL DQL (Data Query Language) Cheatsheet**  

#### **1. Basic SELECT Queries**  
| Action | Command |
|--------|---------|
| Select All Columns | `SELECT * FROM table_name;` |
| Select Specific Columns | `SELECT column1, column2 FROM table_name;` |
| Select with Alias | `SELECT column1 AS alias_name FROM table_name;` |

#### **2. Filtering Data (WHERE Clause)**  
| Condition | Command Example |
|-----------|----------------|
| Equal to | `SELECT * FROM table_name WHERE column = value;` |
| Not Equal to | `SELECT * FROM table_name WHERE column <> value;` |
| Greater/Less Than | `SELECT * FROM table_name WHERE column > value;` |
| Between | `SELECT * FROM table_name WHERE column BETWEEN value1 AND value2;` |
| In List | `SELECT * FROM table_name WHERE column IN (value1, value2, value3);` |
| Like (Pattern) | `SELECT * FROM table_name WHERE column LIKE 'pattern%';` |
| Is NULL | `SELECT * FROM table_name WHERE column IS NULL;` |

#### **3. Sorting Data (ORDER BY Clause)**  
| Action | Command |
|--------|---------|
| Ascending Order | `SELECT * FROM table_name ORDER BY column ASC;` |
| Descending Order | `SELECT * FROM table_name ORDER BY column DESC;` |
| Multiple Columns | `SELECT * FROM table_name ORDER BY column1 ASC, column2 DESC;` |

#### **4. Limiting Results**  
| Action | Command |
|--------|---------|
| Limit Rows | `SELECT * FROM table_name LIMIT n;` |
| Offset Rows | `SELECT * FROM table_name OFFSET n;` |
| Limit with Offset | `SELECT * FROM table_name LIMIT n OFFSET m;` |

#### **5. Grouping & Aggregation (GROUP BY Clause)**  
| Function | Command Example |
|----------|----------------|
| Count | `SELECT column, COUNT(*) FROM table_name GROUP BY column;` |
| Sum | `SELECT column, SUM(column2) FROM table_name GROUP BY column;` |
| Average | `SELECT column, AVG(column2) FROM table_name GROUP BY column;` |
| Min/Max | `SELECT column, MIN(column2), MAX(column2) FROM table_name GROUP BY column;` |

#### **6. Filtering Groups (HAVING Clause)**  
| Action | Command |
|--------|---------|
| Filter Aggregates | `SELECT column, COUNT(*) FROM table_name GROUP BY column HAVING COUNT(*) > 10;` |

#### **7. Joining Tables**  
| Type | Command Example |
|------|----------------|
| Inner Join | `SELECT * FROM t1 INNER JOIN t2 ON t1.id = t2.id;` |
| Left Join | `SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id;` |
| Right Join | `SELECT * FROM t1 RIGHT JOIN t2 ON t1.id = t2.id;` |
| Full Join | `SELECT * FROM t1 FULL JOIN t2 ON t1.id = t2.id;` |

#### **8. Subqueries**  
| Action | Command |
|--------|---------|
| Subquery in WHERE | `SELECT * FROM table1 WHERE column IN (SELECT column FROM table2);` |
| Subquery in FROM | `SELECT * FROM (SELECT column FROM table_name) AS sub;` |
