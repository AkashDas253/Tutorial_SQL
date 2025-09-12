

# Scalar Subquery in MySQL

## Introduction

* A **scalar subquery** is a subquery that returns a **single value** (exactly **one row and one column**).
* Can be used **anywhere an expression is allowed** (e.g., `SELECT`, `WHERE`, `HAVING`, `ORDER BY`).
* If the subquery returns no rows → result is `NULL`.
* If the subquery returns more than one row → error occurs (`Subquery returns more than 1 row`).

---

## Syntax

```sql
-- In WHERE
SELECT column_list
FROM table
WHERE column operator (SELECT single_column FROM table WHERE condition);

-- In SELECT
SELECT column_list,
       (SELECT single_column FROM table WHERE condition) AS alias
FROM table;

-- In HAVING
SELECT group_col, AVG(col)
FROM table
GROUP BY group_col
HAVING AVG(col) > (SELECT AVG(col) FROM table);
```

---

## Placement of Scalar Subqueries

| **Clause** | **Usage**                                    | **Example**                                                                                                                  |
| ---------- | -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `SELECT`   | Return a single computed value as a column   | `sql SELECT name, (SELECT dept_name FROM departments d WHERE d.dept_id = e.dept_id) AS department FROM employees e; `        |
| `WHERE`    | Filter rows based on a single value          | `sql SELECT name FROM employees WHERE salary > (SELECT AVG(salary) FROM employees); `                                        |
| `HAVING`   | Compare aggregate values with a single value | `sql SELECT dept_id, AVG(salary) FROM employees GROUP BY dept_id HAVING AVG(salary) > (SELECT AVG(salary) FROM employees); ` |
| `ORDER BY` | Sort rows by a single computed value         | `sql SELECT name FROM employees ORDER BY (SELECT MAX(salary) FROM employees); `                                              |

---

## Examples

### Example 1: Scalar Subquery in WHERE

```sql
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### Example 2: Scalar Subquery in SELECT

```sql
SELECT e.name,
       (SELECT dept_name FROM departments d WHERE d.dept_id = e.dept_id) AS department
FROM employees e;
```

### Example 3: Scalar Subquery in HAVING

```sql
SELECT dept_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept_id
HAVING AVG(salary) > (SELECT AVG(salary) FROM employees);
```

### Example 4: Scalar Subquery in ORDER BY

```sql
SELECT name
FROM employees
ORDER BY (SELECT MAX(salary) FROM employees) DESC;
```

---

## Characteristics

* Always returns a **single value**.
* Can appear in almost any SQL clause.
* Automatically returns `NULL` if no rows match.
* Errors if multiple rows are returned.

---

## Restrictions

* Must return **exactly one row and one column** (or `NULL`).
* If multiple rows are returned → error: *Subquery returns more than 1 row*.
* Should not be used when multiple results are expected → use **IN, ANY, ALL, or JOIN** instead.

---

## Usage Scenarios

* Fetching aggregated values for comparison.
* Returning computed fields without creating joins.
* Using global constants (like max/min values) inside queries.
* Applying row-by-row transformations via correlated scalar subqueries.

---
