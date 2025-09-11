# Handling Null

## NULL in SQL

* `NULL` represents **missing, unknown, or inapplicable data**.
* It is **not equal to zero or an empty string**.
* Any comparison with `NULL` (except `IS NULL` / `IS NOT NULL`) returns `UNKNOWN`.

---

## Three-Valued Logic (3VL)

SQL uses **TRUE, FALSE, UNKNOWN** when `NULL` is involved.

* Example: `5 = NULL` → `UNKNOWN`.
* Filtering: `WHERE condition` only selects rows where condition is **TRUE** (not FALSE or UNKNOWN).

---

## Testing NULL

* `IS NULL`: Check if a value is NULL.
* `IS NOT NULL`: Check if a value is not NULL.

```sql
SELECT * FROM employees WHERE manager_id IS NULL;
```

---

## Handling NULL in Expressions

* Arithmetic with `NULL` → `NULL`.
* String concatenation with `NULL` → `NULL`.

---

## Functions for NULL Handling

| Function                             | Purpose                                                |
| ------------------------------------ | ------------------------------------------------------ |
| `COALESCE(expr1, expr2, ..., exprN)` | Returns the first non-NULL expression.                 |
| `NULLIF(expr1, expr2)`               | Returns NULL if `expr1 = expr2`, else returns `expr1`. |
| `IFNULL(expr, alt)` *(MySQL)*        | Returns `alt` if `expr` is NULL.                       |
| `NVL(expr, alt)` *(Oracle)*          | Returns `alt` if `expr` is NULL.                       |

---

## Aggregate Functions and NULL

* `COUNT(column)` ignores NULLs.
* `SUM`, `AVG`, `MIN`, `MAX` ignore NULLs.
* `COUNT(*)` counts all rows, including rows with NULLs.

---

## Joins and NULL

* `INNER JOIN`: NULLs in key columns prevent matches.
* `LEFT JOIN`: NULLs appear in unmatched side.
* `NULL` does not equal `NULL` → equality joins skip NULL= NULL rows.

---

## Sorting with NULL

* `ORDER BY column ASC` → NULLs usually come last (DBMS-dependent).
* `ORDER BY column DESC` → NULLs usually come first.
* Control with:

  ```sql
  ORDER BY column ASC NULLS FIRST;
  ORDER BY column DESC NULLS LAST;
  ```

---

## Predicates and NULL

* `=`, `<`, `>`, `<>` with `NULL` → UNKNOWN.
* `IN` list containing NULL → may result in UNKNOWN.
* `NOT IN` with NULL → returns no rows (since condition is UNKNOWN).
* `BETWEEN`, `LIKE` with NULL → UNKNOWN.

---

## Constraints and NULL

* `PRIMARY KEY`: disallows NULL.
* `UNIQUE`: allows multiple NULLs (DBMS-dependent).
* `NOT NULL`: enforces non-NULL values.
* `CHECK`: if condition evaluates to UNKNOWN due to NULL, the row passes (treated as TRUE).

---

## Set Operations and NULL

* `UNION` considers `NULL` = `NULL` for duplicates removal.
* `INTERSECT` includes rows with `NULL` if they exist in both sets.
* `EXCEPT`/`MINUS` removes rows with `NULL` if matched.

---

## Indexing and NULL

* Index behavior depends on DBMS:

  * Some include NULL values in indexes.
  * Others exclude NULLs unless explicitly configured (e.g., `WHERE column IS NOT NULL` indexes).

---

## NULL in GROUP BY and DISTINCT

* `GROUP BY` treats all NULLs as one group.
* `DISTINCT` treats NULLs as equal, returning one NULL in the result set.

---

## NULL and CASE

```sql
CASE 
   WHEN column IS NULL THEN 'Missing'
   ELSE column
END
```

---

## NULL in Subqueries

* `EXISTS` with subquery unaffected by NULLs.
* `IN` with subquery containing NULL → may cause UNKNOWN.
* Use `NOT EXISTS` instead of `NOT IN` for safety with NULL.

---
