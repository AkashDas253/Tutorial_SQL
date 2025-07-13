## SQL Window Functions

### Overview
- **Definition**: Window functions perform calculations across a set of table rows that are related to the current row.
- **Purpose**: Provide advanced analytical capabilities, such as ranking, running totals, moving averages, and more.

### General Syntax
```sql
function_name (expression) 
OVER (
  [PARTITION BY partition_expression]
  [ORDER BY sort_expression [ASC|DESC]]
  [frame_clause]
)
```

### Parameters
- **function_name**: The name of the window function (e.g., `ROW_NUMBER`, `RANK`, `DENSE_RANK`, `SUM`, `AVG`).
- **expression**: The column or expression to be used in the calculation.
- **PARTITION BY partition_expression**: Divides the result set into partitions to which the window function is applied. Optional.
- **ORDER BY sort_expression**: Defines the order of rows within each partition. Optional but often used.
- **frame_clause**: Specifies the subset of rows within the partition to be considered for the calculation. Optional.

### Common Window Functions

#### ROW_NUMBER
- **Purpose**: Assigns a unique sequential integer to rows within a partition of a result set.
- **Syntax**:
  ```sql
  ROW_NUMBER() OVER (PARTITION BY column ORDER BY column)
  ```
- **Example**:
  ```sql
  SELECT employee_id, salary,
         ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS row_num
  FROM employees;
  ```

#### RANK
- **Purpose**: Assigns a rank to each row within a partition of a result set, with gaps in the ranking for ties.
- **Syntax**:
  ```sql
  RANK() OVER (PARTITION BY column ORDER BY column)
  ```
- **Example**:
  ```sql
  SELECT employee_id, salary,
         RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank
  FROM employees;
  ```

#### DENSE_RANK
- **Purpose**: Similar to `RANK`, but without gaps in the ranking for ties.
- **Syntax**:
  ```sql
  DENSE_RANK() OVER (PARTITION BY column ORDER BY column)
  ```
- **Example**:
  ```sql
  SELECT employee_id, salary,
         DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS dense_rank
  FROM employees;
  ```

#### SUM
- **Purpose**: Calculates the sum of a numeric column over a partition.
- **Syntax**:
  ```sql
  SUM(column) OVER (PARTITION BY column ORDER BY column [frame_clause])
  ```
- **Example**:
  ```sql
  SELECT employee_id, salary,
         SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id) AS running_total
  FROM employees;
  ```

#### AVG
- **Purpose**: Calculates the average of a numeric column over a partition.
- **Syntax**:
  ```sql
  AVG(column) OVER (PARTITION BY column ORDER BY column [frame_clause])
  ```
- **Example**:
  ```sql
  SELECT employee_id, salary,
         AVG(salary) OVER (PARTITION BY department_id ORDER BY employee_id) AS avg_salary
  FROM employees;
  ```

### Frame Clauses
- **ROWS**: Defines the frame in terms of physical rows.
  - **Syntax**:
    ```sql
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ```
- **RANGE**: Defines the frame in terms of logical range of values.
  - **Syntax**:
    ```sql
    RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ```

### Examples of Frame Clauses
- **Running Total**:
  ```sql
  SELECT employee_id, salary,
         SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id
                           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
  FROM employees;
  ```
- **Moving Average**:
  ```sql
  SELECT employee_id, salary,
         AVG(salary) OVER (PARTITION BY department_id ORDER BY employee_id
                           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
  FROM employees;
  ```

### Usage Considerations
- **Performance**: Window functions can be resource-intensive; optimize queries and use indexes where appropriate.
- **Compatibility**: Ensure your SQL database supports the specific window functions and syntax you intend to use.

### Best Practices
- **Partitioning**: Use `PARTITION BY` to logically divide data for more meaningful calculations.
- **Ordering**: Use `ORDER BY` to define the sequence of rows for calculations.
- **Frame Clauses**: Use frame clauses to fine-tune the subset of rows considered for each calculation.

