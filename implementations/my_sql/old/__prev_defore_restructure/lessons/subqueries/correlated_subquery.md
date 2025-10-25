

# Correlated Subquery in MySQL

## Introduction

* A **correlated subquery** is a subquery that **depends on values from the outer query**.
* The inner query is executed **once for each row** selected by the outer query.
* Different from a simple subquery, which runs only once and returns a result set used by the outer query.

---

## Syntax

```sql
SELECT column_list
FROM outer_table o
WHERE expr operator (
    SELECT column
    FROM inner_table i
    WHERE i.col = o.col
);
```

---

## How It Works

* The subquery is evaluated repeatedly, once for each row of the outer query.
* Uses **references to outer query columns** inside the subquery.

---

## Types of Correlated Subqueries

| **Type**                | **Description**                                     | **Example**                                                                                                                                   |
| ----------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **WHERE Correlation**   | Filters rows by checking conditions row-by-row      | `sql SELECT e1.name, e1.salary FROM employees e1 WHERE e1.salary > (SELECT AVG(e2.salary) FROM employees e2 WHERE e2.dept_id = e1.dept_id); ` |
| **SELECT Correlation**  | Uses outer query values inside subquery expressions | `sql SELECT e1.name, (SELECT COUNT(*) FROM employees e2 WHERE e2.manager_id = e1.emp_id) AS subordinates FROM employees e1; `                 |
| **EXISTS / NOT EXISTS** | Checks row existence per outer row                  | `sql SELECT d.dept_name FROM departments d WHERE EXISTS (SELECT 1 FROM employees e WHERE e.dept_id = d.dept_id); `                            |

---

## Operators Used with Correlated Subqueries

* `EXISTS` / `NOT EXISTS`
* `IN` / `NOT IN` (with correlation)
* `=`, `>`, `<`, `>=`, `<=`, `<>` (single-row comparisons)
* `ANY` / `ALL` with correlation

---

## Examples

### Example 1: Find employees earning more than the average salary in their department

```sql
SELECT e1.emp_id, e1.name, e1.salary
FROM employees e1
WHERE e1.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.dept_id = e1.dept_id
);
```

### Example 2: Find departments that have at least one employee

```sql
SELECT d.dept_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.dept_id = d.dept_id
);
```

### Example 3: Count employees per manager (subquery in SELECT)

```sql
SELECT m.name AS manager,
       (SELECT COUNT(*) 
        FROM employees e 
        WHERE e.manager_id = m.emp_id) AS num_employees
FROM employees m;
```

---

## Key Characteristics

* **Row-by-row evaluation** (less efficient than joins).
* **Outer query column references** are essential.
* Often used when **joins are not straightforward**.
* Commonly combined with `EXISTS`, `NOT EXISTS`.

---

## Restrictions

* Must return results matching the outer query context (e.g., scalar in single-value comparison).
* Performance can degrade heavily on large datasets (consider `JOIN` with aggregation instead).
* Cannot be optimized as easily as non-correlated subqueries.

---

## Usage Scenarios

* Comparing row values against aggregated/related subsets.
* Checking existence of related rows.
* Row-wise computations that cannot be done with simple joins.

---
