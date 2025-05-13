## 🧑‍⚖️ **SQL PIVOT and UNPIVOT**

### 1. **PIVOT Operation**

The `PIVOT` operator is used to rotate data from rows to columns, making it easier to summarize and analyze.

#### Basic PIVOT Syntax

```sql
-- Trick: Basic PIVOT operation to transform rows into columns
SELECT *
FROM (
    SELECT department, employee, salary
    FROM employees
) AS source
PIVOT (
    MAX(salary) FOR department IN ([HR], [IT], [Sales])
) AS pvt;
```

**Use when**: You need to transform distinct row values into column headers, like summarizing employee salaries by department.

---

### 2. **PIVOT with Aggregation**

```sql
-- Trick: Use PIVOT with aggregation functions (e.g., SUM, COUNT)
SELECT *
FROM (
    SELECT year, product, sales
    FROM sales_data
) AS source
PIVOT (
    SUM(sales) FOR product IN ([ProductA], [ProductB], [ProductC])
) AS pvt;
```

**Use when**: You want to summarize or aggregate data (like summing sales) across multiple categories, such as products or years.

---

### 3. **PIVOT with Dynamic Columns**

```sql
-- Trick: Use dynamic SQL for a dynamic PIVOT (when you don’t know the column values in advance)
DECLARE @columns AS NVARCHAR(MAX), @sql AS NVARCHAR(MAX);

-- Get the list of distinct products to pivot by
SELECT @columns = STRING_AGG(QUOTENAME(product), ',') FROM (SELECT DISTINCT product FROM sales_data) AS product_list;

-- Create dynamic SQL for pivot
SET @sql = 'SELECT year, ' + @columns + ' FROM (SELECT year, product, sales FROM sales_data) AS source PIVOT (SUM(sales) FOR product IN (' + @columns + ')) AS pvt;';
EXEC sp_executesql @sql;
```

**Use when**: You have a dynamic set of values (e.g., products) and want to pivot without knowing them in advance.

---

### 4. **PIVOT with Date-Based Data**

```sql
-- Trick: Use PIVOT for time-series data (like sales per month)
SELECT *
FROM (
    SELECT EXTRACT(MONTH FROM sale_date) AS month, product, sales
    FROM sales_data
) AS source
PIVOT (
    SUM(sales) FOR month IN ([1], [2], [3], [4], [5], [6], [7], [8], [9], [10], [11], [12])
) AS pvt;
```

**Use when**: You want to pivot data based on time, such as monthly sales for different products.

---

### 5. **PIVOT with Multiple Aggregation Functions**

```sql
-- Trick: Use multiple aggregation functions (e.g., SUM, COUNT) in a PIVOT
SELECT *
FROM (
    SELECT department, employee, salary, years_experience
    FROM employees
) AS source
PIVOT (
    SUM(salary) AS TotalSalary, COUNT(employee) AS EmployeeCount
    FOR department IN ([HR], [IT], [Sales])
) AS pvt;
```

**Use when**: You need multiple aggregated columns in the pivoted result, like total salary and employee count per department.

---

## 🔄 **SQL UNPIVOT Operation**

The `UNPIVOT` operator is used to transform columns into rows, essentially the reverse operation of `PIVOT`.

### 1. **Basic UNPIVOT Syntax**

```sql
-- Trick: Basic UNPIVOT operation to transform columns into rows
SELECT department, metric, value
FROM (
    SELECT department, hr, it, sales
    FROM employee_performance
) AS source
UNPIVOT (
    value FOR metric IN (hr, it, sales)
) AS unpvt;
```

**Use when**: You need to turn columns into rows to normalize data, such as transforming performance metrics into a more analysis-friendly format.

---

### 2. **UNPIVOT with Date-Based Data**

```sql
-- Trick: Use UNPIVOT for time-series data (e.g., sales data)
SELECT product, month, sales
FROM (
    SELECT product, [January], [February], [March]
    FROM sales_data
) AS source
UNPIVOT (
    sales FOR month IN ([January], [February], [March])
) AS unpvt;
```

**Use when**: You need to transform date columns into rows for analysis, such as summarizing monthly sales data.

---

### 3. **UNPIVOT with Filtering**

```sql
-- Trick: Use UNPIVOT and apply filters to get specific metrics
SELECT department, metric, value
FROM (
    SELECT department, hr, it, sales
    FROM employee_performance
) AS source
UNPIVOT (
    value FOR metric IN (hr, it, sales)
) AS unpvt
WHERE value > 5000;
```

**Use when**: You want to unpivot data but only need specific rows, such as performance metrics above a certain threshold.

---

### 4. **UNPIVOT with Dynamic Columns**

```sql
-- Trick: Use dynamic SQL to handle dynamic columns for unpivoting
DECLARE @columns AS NVARCHAR(MAX), @sql AS NVARCHAR(MAX);

-- Get the list of columns to unpivot dynamically
SELECT @columns = STRING_AGG(QUOTENAME(column_name), ',') FROM (SELECT column_name FROM sys.columns WHERE object_id = OBJECT_ID('sales_data')) AS col_list;

-- Create dynamic SQL for unpivoting
SET @sql = 'SELECT product, month, sales FROM (SELECT product, ' + @columns + ' FROM sales_data) AS source UNPIVOT (sales FOR month IN (' + @columns + ')) AS unpvt;';
EXEC sp_executesql @sql;
```

**Use when**: You need to dynamically unpivot data when column names are not known in advance.

---

### 5. **UNPIVOT to Normalize Data**

```sql
-- Trick: UNPIVOT to normalize wide tables (e.g., survey data)
SELECT respondent_id, question, response
FROM (
    SELECT respondent_id, q1, q2, q3
    FROM survey_responses
) AS source
UNPIVOT (
    response FOR question IN (q1, q2, q3)
) AS unpvt;
```

**Use when**: You want to normalize data from a wide table (like survey data with responses in columns) into a long format for easier analysis.

---

### Key Tips for **PIVOT** and **UNPIVOT**:

* **PIVOT** can be used to summarize data, making it more readable for certain types of analysis (like sales by month).
* **UNPIVOT** is useful for normalizing or transforming wide datasets into a long format for analysis.
* For dynamic column handling in both `PIVOT` and `UNPIVOT`, use **dynamic SQL** to adapt to changing column names or unknown values.
* Be cautious when using **aggregate functions** in `PIVOT` as it can lead to unexpected results if the data is not properly grouped.
* When using `PIVOT`, ensure that the data is well-organized and the column names are consistent to avoid errors in transformation.

---
