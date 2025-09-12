
# `DROP VIEW` in MySQL

## Introduction

* `DROP VIEW` removes one or more views from the database.
* Only removes the **view definition**, not the underlying data.
* If the view does not exist, MySQL can throw an error unless `IF EXISTS` is used.

---

## Syntax

```sql
DROP VIEW [IF EXISTS]
    view_name [, view_name2, ...]
    [RESTRICT | CASCADE];
```

---

## Components

### `IF EXISTS`

* Prevents error if the specified view does not exist.
* Issues a **warning** instead.

### `view_name`

* Name of the view to drop.
* Multiple views can be dropped in a single statement, separated by commas.

### `RESTRICT` | `CASCADE`

* Present for SQL standard compliance; **ignored in MySQL**.
* MySQL always behaves as if `RESTRICT` is applied.

---

## Examples

### Drop a Single View

```sql
DROP VIEW high_salary_emps;
```

### Drop Multiple Views

```sql
DROP VIEW dept_summary, hr_emps;
```

### Drop with Safety Check

```sql
DROP VIEW IF EXISTS emp_details;
```

---

## Restrictions

* Cannot drop views that don’t exist unless `IF EXISTS` is used.
* Requires `DROP` privilege for each view.
* Dropping a view does **not affect the underlying tables** or data.
* If other views depend on the dropped view, those dependent views will become invalid.

---

## Usage Scenarios

* Removing outdated or unused views.
* Cleaning up development or test databases.
* Replacing with a new version (often used with `CREATE OR REPLACE VIEW`).

---

## Comparison with Related Commands

| **Command**              | **Purpose**               |
| ------------------------ | ------------------------- |
| `CREATE VIEW`            | Create a new view.        |
| `CREATE OR REPLACE VIEW` | Create or update a view.  |
| `ALTER VIEW`             | Modify an existing view.  |
| `DROP VIEW`              | Delete a view definition. |

---
