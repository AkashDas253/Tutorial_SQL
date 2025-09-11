

# Window Functions in MySQL

## Introduction

* Window functions perform calculations across a set of rows related to the current row.
* Unlike aggregate functions, they do not collapse rows; results are available per row.
* Operate using an **OVER()** clause to define a **window** (partition + order + frame).

---

## Syntax

```sql
function_name ([expression]) 
OVER (
    [PARTITION BY expr_list]   -- Divide rows into partitions
    [ORDER BY expr_list]       -- Define order of rows within each partition
    [frame_clause]             -- Limit the set of rows for calculation
)
```

---

## Frame Clause

```sql
ROWS | RANGE | GROUPS frame_start [frame_exclusion]
ROWS | RANGE | GROUPS BETWEEN frame_start AND frame_end [frame_exclusion]
```

### Frame Units

* `ROWS` → physical rows
* `RANGE` → logical range of values
* `GROUPS` → groups of peer rows

### Frame Boundaries

* `UNBOUNDED PRECEDING` → start from the first row
* `n PRECEDING` → n rows before
* `CURRENT ROW` → current row
* `n FOLLOWING` → n rows after
* `UNBOUNDED FOLLOWING` → last row

### Frame Exclusion

* `EXCLUDE CURRENT ROW`
* `EXCLUDE GROUP`
* `EXCLUDE TIES`
* `EXCLUDE NO OTHERS` (default)

---

## Categories of Window Functions

### 1. Aggregate Window Functions

Used with `OVER()` without collapsing rows.

* `SUM(expr)`
* `AVG(expr)`
* `MIN(expr)`
* `MAX(expr)`
* `COUNT(expr)`
* `BIT_AND(expr)`
* `BIT_OR(expr)`
* `BIT_XOR(expr)`
* `STDDEV_POP(expr)`
* `STDDEV_SAMP(expr)`
* `VAR_POP(expr)`
* `VAR_SAMP(expr)`

---

### 2. Ranking Functions

Assign ranks or numbers to rows.

* `ROW_NUMBER()` → sequential row number
* `RANK()` → rank with gaps
* `DENSE_RANK()` → rank without gaps
* `PERCENT_RANK()` → relative rank (0–1)
* `CUME_DIST()` → cumulative distribution
* `NTILE(n)` → distribute rows into n buckets

---

### 3. Value Functions

Access specific row values in a window.

* `FIRST_VALUE(expr)` → first value in frame
* `LAST_VALUE(expr)` → last value in frame
* `NTH_VALUE(expr, n)` → nth value in frame
* `LEAD(expr [, offset [, default]])` → value of following row
* `LAG(expr [, offset [, default]])` → value of preceding row

---

### 4. Navigation Functions

Used with ordering to calculate movements between rows.

* `NTH_VALUE()`
* `LAG()`
* `LEAD()`

---

### 5. Special Functions

* `JSON_ARRAYAGG(expr) OVER (...)`
* `JSON_OBJECTAGG(key, value) OVER (...)`

---

## Usage Scenarios

* **Analytics** → running totals, moving averages
* **Ranking** → top-N queries
* **Comparisons** → previous vs current row
* **Percentile/Distribution** → cumulative distribution analysis
* **Data exploration** → segmenting rows with partitions

---

## Example Syntaxes

### Running Total

```sql
SELECT 
    emp_id,
    salary,
    SUM(salary) OVER (PARTITION BY dept_id ORDER BY hire_date) AS running_total
FROM employees;
```

### Ranking

```sql
SELECT 
    emp_id,
    salary,
    RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS salary_rank
FROM employees;
```

### Lead/Lag

```sql
SELECT 
    emp_id,
    salary,
    LAG(salary, 1, 0) OVER (ORDER BY hire_date) AS prev_salary,
    LEAD(salary, 1, 0) OVER (ORDER BY hire_date) AS next_salary
FROM employees;
```

---

## Key Notes

* `OVER()` must be present; otherwise, the function acts as a normal aggregate.
* `PARTITION BY` is optional (default = entire result set).
* `ORDER BY` defines row sequence; essential for ranking, lead/lag, frame calculations.
* `FRAME` is optional but defaults differ:

  * Aggregate window functions: default is `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`.
  * Ranking functions: no frame (order only).

---

