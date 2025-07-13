## **PostgreSQL Common Table Expressions (CTEs): Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **Common Table Expression (CTE)** | A temporary result set used within a query. |
| **WITH Clause** | Defines the CTE before the main query. |
| **Recursive CTE** | Enables hierarchical queries like trees and graphs. |
| **Multiple CTEs** | Supports defining multiple CTEs in one query. |
| **Readability & Performance** | Improves query organization but may not always optimize performance. |

---

## **2. Basic CTE Syntax**  
```sql
WITH cte_name AS (
    SELECT column1, column2 FROM table_name WHERE condition
)
SELECT * FROM cte_name;
```

---

## **3. Using Multiple CTEs**  
```sql
WITH cte1 AS (
    SELECT id, name FROM employees WHERE department = 'HR'
),
cte2 AS (
    SELECT id, salary FROM salaries WHERE salary > 50000
)
SELECT cte1.name, cte2.salary
FROM cte1
JOIN cte2 ON cte1.id = cte2.id;
```
- Defines multiple CTEs (`cte1`, `cte2`).  
- Uses them in the main `SELECT` query.  

---

## **4. Recursive CTEs**  
| Feature | Description |
|---------|-------------|
| **Recursive Queries** | Useful for hierarchical data (e.g., organizational charts, category trees). |
| **Anchor Query** | Initial set of rows (base case). |
| **Recursive Query** | Iterates using `UNION ALL`. |
| **Termination Condition** | Stops when no new rows are generated. |

### **Example: Employee Hierarchy**
```sql
WITH RECURSIVE employee_hierarchy AS (
    -- Anchor Query: Select the top-level employees
    SELECT id, name, manager_id, 1 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive Query: Select employees reporting to the previous level
    SELECT e.id, e.name, e.manager_id, eh.level + 1
    FROM employees e
    INNER JOIN employee_hierarchy eh ON e.manager_id = eh.id
)
SELECT * FROM employee_hierarchy;
```
- **Finds hierarchical employee relationships**  
- **Levels indicate depth in hierarchy**  

---

## **5. CTE vs. Subquery vs. Temporary Table**  
| Feature | CTE | Subquery | Temporary Table |
|---------|-----|----------|----------------|
| **Scope** | Exists only within query execution | Part of the same query | Exists in session |
| **Readability** | High | Low | Moderate |
| **Performance** | Can be optimized | May be repeated | Can be indexed |

---

## **6. Performance Considerations**  
| Optimization | Description |
|-------------|-------------|
| **Use `MATERIALIZED` (PostgreSQL 12+ Only)** | Forces CTE to be evaluated once and stored. |
| **Avoid Unnecessary CTEs** | Inlining subqueries may be more efficient. |
| **Index Key Columns** | Index columns used in joins within CTEs. |

### **Example: Materialized CTE**
```sql
WITH MATERIALIZED expensive_cte AS (
    SELECT * FROM large_table WHERE expensive_condition
)
SELECT * FROM expensive_cte WHERE another_condition;
```
- **Evaluated once and stored for reuse.**  
