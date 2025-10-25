

# Single-column Index in MySQL

## Introduction

* An **index** is a database object that improves query performance by providing faster access to rows.
* A **single-column index** is created on **one column only**.
* MySQL uses **B-tree indexes** by default (InnoDB, MyISAM) for single-column indexes, but other types (HASH, FULLTEXT, SPATIAL) are also available depending on storage engine and column type.

---

## Syntax

### Create Index

```sql
CREATE INDEX index_name
ON table_name (column_name);
```

### Add Index via ALTER

```sql
ALTER TABLE table_name
ADD INDEX index_name (column_name);
```

### Drop Index

```sql
DROP INDEX index_name
ON table_name;
```

---

## Types of Single-column Indexes

| **Index Type**                 | **Syntax**                                             | **Use Case**                                              |
| ------------------------------ | ------------------------------------------------------ | --------------------------------------------------------- |
| Normal (non-unique)            | `CREATE INDEX idx_col ON table(col);`                  | Speeds up queries but allows duplicates & NULLs           |
| UNIQUE                         | `CREATE UNIQUE INDEX idx_col ON table(col);`           | Ensures all values are unique (like `UNIQUE` constraint)  |
| PRIMARY (special unique index) | Defined in `PRIMARY KEY (col)`                         | Enforces uniqueness & non-null, clustered index in InnoDB |
| FULLTEXT                       | `CREATE FULLTEXT INDEX idx_col ON table(col);`         | For text searching (`CHAR`, `VARCHAR`, `TEXT`)            |
| SPATIAL                        | `CREATE SPATIAL INDEX idx_col ON table(geometry_col);` | For spatial/geographic data (MyISAM/InnoDB with GIS)      |

---

## Characteristics

* Applies to a **single column** only.
* Index speeds up `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY` operations.
* Uses **B-tree structure** (except FULLTEXT and SPATIAL).
* Does not change query results, only performance.
* MySQL automatically creates indexes for:

  * `PRIMARY KEY` (single or composite)
  * `UNIQUE` constraints
  * `FOREIGN KEY` (on child column)

---

## Examples

### Example 1: Normal index

```sql
CREATE INDEX idx_name
ON employees (last_name);
```

✔ Speeds up lookups on `last_name`.

---

### Example 2: Unique index

```sql
CREATE UNIQUE INDEX idx_email
ON users (email);
```

✔ Prevents duplicate emails.

---

### Example 3: Add via ALTER

```sql
ALTER TABLE products
ADD INDEX idx_price (price);
```

---

### Example 4: Drop index

```sql
DROP INDEX idx_price
ON products;
```

---

### Example 5: FULLTEXT index

```sql
CREATE FULLTEXT INDEX idx_desc
ON articles (content);
```

✔ Enables fast text searching using `MATCH() AGAINST()`.

---

## Restrictions

* A table can have multiple single-column indexes (but too many hurt performance).
* Column data type must be supported by the index type:

  * `FULLTEXT` → only on `CHAR`, `VARCHAR`, `TEXT`.
  * `SPATIAL` → only on spatial types.
* Index length for `CHAR`/`VARCHAR`/`BLOB`/`TEXT` can be limited with prefix indexing. Example:

  ```sql
  CREATE INDEX idx_partname ON products(name(20));
  ```
* Storage engine must support the index type (InnoDB vs MyISAM differences).
* Write operations (`INSERT`, `UPDATE`, `DELETE`) may become slower with many indexes because indexes must be updated too.

---

## Usage Scenarios

* Speeding up queries on frequently searched columns.
* Enforcing uniqueness on specific attributes.
* Optimizing joins when column is used as a join condition.
* Supporting full-text search and spatial queries.

---

## Comparison: Single-column vs Multi-column Index

| **Aspect**         | **Single-column Index**                     | **Multi-column Index**                                    |
| ------------------ | ------------------------------------------- | --------------------------------------------------------- |
| Columns involved   | One                                         | Two or more                                               |
| Simplicity         | Easier to create/manage                     | More complex                                              |
| Query optimization | Best for queries filtering on single column | Best for queries filtering on multiple columns together   |
| Storage            | Less overhead                               | More storage needed                                       |
| Example            | `CREATE INDEX idx_name ON employees(name);` | `CREATE INDEX idx_name_dept ON employees(name, dept_id);` |

---
