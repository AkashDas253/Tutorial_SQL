## Window (Analytic) Functions in T-SQL

**Window functions** (also called **analytic functions**) in **T-SQL** perform calculations across a set of table rows that are **related to the current row**, without collapsing the rows into a single summary result.
They extend aggregate capabilities while preserving the **row-by-row output**.

---

### Core Characteristics

* Operate over a “window” or **subset of rows** defined by `OVER()` clause.
* Do **not reduce** rows like aggregate functions with `GROUP BY`.
* Can compute **running totals**, **ranks**, **percentiles**, **moving averages**, etc.
* Can be used in **SELECT**, **ORDER BY**, and **HAVING** clauses (but not in `WHERE`).

---

### General Syntax

```sql
<function_name> ( [expression] )  
OVER ( 
    [PARTITION BY column_list]  
    [ORDER BY column_list [ASC|DESC]]  
    [ROWS or RANGE frame_specification]
)
```

#### Parameters

| Element          | Description                                                         |
| ---------------- | ------------------------------------------------------------------- |
| **PARTITION BY** | Divides result set into groups (“window partitions”).               |
| **ORDER BY**     | Orders rows within each partition.                                  |
| **ROWS / RANGE** | Defines subset of rows relative to the current row for calculation. |

---

### Types of Window Functions

| Category                       | Description                                         | Examples                                            |
| ------------------------------ | --------------------------------------------------- | --------------------------------------------------- |
| **Aggregate Window Functions** | Perform aggregate operations over a window of rows. | `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()`       |
| **Ranking Functions**          | Assign rank/order values to rows.                   | `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `NTILE()` |
| **Value Functions**            | Access values from other rows in the window.        | `LAG()`, `LEAD()`, `FIRST_VALUE()`, `LAST_VALUE()`  |
| **Distribution Functions**     | Provide statistical ranking or percentiles.         | `PERCENT_RANK()`, `CUME_DIST()`                     |

---

### 1. Aggregate Window Functions

Perform aggregations while retaining each row.

#### Example

```sql
SELECT 
    Department,
    EmployeeName,
    Salary,
    SUM(Salary) OVER (PARTITION BY Department) AS DeptTotal,
    AVG(Salary) OVER (PARTITION BY Department) AS DeptAvg
FROM Employees;
```

Output: Each employee row shows department total and average salaries.

---

### 2. Ranking Functions

#### **ROW_NUMBER()** — Sequential Row Number

```sql
ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC)
```

→ Gives a unique number per partition ordered by salary.

---

#### **RANK()** — Ranking with Gaps

```sql
RANK() OVER (ORDER BY Salary DESC)
```

→ Equal salaries get same rank; next rank is skipped.

| Salary | RANK() |
| ------ | ------ |
| 90000  | 1      |
| 90000  | 1      |
| 85000  | 3      |

---

#### **DENSE_RANK()** — Ranking Without Gaps

```sql
DENSE_RANK() OVER (ORDER BY Salary DESC)
```

| Salary | DENSE_RANK() |
| ------ | ------------ |
| 90000  | 1            |
| 90000  | 1            |
| 85000  | 2            |

---

#### **NTILE(n)** — Divide Rows into Equal Buckets

```sql
NTILE(4) OVER (ORDER BY Salary DESC)
```

→ Divides rows into 4 quartiles based on order.

---

### 3. Value Functions

#### **LAG()** — Access Previous Row

```sql
LAG(Salary, 1, 0) OVER (ORDER BY HireDate)
```

→ Returns previous row’s salary; `0` if none exists.

---

#### **LEAD()** — Access Next Row

```sql
LEAD(Salary, 1, NULL) OVER (ORDER BY HireDate)
```

→ Returns next row’s salary.

---

#### **FIRST_VALUE()** and **LAST_VALUE()**

```sql
FIRST_VALUE(Salary) OVER (ORDER BY HireDate ASC)
LAST_VALUE(Salary) OVER (ORDER BY HireDate ASC ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
```

→ Returns first and last salary in the ordered window.

> Note: Use explicit frame (`ROWS BETWEEN ...`) with `LAST_VALUE()` to avoid limiting scope to current row.

---

### 4. Distribution Functions

#### **PERCENT_RANK()** — Relative Rank Between 0 and 1

```sql
PERCENT_RANK() OVER (ORDER BY Salary)
```

→ `(Rank - 1) / (TotalRows - 1)`

---

#### **CUME_DIST()** — Cumulative Distribution

```sql
CUME_DIST() OVER (ORDER BY Salary)
```

→ Fraction of rows with value ≤ current row’s value.

---

### 5. Frame Specifications

Used in `ROWS` or `RANGE` to define how far backward/forward the window extends.

#### Syntax

```sql
ROWS | RANGE BETWEEN 
    UNBOUNDED PRECEDING AND CURRENT ROW
```

| Clause                        | Description                      |
| ----------------------------- | -------------------------------- |
| `UNBOUNDED PRECEDING`         | From first row of partition      |
| `CURRENT ROW`                 | Up to current row                |
| `UNBOUNDED FOLLOWING`         | To last row of partition         |
| `N PRECEDING` / `N FOLLOWING` | Limited frame around current row |

#### Example — Running Total

```sql
SUM(SalesAmount) OVER (
    PARTITION BY Region
    ORDER BY SaleDate
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
) AS RunningTotal
```

---

### 6. Combining Multiple Window Functions

```sql
SELECT 
    EmployeeID,
    Department,
    Salary,
    SUM(Salary) OVER (PARTITION BY Department) AS DeptTotal,
    ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) AS RankInDept,
    LAG(Salary) OVER (PARTITION BY Department ORDER BY Salary) AS PrevSalary
