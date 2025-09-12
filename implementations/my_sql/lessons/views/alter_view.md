
# `ALTER VIEW` in MySQL

## Introduction

* `ALTER VIEW` is used to **modify an existing view** without dropping and recreating it manually.
* Equivalent to `CREATE OR REPLACE VIEW`.
* Useful when updating view definitions after schema or business rule changes.

---

## Syntax

```sql
ALTER [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
VIEW view_name [(column_list)] AS
select_statement
[WITH [CASCADED | LOCAL] CHECK OPTION];
```

---

## Components

### `ALGORITHM`

* Defines how MySQL processes the view:

  * `UNDEFINED` → MySQL decides automatically (default).
  * `MERGE` → Query merges with the outer query.
  * `TEMPTABLE` → Creates a temporary table to hold intermediate results.

### `view_name`

* The name of the view to be modified.
* Must exist in the schema.

### `(column_list)`

* Optional.
* Renames or reorders columns of the view output.

### `select_statement`

* The new query definition of the view.
* Same rules as `CREATE VIEW` apply:

  * Cannot contain invalid clauses (`LOCK`, `TEMPORARY`, etc.).
  * For updatable views, must follow update restrictions.

### `WITH CHECK OPTION`

* Controls insert/update behavior through the view:

  * `CASCADED` (default): Checks conditions of this view and underlying views.
  * `LOCAL`: Checks only this view’s condition.

---

## Examples

### Basic Alter

```sql
ALTER VIEW high_salary_emps AS
SELECT emp_id, name, salary
FROM employees
WHERE salary > 60000;
```

### Alter with Column List

```sql
ALTER VIEW dept_summary (dept_id, total_emps, avg_salary) AS
SELECT dept_id, COUNT(*), AVG(salary)
FROM employees
GROUP BY dept_id;
```

### Alter with Algorithm

```sql
ALTER ALGORITHM = TEMPTABLE VIEW emp_details AS
SELECT emp_id, dept_id, name, salary
FROM employees;
```

### Alter with Check Option

```sql
ALTER VIEW hr_emps AS
SELECT emp_id, dept_id
FROM employees
WHERE dept_id = 'HR'
WITH LOCAL CHECK OPTION;
```

---

## Restrictions

* Same as `CREATE VIEW`:

  * Cannot reference temporary tables.
  * Cannot use `LOCK`, `CALL`, `LOAD DATA`, `DO`, etc.
  * Cannot define recursive views (a view referencing itself).
* Cannot alter a view that does not exist (use `CREATE OR REPLACE VIEW` instead).
* Privileges:

  * Requires `CREATE VIEW` and `ALTER` privileges on the view.
  * Requires privileges on underlying tables/columns.

---

## Usage Scenarios

* **Schema change** → underlying table columns renamed/removed.
* **Business logic change** → new filtering condition or join added.
* **Performance tuning** → change algorithm (`MERGE` vs `TEMPTABLE`).
* **Security updates** → hide or expose different columns.

---

## Comparison with Related Commands

| **Command**              | **Purpose**                            |
| ------------------------ | -------------------------------------- |
| `CREATE VIEW`            | Defines a new view.                    |
| `CREATE OR REPLACE VIEW` | Creates new or replaces existing view. |
| `ALTER VIEW`             | Modifies existing view definition.     |
| `DROP VIEW`              | Removes a view.                        |

---