### Additional Resources
- **Documentation**: Refer to your specific SQL database documentation for detailed information on supported window functions and syntax.
- **Examples**: Practice with sample data to understand the behavior and performance of window functions in different scenarios.



## Differences in SQL Window Functions Across Implementations

| Feature/Function       | PostgreSQL | MySQL (8.0+) | SQL Server | Oracle |
|------------------------|------------|--------------|------------|--------|
| **Basic Syntax**       | Supported  | Supported    | Supported  | Supported |
| **PARTITION BY**       | Supported  | Supported    | Supported  | Supported |
| **ORDER BY**           | Supported  | Supported    | Supported  | Supported |
| **ROWS Frame Clause**  | Supported  | Supported    | Supported  | Supported |
| **RANGE Frame Clause** | Supported  | Supported    | Supported  | Supported |
| **ROW_NUMBER**         | Supported  | Supported    | Supported  | Supported |
| **RANK**               | Supported  | Supported    | Supported  | Supported |
| **DENSE_RANK**         | Supported  | Supported    | Supported  | Supported |
| **SUM**                | Supported  | Supported    | Supported  | Supported |
| **AVG**                | Supported  | Supported    | Supported  | Supported |
| **NTILE**              | Supported  | Supported    | Supported  | Supported |
| **LAG**                | Supported  | Supported    | Supported  | Supported |
| **LEAD**               | Supported  | Supported    | Supported  | Supported |
| **FIRST_VALUE**        | Supported  | Supported    | Supported  | Supported |
| **LAST_VALUE**         | Supported  | Supported    | Supported  | Supported |
| **CUME_DIST**          | Supported  | Supported    | Supported  | Supported |
| **PERCENT_RANK**       | Supported  | Supported    | Supported  | Supported |
| **NTH_VALUE**          | Supported  | Supported    | Supported  | Supported |
| **Window Frame Exclusion** | Supported | Not Supported | Supported | Supported |
| **Custom Aggregates**  | Supported  | Limited      | Supported  | Supported |
| **Window Function Extensions** | Supported | Limited | Supported | Supported |

### Notes on Differences

1. **Frame Clauses**:
   - **PostgreSQL, SQL Server, Oracle**: Fully support both `ROWS` and `RANGE` frame clauses with extensive options.
   - **MySQL**: Supports `ROWS` and `RANGE` frame clauses, but with some limitations compared to other databases.

2. **Function Availability**:
   - **MySQL**: Introduced window functions in version 8.0, so older versions do not support them.
   - **PostgreSQL, SQL Server, Oracle**: Have supported window functions for a longer time, with a wide range of functions available.

3. **Syntax Variations**:
   - **Oracle**: Sometimes uses slightly different syntax for certain functions or additional options.
   - **SQL Server**: May have additional proprietary functions or options not available in other databases.

4. **Window Frame Exclusion**:
   - **PostgreSQL, SQL Server, Oracle**: Support window frame exclusion clauses like `EXCLUDE CURRENT ROW`.
   - **MySQL**: Does not support window frame exclusion clauses.

5. **Custom Aggregates**:
   - **PostgreSQL, SQL Server, Oracle**: Support creating custom aggregate functions that can be used with window functions.
   - **MySQL**: Limited support for custom aggregates.

6. **Window Function Extensions**:
   - **PostgreSQL, SQL Server, Oracle**: Provide additional extensions and optimizations for window functions.
   - **MySQL**: Limited extensions and optimizations compared to other databases.

### Example Queries

#### Running Total Example

- **PostgreSQL**:
  ```sql
  SELECT employee_id, salary,
         SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id
                           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
  FROM employees;
  ```

- **MySQL**:
  ```sql
  SELECT employee_id, salary,
         SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id
                           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
  FROM employees;
  ```

- **SQL Server**:
  ```sql
  SELECT employee_id, salary,
         SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id
                           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
  FROM employees;
  ```

- **Oracle**:
  ```sql
  SELECT employee_id, salary,
         SUM(salary) OVER (PARTITION BY department_id ORDER BY employee_id
                           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
  FROM employees;
  ```
