

# Simple Subquery in MySQL

## Introduction

* A **subquery** (or inner query) is a query nested inside another SQL statement.
* A **simple subquery** returns a single value or a single column of values to be used by the outer query.
* Often used in `WHERE`, `HAVING`, or `FROM` clauses.

---

## Syntax

```sql
SELECT column_list
FROM table
WHERE expr operator (subquery);
```

---

## Types of Simple Subqueries

### 1. Single-Row Subquery

* Returns exactly **one row and one column**.
* Used with single-value comparison operators.

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

**Operators allowed**: `=`, `>`, `<`, `>=`, `<=`, `<>`

---

### 2. Multiple-Row Subquery

* Returns **multiple rows in a single column**.
* Used with multi-value operators.

```sql
SELECT emp_id, name
FROM employees
WHERE dept_id IN (SELECT dept_id FROM departments WHERE location = 'NY');
```

**Operators allowed**:

* `IN` / `NOT IN`
* `ANY` / `SOME`
* `ALL`

---

### 3. Scalar Subquery

* Returns a **single value** (single row, single column).
* Can appear anywhere an expression is valid (e.g., `SELECT`, `WHERE`, `HAVING`).

```sql
SELECT emp_id, name, 
       (SELECT dept_name FROM departments d WHERE d.dept_id = e.dept_id) AS department
FROM employees e;
```

---

## Placement of Subqueries

| **Clause**             | **Usage**                                      |
| ---------------------- | ---------------------------------------------- |
| `WHERE`                | Filter rows based on subquery result           |
| `HAVING`               | Filter grouped rows using aggregate comparison |
| `FROM` (Derived Table) | Use subquery as a temporary table              |
| `SELECT`               | Return scalar values as columns                |

---

## Examples

### Subquery in WHERE

```sql
SELECT name
FROM employees
WHERE dept_id = (SELECT dept_id FROM departments WHERE dept_name = 'HR');
```

### Subquery with IN

```sql
SELECT name
FROM employees
WHERE dept_id IN (SELECT dept_id FROM departments WHERE location = 'London');
```

### Subquery in SELECT

```sql
SELECT name,
       (SELECT MAX(salary) FROM employees) AS highest_salary
FROM employees;
```

### Subquery in HAVING

```sql
SELECT dept_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept_id
HAVING AVG(salary) > (SELECT AVG(salary) FROM employees);
```

---

## Restrictions

* Subquery must be enclosed in parentheses.
* Must return the correct number of columns expected by the outer query.
* A single-row subquery cannot return multiple rows (will cause error).
* Performance may degrade if subquery runs for each row (consider joins instead).

---

## Usage Scenarios

* Comparing values against aggregated results.
* Filtering rows dynamically.
* Fetching values from related tables without explicit joins.
* Breaking complex logic into smaller steps.

---
