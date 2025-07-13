## Common SQL Aggregation Functions

### 1. COUNT
- `COUNT(column_name)`  # Count the number of rows in a column
- `COUNT(*)`  # Count the total number of rows

### 2. SUM
- `SUM(column_name)`  # Calculate the sum of values in a column

### 3. AVG
- `AVG(column_name)`  # Calculate the average of values in a column

### 4. MIN
- `MIN(column_name)`  # Find the minimum value in a column

### 5. MAX
- `MAX(column_name)`  # Find the maximum value in a column

### 6. GROUP BY
- `GROUP BY column_name`  # Group rows that have the same values in specified columns

### 7. HAVING
- `HAVING condition`  # Filter groups based on a condition

### 8. DISTINCT
- `SELECT DISTINCT column_name`  # Select distinct values from a column

### 9. VARIANCE
- `VARIANCE(column_name)`  # Calculate the variance of values in a column

### 10. STDDEV
- `STDDEV(column_name)`  # Calculate the standard deviation of values in a column

### 11. MEDIAN
- `MEDIAN(column_name)`  # Calculate the median of values in a column (availability depends on the RDBMS)

### 12. MODE
- `MODE(column_name)`  # Calculate the mode of values in a column (availability depends on the RDBMS)

### 13. PERCENTILE_CONT
- `PERCENTILE_CONT(percent) WITHIN GROUP (ORDER BY column_name)`  # Calculate a continuous percentile (availability depends on the RDBMS)

### 14. PERCENTILE_DISC
- `PERCENTILE_DISC(percent) WITHIN GROUP (ORDER BY column_name)`  # Calculate a discrete percentile (availability depends on the RDBMS)

### 15. CUME_DIST
- `CUME_DIST() OVER (ORDER BY column_name)`  # Calculate the cumulative distribution of a value in a set (availability depends on the RDBMS)

### 16. RANK
- `RANK() OVER (ORDER BY column_name)`  # Assign a rank to each row within a partition of a result set (availability depends on the RDBMS)

### 17. DENSE_RANK
- `DENSE_RANK() OVER (ORDER BY column_name)`  # Assign a rank to each row within a partition of a result set, without gaps (availability depends on the RDBMS)

### 18. ROW_NUMBER
- `ROW_NUMBER() OVER (ORDER BY column_name)`  # Assign a unique number to each row within a partition of a result set (availability depends on the RDBMS)
