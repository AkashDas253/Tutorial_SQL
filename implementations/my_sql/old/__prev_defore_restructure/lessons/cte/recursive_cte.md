

# Recursive CTE in MySQL

## Introduction

* A **Recursive CTE** is a CTE that references itself in its definition.
* Useful for **hierarchical data** (org charts, category trees, graph traversal, etc.).
* Defined with the **`WITH RECURSIVE`** keyword.

---

## Syntax

```sql
WITH RECURSIVE cte_name (column_list) AS (
    anchor_query
    UNION [ALL]
    recursive_query
)
SELECT * FROM cte_name;
```

### Components

* `cte_name` → name of the CTE.
* `(column_list)` → optional output column names.
* `anchor_query` → non-recursive base query.
* `recursive_query` → query that references `cte_name`.
* `UNION ALL` → required for recursion (to avoid removing duplicates).
* Recursion stops when recursive query returns **no new rows**.

---

## Working Principle

1. Run **anchor query** → produces initial result set.
2. Run **recursive query** using previous result set as input.
3. Append new rows using **UNION ALL**.
4. Repeat until no rows returned.
5. Final result = union of all iterations.

---

## Example 1: Employee Hierarchy

```sql
WITH RECURSIVE emp_hierarchy AS (
    -- Anchor: top-level managers
    SELECT emp_id, manager_id, name, 1 AS level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive: find direct reports
    SELECT e.emp_id, e.manager_id, e.name, eh.level + 1
    FROM employees e
    JOIN emp_hierarchy eh ON e.manager_id = eh.emp_id
)
SELECT * FROM emp_hierarchy;
```

📌 This builds a **tree of employees** with their hierarchy levels.

---

## Example 2: Number Sequence Generator

```sql
WITH RECURSIVE numbers AS (
    SELECT 1 AS n
    UNION ALL
    SELECT n + 1 FROM numbers WHERE n < 10
)
SELECT * FROM numbers;
```

📌 Generates numbers from **1 to 10**.

---

## Example 3: Category Tree

```sql
WITH RECURSIVE category_tree AS (
    SELECT category_id, parent_id, name, 1 AS level
    FROM categories
    WHERE parent_id IS NULL
    
    UNION ALL
    
    SELECT c.category_id, c.parent_id, c.name, ct.level + 1
    FROM categories c
    JOIN category_tree ct ON c.parent_id = ct.category_id
)
SELECT * FROM category_tree;
```

📌 Expands nested categories into a tree.

---

## Key Rules & Restrictions

* Must use `WITH RECURSIVE`.
* Recursive query must reference the CTE **exactly once**.
* Recursive query and anchor query must have **same number of columns** and **compatible types**.
* Recursive queries require **`UNION ALL`** (not just `UNION`).
* **Termination**:

  * Automatic when recursive query returns no rows.
  * Can also use conditions (`WHERE`, `LIMIT`) to prevent infinite recursion.
* Performance may degrade with very deep recursion.

---

## Usage Scenarios

* **Hierarchical Data** → Employees, categories, org charts.
* **Graph Traversal** → Paths in networks, relationships.
* **Number Generators** → Useful in test data generation.
* **Transitive Closures** → Finding all descendants/ancestors.
* **Path Finding** → Parent-to-child or child-to-parent navigation.

---

## Recursive CTE vs Iterative Methods

| **Aspect**   | **Recursive CTE**                                            | **Loop / Procedural Code**     |
| ------------ | ------------------------------------------------------------ | ------------------------------ |
| SQL Standard | Yes                                                          | No                             |
| Readability  | High                                                         | Medium                         |
| Performance  | Good for moderate depth                                      | Better for very deep recursion |
| Portability  | Supported in SQL standard (MySQL 8+, PostgreSQL, SQL Server) | DB-specific                    |

---
