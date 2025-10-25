## Aggregate Functions in T-SQL

**Aggregate functions** in **T-SQL (Transact-SQL)** perform calculations on multiple rows of a dataset and return a **single summarized value**. These functions are primarily used with **GROUP BY**, **HAVING**, and **SELECT** statements to derive insights from large data collections.

---

### Core Characteristics

* Operate on a set of values, returning one result per group.
* Often used with **GROUP BY** for grouped aggregation.
* Ignore `NULL` values unless specified otherwise.
* Can be combined with **DISTINCT** to eliminate duplicates.
* Cannot be directly used in **WHERE** (use **HAVING** instead).

---

### Common Aggregate Functions

| Function               | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `AVG()`                | Calculates the average of non-null numeric values.           |
| `SUM()`                | Returns the total sum of non-null numeric values.            |
| `MIN()`                | Returns the smallest value in a set.                         |
| `MAX()`                | Returns the largest value in a set.                          |
| `COUNT()`              | Counts rows or non-null values.                              |
| `COUNT_BIG()`          | Like `COUNT()` but returns `BIGINT` (used for large tables). |
| `VAR()` / `VARP()`     | Computes variance (sample/population).                       |
| `STDEV()` / `STDEVP()` | Computes standard deviation (sample/population).             |
| `CHECKSUM_AGG()`       | Returns checksum of all values (for change tracking).        |

---

### 1. **AVG()** — Average Value

#### Syntax

```sql
AVG([DISTINCT] expression)
```

#### Example

```sql
SELECT AVG(Salary) AS AvgSalary
FROM Employees
WHERE Department = 'Finance';
```

With DISTINCT:

```sql
SELECT AVG(DISTINCT Salary) FROM Employees;
```

---

### 2. **SUM()** — Total Sum

#### Syntax

```sql
SUM([DISTINCT] expression)
```

#### Example

```sql
SELECT SUM(Quantity) AS TotalSold
FROM Orders
WHERE ProductID = 101;
```

---

### 3. **MIN()** and **MAX()** — Minimum and Maximum

#### Syntax

```sql
MIN(expression)
MAX(expression)
```

#### Example

```sql
SELECT 
    MIN(Salary) AS MinSalary,
    MAX(Salary) AS MaxSalary
FROM Employees;
```

---

### 4. **COUNT()** — Count of Rows or Values

#### Syntax

```sql
COUNT({ * | [DISTINCT] expression })
```

#### Examples

Count all rows (including NULLs):

```sql
SELECT COUNT(*) FROM Orders;
```

Count non-null values:

```sql
SELECT COUNT(Salary) FROM Employees;
```

Count distinct values:

```sql
SELECT COUNT(DISTINCT Department) FROM Employees;
```

---

### 5. **COUNT_BIG()** — Large-Scale Count

Returns **BIGINT** instead of **INT**. Used for very large datasets.

```sql
SELECT COUNT_BIG(*) AS TotalRows FROM LargeTable;
```

---

### 6. **VAR() / VARP()** — Variance

| Function | Description         |
| -------- | ------------------- |
| `VAR()`  | Sample variance     |
| `VARP()` | Population variance |

#### Syntax

```sql
VAR([DISTINCT] expression)
VARP([DISTINCT] expression)
```

Example:

```sql
SELECT VAR(Salary) AS SalaryVariance FROM Employees;
```

---

### 7. **STDEV() / STDEVP()** — Standard Deviation

| Function   | Description                   |
| ---------- | ----------------------------- |
| `STDEV()`  | Sample standard deviation     |
| `STDEVP()` | Population standard deviation |

#### Syntax

```sql
STDEV([DISTINCT] expression)
STDEVP([DISTINCT] expression)
```

Example:

```sql
SELECT STDEV(Salary) AS SalaryDeviation FROM Employees;
```

---

### 8. **CHECKSUM_AGG()** — Checksum Aggregation

Generates a checksum across a group of rows to detect data changes.

#### Syntax

```sql
CHECKSUM_AGG([DISTINCT] expression)
```

#### Example

```sql
SELECT CHECKSUM_AGG(BINARY_CHECKSUM(*)) AS DataHash FROM Employees;
```

---

### Using Aggregate Functions with GROUP BY

#### Example

```sql
SELECT 
    Department, 
    AVG(Salary) AS AvgSalary,
    COUNT(*) AS EmployeeCount,
    SUM(Salary) AS TotalSalary
FROM Employees
GROUP BY Department;
```

---

### Using HAVING with Aggregate Functions

Used for filtering results based on aggregated values (cannot use WHERE).

#### Example

```sql
SELECT Department, AVG(Salary) AS AvgSalary
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 70000;
```

---

### Combining Multiple Aggregate Functions

```sql
SELECT 
    COUNT(*) AS TotalEmployees,
    SUM(Salary) AS TotalSalary,
    AVG(Salary) AS AvgSalary,
    MAX(Salary) AS Highest,
    MIN(Salary) AS Lowest
FROM Employees;
```

---

### Aggregate Functions with NULL Handling

* All aggregate functions **ignore NULLs**, except `COUNT(*)`.
* To include or replace NULLs, use `ISNULL()` or `COALESCE()`.

Example:

```sql
SELECT AVG(ISNULL(Salary,0)) FROM Employees;
```

---

### Windowed Aggregates (With OVER Clause)

Aggregate functions can act as **window functions** using `OVER()` to compute results **without grouping rows**.

#### Example

```sql
SELECT 
    Department, 
    Salary,
    AVG(Salary) OVER (PARTITION BY Department) AS DeptAvg
FROM Employees;
```

---

### Best Practices

* Use **GROUP BY** for multi-row aggregation; **OVER()** for analytical queries.
* Replace NULLs before aggregation to avoid unintended exclusion.
* Avoid unnecessary DISTINCT inside aggregates for performance.
* Use `COUNT_BIG()` for very large datasets.
* Prefer **HAVING** for aggregated filtering, not WHERE.

---

### Aggregate Function Flow Diagram

```mermaid
flowchart TD;
    A[Data Rows] --> B[Apply WHERE Filter];
    B --> C[Group Data (GROUP BY)];
    C --> D[Apply Aggregate Functions];
    D --> E[Apply HAVING Filter];
    E --> F[Return Aggregated Results];
```

---
