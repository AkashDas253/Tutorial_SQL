
## Common SQL Window Functions

### 1. ROW_NUMBER
- `ROW_NUMBER() OVER (PARTITION BY column_name ORDER BY column_name)`  # Assign a unique number to each row within a partition of a result set

### 2. RANK
- `RANK() OVER (PARTITION BY column_name ORDER BY column_name)`  # Assign a rank to each row within a partition of a result set

### 3. DENSE_RANK
- `DENSE_RANK() OVER (PARTITION BY column_name ORDER BY column_name)`  # Assign a rank to each row within a partition of a result set, without gaps

### 4. NTILE
- `NTILE(number) OVER (PARTITION BY column_name ORDER BY column_name)`  # Distribute rows into a specified number of approximately equal groups

### 5. LAG
- `LAG(column_name, offset, default_value) OVER (PARTITION BY column_name ORDER BY column_name)`  # Access data from a previous row in the same result set

### 6. LEAD
- `LEAD(column_name, offset, default_value) OVER (PARTITION BY column_name ORDER BY column_name)`  # Access data from a subsequent row in the same result set

### 7. FIRST_VALUE
- `FIRST_VALUE(column_name) OVER (PARTITION BY column_name ORDER BY column_name)`  # Return the first value in an ordered set of values

### 8. LAST_VALUE
- `LAST_VALUE(column_name) OVER (PARTITION BY column_name ORDER BY column_name)`  # Return the last value in an ordered set of values

### 9. CUME_DIST
- `CUME_DIST() OVER (PARTITION BY column_name ORDER BY column_name)`  # Calculate the cumulative distribution of a value in a set

### 10. PERCENT_RANK
- `PERCENT_RANK() OVER (PARTITION BY column_name ORDER BY column_name)`  # Calculate the relative rank of a row within a partition

### 11. NTH_VALUE
- `NTH_VALUE(column_name, n) OVER (PARTITION BY column_name ORDER BY column_name)`  # Return the nth value in an ordered set of values

### 12. SUM
- `SUM(column_name) OVER (PARTITION BY column_name ORDER BY column_name)`  # Calculate the sum of values in a column over a partition

### 13. AVG
- `AVG(column_name) OVER (PARTITION BY column_name ORDER BY column_name)`  # Calculate the average of values in a column over a partition

### 14. MIN
- `MIN(column_name) OVER (PARTITION BY column_name ORDER BY column_name)`  # Find the minimum value in a column over a partition

### 15. MAX
- `MAX(column_name) OVER (PARTITION BY column_name ORDER BY column_name)`  # Find the maximum value in a column over a partition

### 16. COUNT
- `COUNT(column_name) OVER (PARTITION BY column_name ORDER BY column_name)`  # Count the number of non-NULL values in a column over a partition