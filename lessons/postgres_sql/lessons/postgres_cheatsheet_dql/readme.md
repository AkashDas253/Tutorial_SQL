# **PostgreSQL DQL (Data Query Language) Cheatsheet**  

## **Overview**  
DQL (Data Query Language) in PostgreSQL consists of SQL statements used to **retrieve data** from tables using `SELECT` queries. These queries can include filtering, sorting, grouping, and joining tables.

---

## **1. Basic SELECT Queries**  
| Action | Command |
|--------|---------|
| Select All Columns | `SELECT * FROM table_name;` |
| Select Specific Columns | `SELECT column1, column2 FROM table_name;` |
| Select with Alias | `SELECT column1 AS alias_name FROM table_name;` |
| Select with Expressions | `SELECT column1, (column2 * 2) AS new_column FROM table_name;` |
| Select Unique Values | `SELECT DISTINCT column FROM table_name;` |

#### **Example**
```sql
SELECT id, name AS employee_name FROM employees;
```

---

## **2. Filtering Data (WHERE Clause)**  
| Condition | Command Example |
|-----------|----------------|
| Equal to | `SELECT * FROM table_name WHERE column = value;` |
| Not Equal to | `SELECT * FROM table_name WHERE column <> value;` |
| Greater/Less Than | `SELECT * FROM table_name WHERE column > value;` |
| Between | `SELECT * FROM table_name WHERE column BETWEEN value1 AND value2;` |
| In List | `SELECT * FROM table_name WHERE column IN (value1, value2, value3);` |
| Like (Pattern) | `SELECT * FROM table_name WHERE column LIKE 'pattern%';` |
| Case-Insensitive Search | `SELECT * FROM table_name WHERE column ILIKE 'pattern%';` |
| Is NULL | `SELECT * FROM table_name WHERE column IS NULL;` |
| Is Not NULL | `SELECT * FROM table_name WHERE column IS NOT NULL;` |

#### **Example**
```sql
SELECT * FROM employees WHERE salary BETWEEN 50000 AND 80000;
```

---

## **3. Sorting Data (ORDER BY Clause)**  
| Action | Command |
|--------|---------|
| Ascending Order | `SELECT * FROM table_name ORDER BY column ASC;` |
| Descending Order | `SELECT * FROM table_name ORDER BY column DESC;` |
| Multiple Columns | `SELECT * FROM table_name ORDER BY column1 ASC, column2 DESC;` |
| Sort by Expression | `SELECT * FROM table_name ORDER BY column1 * column2 DESC;` |

#### **Example**
```sql
SELECT * FROM employees ORDER BY salary DESC, name ASC;
```

---

## **4. Limiting Results**  
| Action | Command |
|--------|---------|
| Limit Rows | `SELECT * FROM table_name LIMIT n;` |
| Offset Rows | `SELECT * FROM table_name OFFSET n;` |
| Limit with Offset | `SELECT * FROM table_name LIMIT n OFFSET m;` |

#### **Example**
```sql
SELECT * FROM employees ORDER BY salary DESC LIMIT 5 OFFSET 2;
```

---

## **5. Grouping & Aggregation (GROUP BY Clause)**  
| Function | Command Example |
|----------|----------------|
| Count | `SELECT column, COUNT(*) FROM table_name GROUP BY column;` |
| Sum | `SELECT column, SUM(column2) FROM table_name GROUP BY column;` |
| Average | `SELECT column, AVG(column2) FROM table_name GROUP BY column;` |
| Min/Max | `SELECT column, MIN(column2), MAX(column2) FROM table_name GROUP BY column;` |
| Group by Multiple Columns | `SELECT column1, column2, COUNT(*) FROM table_name GROUP BY column1, column2;` |

#### **Example**
```sql
SELECT department, AVG(salary) FROM employees GROUP BY department;
```

---

## **6. Filtering Groups (HAVING Clause)**  
| Action | Command |
|--------|---------|
| Filter Aggregates | `SELECT column, COUNT(*) FROM table_name GROUP BY column HAVING COUNT(*) > 10;` |

#### **Example**
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;
```

---

## **7. Joining Tables**  
| Type | Command Example |
|------|----------------|
| Inner Join | `SELECT * FROM t1 INNER JOIN t2 ON t1.id = t2.id;` |
| Left Join | `SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id;` |
| Right Join | `SELECT * FROM t1 RIGHT JOIN t2 ON t1.id = t2.id;` |
| Full Join | `SELECT * FROM t1 FULL JOIN t2 ON t1.id = t2.id;` |
| Cross Join | `SELECT * FROM t1 CROSS JOIN t2;` |
| Self Join | `SELECT e1.name, e2.name AS manager FROM employees e1 JOIN employees e2 ON e1.manager_id = e2.id;` |

#### **Example**
```sql
SELECT e.name, d.department_name 
FROM employees e 
INNER JOIN departments d ON e.department_id = d.id;
```

---

## **8. Subqueries**  
| Action | Command |
|--------|---------|
| Subquery in WHERE | `SELECT * FROM table1 WHERE column IN (SELECT column FROM table2);` |
| Subquery in FROM | `SELECT * FROM (SELECT column FROM table_name) AS sub;` |
| Subquery in SELECT | `SELECT column1, (SELECT MAX(column2) FROM table2) FROM table1;` |

#### **Example**
```sql
SELECT name, salary FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

## **9. Common Table Expressions (CTEs)**  
| Action | Command |
|--------|---------|
| Simple CTE | `WITH cte_name AS (SELECT column FROM table_name) SELECT * FROM cte_name;` |
| Recursive CTE | `WITH RECURSIVE cte_name AS (...) SELECT * FROM cte_name;` |

#### **Example**
```sql
WITH high_salary AS (
  SELECT * FROM employees WHERE salary > 70000
)
SELECT * FROM high_salary;
```

---

## **10. Window Functions**  
| Function | Command Example |
|----------|----------------|
| Rank | `SELECT column, RANK() OVER (PARTITION BY column ORDER BY column2 DESC) FROM table_name;` |
| Dense Rank | `SELECT column, DENSE_RANK() OVER (PARTITION BY column ORDER BY column2 DESC) FROM table_name;` |
| Row Number | `SELECT column, ROW_NUMBER() OVER (PARTITION BY column ORDER BY column2 DESC) FROM table_name;` |
| Running Total | `SELECT column, SUM(column2) OVER (PARTITION BY column ORDER BY column2) FROM table_name;` |

#### **Example**
```sql
SELECT name, department, salary, 
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```

---

## **Key Takeaways**  
- **DQL retrieves data** using `SELECT` queries.  
- **WHERE filters results**, while **ORDER BY sorts them**.  
- **LIMIT and OFFSET control pagination**.  
- **GROUP BY aggregates data**, and **HAVING filters groups**.  
- **Joins combine multiple tables**, and **subqueries enhance queries**.  
- **CTEs and window functions improve readability and efficiency**.  
