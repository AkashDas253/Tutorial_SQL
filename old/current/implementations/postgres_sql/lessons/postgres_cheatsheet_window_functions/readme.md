## **PostgreSQL Window Functions: Comprehensive Cheatsheet**  

---
 
## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **Window Functions** | Perform calculations across a set of rows related to the current row. |
| **OVER() Clause** | Defines the partitioning and ordering of rows for window calculations. |
| **PARTITION BY** | Divides rows into subsets for independent calculations. |
| **ORDER BY** | Defines the order within each partition. |
| **Frame Clause** | Limits the range of rows considered in the calculation (default: entire partition). |

---

## **2. Common Window Functions**  
| Function | Description |
|----------|-------------|
| **RANK()** | Assigns a rank, allowing duplicate ranks (gaps exist). |
| **DENSE_RANK()** | Assigns a rank without gaps. |
| **ROW_NUMBER()** | Assigns a unique sequential number to each row. |
| **NTILE(n)** | Distributes rows into `n` equal groups. |
| **LEAD()** | Returns the next row’s value in order. |
| **LAG()** | Returns the previous row’s value in order. |
| **FIRST_VALUE()** | Returns the first value in the partition. |
| **LAST_VALUE()** | Returns the last value in the partition. |
| **CUME_DIST()** | Calculates cumulative distribution (percentile rank). |
| **PERCENT_RANK()** | Computes relative rank as a percentage. |
| **SUM() OVER** | Computes a cumulative sum. |
| **AVG() OVER** | Computes a moving average. |

---

## **3. Basic Syntax**  
```sql
SELECT 
    employee_id, department, salary,
    RANK() OVER(PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```
- **Partitions by `department`**
- **Ranks employees by `salary` within each department**

---

## **4. Ranking Functions**  
| Function | Example | Behavior |
|----------|---------|-----------|
| **RANK()** | `RANK() OVER (ORDER BY salary DESC)` | Gaps exist in ranking for duplicate values. |
| **DENSE_RANK()** | `DENSE_RANK() OVER (ORDER BY salary DESC)` | No gaps in ranking. |
| **ROW_NUMBER()** | `ROW_NUMBER() OVER (ORDER BY salary DESC)` | Unique sequence, even for duplicates. |

```sql
SELECT employee_id, salary, 
       RANK() OVER (ORDER BY salary DESC),
       DENSE_RANK() OVER (ORDER BY salary DESC),
       ROW_NUMBER() OVER (ORDER BY salary DESC)
FROM employees;
```

---

## **5. LEAD() & LAG()**  
```sql
SELECT 
    employee_id, salary,
    LAG(salary, 1) OVER (ORDER BY salary) AS prev_salary,
    LEAD(salary, 1) OVER (ORDER BY salary) AS next_salary
FROM employees;
```
- **LAG()** → Previous row’s salary  
- **LEAD()** → Next row’s salary  

---

## **6. FIRST_VALUE() & LAST_VALUE()**  
```sql
SELECT 
    employee_id, department, salary,
    FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary) AS lowest_salary,
    LAST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS highest_salary
FROM employees;
```
- **FIRST_VALUE()** → First salary in department  
- **LAST_VALUE()** → Last salary (entire partition must be defined)  

---

## **7. Moving Aggregates**  
| Function | Example | Description |
|----------|---------|-------------|
| **SUM() OVER** | `SUM(salary) OVER (PARTITION BY department ORDER BY salary ROWS BETWEEN 1 PRECEDING AND CURRENT ROW)` | Rolling sum. |
| **AVG() OVER** | `AVG(salary) OVER (PARTITION BY department ORDER BY salary ROWS BETWEEN 2 PRECEDING AND 1 FOLLOWING)` | Moving average. |

```sql
SELECT 
    employee_id, department, salary,
    SUM(salary) OVER (PARTITION BY department ORDER BY salary ROWS BETWEEN 1 PRECEDING AND CURRENT ROW) AS rolling_sum
FROM employees;
```

---

## **8. CUME_DIST() & PERCENT_RANK()**  
```sql
SELECT 
    employee_id, salary,
    CUME_DIST() OVER (ORDER BY salary) AS cumulative_distribution,
    PERCENT_RANK() OVER (ORDER BY salary) AS percent_rank
FROM employees;
```
- **CUME_DIST()** → Percent of values less than or equal to the current row  
- **PERCENT_RANK()** → Relative rank as a percentage  
