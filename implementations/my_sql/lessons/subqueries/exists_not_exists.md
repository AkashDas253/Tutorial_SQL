

# EXISTS / NOT EXISTS in MySQL

## Introduction

* `EXISTS` and `NOT EXISTS` are **subquery operators** that check for the **existence of rows** returned by a subquery.
* They return **TRUE** or **FALSE**:

  * `EXISTS` → TRUE if the subquery returns **at least one row**.
  * `NOT EXISTS` → TRUE if the subquery returns **no rows**.
* Commonly used with **correlated subqueries**, where the inner query references columns from the outer query.

---

## Syntax

```sql
-- EXISTS
SELECT column_list
FROM outer_table o
WHERE EXISTS (
    SELECT 1
    FROM inner_table i
    WHERE i.col = o.col
);

-- NOT EXISTS
SELECT column_list
FROM outer_table o
WHERE NOT EXISTS (
    SELECT 1
    FROM inner_table i
    WHERE i.col = o.col
);
```

> Note:

* The subquery usually uses `SELECT 1` (or any constant) since only **row existence** matters, not the returned values.

---

## Behavior

* `EXISTS` stops searching once it finds the first matching row → efficient.
* `NOT EXISTS` checks that **no row** matches.
* Often used instead of `IN` or `JOIN` when handling `NULL` values.

---

## Examples

### Example 1: `EXISTS` – Departments with employees

```sql
SELECT d.dept_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.dept_id = d.dept_id
);
```

✔ Returns only departments that have employees.

---

### Example 2: `NOT EXISTS` – Departments without employees

```sql
SELECT d.dept_name
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.dept_id = d.dept_id
);
```

✔ Returns departments where no employees exist.

---

### Example 3: `EXISTS` with Correlated Condition

```sql
SELECT e1.name, e1.emp_id
FROM employees e1
WHERE EXISTS (
    SELECT 1
    FROM employees e2
    WHERE e2.manager_id = e1.emp_id
);
```

✔ Returns employees who manage at least one other employee.

---

### Example 4: `NOT EXISTS` with Correlated Condition

```sql
SELECT e1.name, e1.emp_id
FROM employees e1
WHERE NOT EXISTS (
    SELECT 1
    FROM employees e2
    WHERE e2.manager_id = e1.emp_id
);
```

✔ Returns employees who are **not managers**.

---

## EXISTS vs IN

* `EXISTS` is usually faster when the subquery returns a **large number of rows**.
* `IN` can be faster when the subquery returns a **small list**.
* `EXISTS` handles `NULL` values properly, while `IN` may fail with `NULL`.

---

## Restrictions

* Subquery must be enclosed in parentheses.
* Cannot directly return values (only checks row existence).
* Typically requires correlated subqueries for meaningful filtering.

---

## Usage Scenarios

* Checking if related data exists in another table.
* Returning rows only when matches exist in a child table.
* Filtering out rows that do not meet relational criteria.
* Avoiding issues with `NULL` values compared to `IN`.

---