FROM Employees;
```

---

### 7. ORDER OF EXECUTION

| Step | Operation                               |
| ---- | --------------------------------------- |
| 1    | FROM / JOIN                             |
| 2    | WHERE                                   |
| 3    | GROUP BY                                |
| 4    | HAVING                                  |
| 5    | SELECT (Window functions computed here) |
| 6    | ORDER BY                                |

---

### 8. Window Function Performance

* Use **PARTITION BY** wisely — large partitions can slow performance.
* Use **indexes** on `ORDER BY` columns to improve efficiency.
* Prefer **ROWS** over **RANGE** for deterministic windowing.
* Avoid using **non-deterministic functions** (like `NEWID()`) inside window expressions.

---

### 9. Example — Ranking and Running Totals

```sql
SELECT 
    Department,
    EmployeeName,
    Salary,
    RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS RankInDept,
    SUM(Salary) OVER (PARTITION BY Department ORDER BY Salary DESC 
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS RunningTotal
FROM Employees;
```

---

### 10. Example — Moving Average

```sql
SELECT 
    SaleDate,
    SalesAmount,
    AVG(SalesAmount) OVER (
        ORDER BY SaleDate 
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS MovingAvg
FROM Sales;
```

---

### Concept Diagram

```mermaid
flowchart TD;
    A[Dataset Rows] --> B[Apply PARTITION BY];
    B --> C[Apply ORDER BY within each partition];
    C --> D[Define ROWS or RANGE window];
    D --> E[Compute Window Function (e.g., SUM, RANK, LAG)];
    E --> F[Return result with each row preserved];
```

---

### 11. Differences Between GROUP BY and Window Functions

| Feature     | GROUP BY                    | Window Functions                       |
| ----------- | --------------------------- | -------------------------------------- |
| Output Rows | Collapsed                   | Preserved                              |
| Filtering   | Use `HAVING`                | Use `WHERE` or outer query             |
| Use Case    | Aggregation summaries       | Row-level analytics                    |
| Example     | `SUM(Salary) GROUP BY Dept` | `SUM(Salary) OVER (PARTITION BY Dept)` |

---

### Best Practices

* Always define **ORDER BY** for deterministic output.
* Explicitly declare frame range when needed.
* For large data, avoid nested window operations in one query.
* Combine window functions with **CTEs** for readability.
* Use for analytics, cumulative metrics, and real-time dashboards.

---
