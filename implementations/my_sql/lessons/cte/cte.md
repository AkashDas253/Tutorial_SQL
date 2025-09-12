

# Common Table Expressions (CTE) in MySQL

## Introduction

* A **CTE** is a temporary named result set that exists only during query execution.
* Introduced in **MySQL 8.0+**.
* Similar to a derived table or subquery but with **better readability and reusability**.
* Defined using the `WITH` clause before the main query.

---

## Syntax

```sql
WITH [RECURSIVE] cte_name [(column_list)] AS (
    cte_query
)
[ , cte_name2 [(column_list)] AS (
    cte_query2
) ... ]
main_query;
```

### Components

* `WITH` → starts the CTE definition.
* `RECURSIVE` → enables recursive CTEs.
* `cte_name` → alias for the temporary result set.
* `column_list` → optional, names for CTE output columns.
* `cte_query` → SELECT query defining the CTE.
* Multiple CTEs can be defined, separated by commas.
* `main_query` → final query that uses the CTE(s).

---

## Types of CTEs

### 1. Non-Recursive CTE

* Acts like a named subquery.
* Used for readability and reusability.
* Example:

```sql
WITH dept_salary AS (
    SELECT dept_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY dept_id
)
SELECT e.emp_id, e.salary, d.avg_salary
FROM employees e
JOIN dept_salary d ON e.dept_id = d.dept_id;
```

---

### 2. Recursive CTE

* Self-referential CTE to work with hierarchical/recursive data.
* Requires `WITH RECURSIVE`.
* Has **two parts**:

  * **Anchor query** → starting point
  * **Recursive query** → refers to CTE name
* Union of anchor + recursive queries.
* Stops when recursive part returns no rows.

#### Example: Hierarchical Employee Tree

```sql
WITH RECURSIVE emp_hierarchy AS (
    -- Anchor member
    SELECT emp_id, manager_id, name, 1 AS level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive member
    SELECT e.emp_id, e.manager_id, e.name, eh.level + 1
    FROM employees e
    JOIN emp_hierarchy eh ON e.manager_id = eh.emp_id
)
SELECT * FROM emp_hierarchy;
```

---

## Key Features

* Improves **query readability** compared to nested subqueries.
* **Reusability**: Can be referenced multiple times within main query.
* **Multiple CTEs** can be chained together.
* Used for **recursive hierarchies**, **data transformations**, **complex joins**, etc.
* Scope is **only within the query** in which it is defined (not persistent).

---

## Restrictions

* Must appear at the start of the statement.
* Not materialized permanently (unlike views).
* Cannot be indexed (since temporary).
* Recursive CTE must use **`UNION ALL`** (not just `UNION`).
* Recursive part must reference the CTE **exactly once**.

---

## Usage Scenarios

* **Simplifying complex subqueries**.
* **Hierarchical queries** (org charts, category trees).
* **Graph traversal**.
* **Breaking down transformations** step by step.
* **Reusing intermediate results** across multiple joins.

---

## Example with Multiple CTEs

```sql
WITH dept_avg AS (
    SELECT dept_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY dept_id
),
high_salary AS (
    SELECT emp_id, salary, dept_id
    FROM employees
    WHERE salary > 50000
)
SELECT h.emp_id, h.salary, d.avg_salary
FROM high_salary h
JOIN dept_avg d ON h.dept_id = d.dept_id;
```

---

## Comparison with Alternatives

| **Feature**            | **CTE** | **Derived Table** | **View**                             |
| ---------------------- | ------- | ----------------- | ------------------------------------ |
| Defined in query       | Yes     | Yes               | No                                   |
| Persistent             | No      | No                | Yes                                  |
| Reusable in same query | Yes     | No                | Yes                                  |
| Recursive support      | Yes     | No                | No                                   |
| Index support          | No      | No                | Yes (materialized views in some DBs) |

---

## Syntax Variations

### Basic

```sql
WITH cte AS (SELECT ... )
SELECT ... FROM cte;
```

### Recursive

```sql
WITH RECURSIVE cte AS (
    anchor_query
    UNION ALL
    recursive_query
)
SELECT ... FROM cte;
```

### Multiple CTEs

```sql
WITH cte1 AS (...),
     cte2 AS (...)
SELECT ... FROM cte1 JOIN cte2;
```

---
