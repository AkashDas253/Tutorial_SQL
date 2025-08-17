# ANSI SQL Syntax Cheatsheet

## 1. Creating a Database
- `CREATE DATABASE database_name;`  # Create a new database

## 2. Using a Database
- `USE database_name;`  # Select a database to use

## 3. Creating a Table
- `CREATE TABLE table_name (`  # Create a new table
  - `column1 datatype constraints,`  # Define column1 with datatype and constraints
  - `column2 datatype constraints,`  # Define column2 with datatype and constraints
  - `...`  # Additional columns
  - `PRIMARY KEY (column1)`  # Define primary key
- `);`

## 4. Inserting Data
- `INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);`  # Insert data into a table

## 5. Selecting Data
- `SELECT column1, column2, ... FROM table_name;`  # Select specific columns
- `SELECT * FROM table_name;`  # Select all columns

## 6. Updating Data
- `UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;`  # Update data in a table

## 7. Deleting Data
- `DELETE FROM table_name WHERE condition;`  # Delete data from a table

## 8. Adding a Column
- `ALTER TABLE table_name ADD column_name datatype constraints;`  # Add a new column to a table

## 9. Modifying a Column
- `ALTER TABLE table_name ALTER COLUMN column_name SET DATA TYPE new_datatype;`  # Modify an existing column

## 10. Dropping a Column
- `ALTER TABLE table_name DROP COLUMN column_name;`  # Drop a column from a table

## 11. Dropping a Table
- `DROP TABLE table_name;`  # Drop a table

## 12. Dropping a Database
- `DROP DATABASE database_name;`  # Drop a database

## 13. Creating an Index
- `CREATE INDEX index_name ON table_name (column1, column2, ...);`  # Create an index on specified columns

## 14. Dropping an Index
- `DROP INDEX index_name;`  # Drop an index

## 15. Joining Tables
- `SELECT columns FROM table1 INNER JOIN table2 ON table1.column = table2.column;`  # Inner join
- `SELECT columns FROM table1 LEFT JOIN table2 ON table1.column = table2.column;`  # Left join
- `SELECT columns FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;`  # Right join
- `SELECT columns FROM table1 FULL OUTER JOIN table2 ON table1.column = table2.column;`  # Full outer join

## 16. Grouping Data
- `SELECT column1, COUNT(*) FROM table_name GROUP BY column1;`  # Group data by a column

## 17. Filtering Data
- `SELECT * FROM table_name WHERE condition;`  # Filter data using a condition
- `SELECT * FROM table_name WHERE column1 = value1 AND column2 = value2;`  # Multiple conditions with AND
- `SELECT * FROM table_name WHERE column1 = value1 OR column2 = value2;`  # Multiple conditions with OR

## 18. Sorting Data
- `SELECT * FROM table_name ORDER BY column1 ASC;`  # Sort data in ascending order
- `SELECT * FROM table_name ORDER BY column1 DESC;`  # Sort data in descending order

## 19. Limiting Results
- `SELECT * FROM table_name FETCH FIRST number ROWS ONLY;`  # Limit the number of results

## 20. Aggregate Functions
- `SELECT COUNT(column) FROM table_name;`  # Count the number of rows
- `SELECT AVG(column) FROM table_name;`  # Calculate the average value
- `SELECT SUM(column) FROM table_name;`  # Calculate the sum of values
- `SELECT MAX(column) FROM table_name;`  # Find the maximum value
- `SELECT MIN(column) FROM table_name;`  # Find the minimum value

## 21. Creating a View
- `CREATE VIEW view_name AS SELECT column1, column2, ... FROM table_name WHERE condition;`  # Create a view

## 22. Dropping a View
- `DROP VIEW view_name;`  # Drop a view

## 23. Renaming a Table
- `ALTER TABLE old_table_name RENAME TO new_table_name;`  # Rename a table

## 24. Renaming a Column
- `ALTER TABLE table_name RENAME COLUMN old_column_name TO new_column_name;`  # Rename a column

## 25. Creating a Stored Procedure
- `CREATE PROCEDURE procedure_name AS BEGIN SQL_statements END;`  # Create a stored procedure

## 26. Executing a Stored Procedure
- `CALL procedure_name;`  # Execute a stored procedure

## 27. Creating a Trigger
- `CREATE TRIGGER trigger_name BEFORE/AFTER INSERT/UPDATE/DELETE ON table_name FOR EACH ROW BEGIN SQL_statements END;`  # Create a trigger

## 28. Dropping a Trigger
- `DROP TRIGGER trigger_name;`  # Drop a trigger

## 29. Creating a Function
- `CREATE FUNCTION function_name (parameters) RETURNS return_datatype AS BEGIN SQL_statements RETURN return_value; END;`  # Create a function

## 30. Calling a Function
- `SELECT function_name(parameters);`  # Call a function

## 31. Creating a Sequence
- `CREATE SEQUENCE sequence_name START WITH initial_value INCREMENT BY increment_value;`  # Create a sequence

## 32. Using a Sequence
- `SELECT sequence_name.NEXTVAL;`  # Get the next value in a sequence

## 33. Dropping a Sequence
- `DROP SEQUENCE sequence_name;`  # Drop a sequence

## 34. Creating a Temporary Table
- `CREATE TEMPORARY TABLE temp_table_name (column1 datatype, column2 datatype, ...);`  # Create a temporary table

## 35. Dropping a Temporary Table
- `DROP TEMPORARY TABLE temp_table_name;`  # Drop a temporary table

## 36. Creating a Schema
- `CREATE SCHEMA schema_name;`  # Create a schema

## 37. Dropping a Schema
- `DROP SCHEMA schema_name;`  # Drop a schema

## 38. Granting Privileges
- `GRANT privilege ON object TO user;`  # Grant privileges to a user

## 39. Revoking Privileges
- `REVOKE privilege ON object FROM user;`  # Revoke privileges from a user

## 40. Creating a User
- `CREATE USER 'username' IDENTIFIED BY 'password';`  # Create a new user

## 41. Dropping a User
- `DROP USER 'username';`  # Drop a user

## 42. Creating a Role
- `CREATE ROLE role_name;`  # Create a role

## 43. Dropping a Role
- `DROP ROLE role_name;`  # Drop a role

## 44. Assigning a Role to a User
- `GRANT role_name TO user;`  # Assign a role to a user

## 45. Revoking a Role from a User
- `REVOKE role_name FROM user;`  # Revoke a role from a user

## 46. Creating a Synonym
- `CREATE SYNONYM synonym_name FOR object_name;`  # Create a synonym for an object

## 47. Dropping a Synonym
- `DROP SYNONYM synonym_name;`  # Drop a synonym

## 48. Creating a Cursor
- `DECLARE cursor_name CURSOR FOR SELECT_statement;`  # Declare a cursor

## 49. Opening a Cursor
- `OPEN cursor_name;`  # Open a cursor

## 50. Fetching from a Cursor
- `FETCH cursor_name INTO variable1, variable2, ...;`  # Fetch data from a cursor

## 51. Closing a Cursor
- `CLOSE cursor_name;`  # Close a cursor

## 52. Declaring a Variable
- `DECLARE variable_name datatype;`  # Declare a variable

## 53. Setting a Variable
- `SET variable_name = value;`  # Set a variable's value

## 54. Using a Case Statement
- `CASE`  # Start a case statement
  - `WHEN condition1 THEN result1`  # Condition and result
  - `WHEN condition2 THEN result2`  # Another condition and result
  - `ELSE result`  # Default result
- `END;`

## 55. Using a Subquery
- `SELECT column1, column2, ... FROM (SELECT column1, column2, ... FROM table_name WHERE condition) AS subquery;`  # Use a subquery

## 56. Using EXISTS
- `SELECT column1, column2, ... FROM table_name WHERE EXISTS (SELECT 1 FROM another_table WHERE condition);`  # Use EXISTS to check for the existence of rows

## 57. Using IN
- `SELECT column1, column2, ... FROM table_name WHERE column IN (value1, value2, ...);`  # Use IN to filter by a list of values

## 58. Using BETWEEN
- `SELECT column1, column2, ... FROM table_name WHERE column BETWEEN value1 AND value2;`  # Use BETWEEN to filter by a range of values

## 59. Using LIKE
- `SELECT column1, column2, ... FROM table_name WHERE column LIKE pattern;`  # Use LIKE to filter by a pattern

## 60. Using DISTINCT
- `SELECT DISTINCT column1, column2, ... FROM table_name;`  # Select distinct values

## 61. Using UNION
- `SELECT column1, column2, ... FROM table1 UNION SELECT column1, column2, ... FROM table2;`  # Combine results from multiple queries

## 62. Using INTERSECT
- `SELECT column1, column2, ... FROM table1 INTERSECT SELECT column1, column2, ... FROM table2;`  # Get the intersection of results from multiple queries

## 63. Using EXCEPT
- `SELECT column1, column2, ... FROM table1 EXCEPT SELECT column1, column2, ... FROM table2;`  # Get the difference of results from multiple queries

## 64. Using COALESCE
- `SELECT COALESCE(column1, column2, ...);`  # Return the first non-null value

## 65. Using NULLIF
- `SELECT NULLIF(expression1, expression2);`  # Return NULL if the expressions are equal

## 66. Using CAST
- `SELECT CAST(expression AS datatype);`  # Convert a value to a different datatype

## 67. Using CONVERT
- `SELECT CONVERT(datatype, expression);`  # Convert a value to a different datatype

## 68. Using TRIM
- `SELECT TRIM(column);`  # Remove leading and trailing spaces

## 69. Using SUBSTRING
- `SELECT SUBSTRING(column FROM start FOR length);`  # Extract a substring

## 70. Using LENGTH
- `SELECT LENGTH(column);`  # Get the length of a string

## Common SQL String Functions

### 1. CONCAT
- `CONCAT(string1, string2, ...)`  # Concatenate multiple strings

### 2. SUBSTRING
- `SUBSTRING(string FROM start FOR length)`  # Extract a substring from a string

### 3. LENGTH
- `LENGTH(string)`  # Get the length of a string

### 4. TRIM
- `TRIM(string)`  # Remove leading and trailing spaces from a string

### 5. LTRIM
- `LTRIM(string)`  # Remove leading spaces from a string

### 6. RTRIM
- `RTRIM(string)`  # Remove trailing spaces from a string

### 7. UPPER
- `UPPER(string)`  # Convert a string to uppercase

### 8. LOWER
- `LOWER(string)`  # Convert a string to lowercase

### 9. REPLACE
- `REPLACE(string, search, replace)`  # Replace occurrences of a substring within a string

### 10. POSITION
- `POSITION(substring IN string)`  # Find the position of a substring within a string

### 11. LEFT
- `LEFT(string, number)`  # Extract a specified number of characters from the left of a string

### 12. RIGHT
- `RIGHT(string, number)`  # Extract a specified number of characters from the right of a string

### 13. CHAR_LENGTH
- `CHAR_LENGTH(string)`  # Get the number of characters in a string

### 14. ASCII
- `ASCII(character)`  # Get the ASCII value of a character

### 15. CHAR
- `CHAR(ascii_value)`  # Convert an ASCII value to a character

### 16. INITCAP
- `INITCAP(string)`  # Capitalize the first letter of each word in a string

### 17. LPAD
- `LPAD(string, length, pad_string)`  # Pad the left side of a string with a specified character

### 18. RPAD
- `RPAD(string, length, pad_string)`  # Pad the right side of a string with a specified character

### 19. REVERSE
- `REVERSE(string)`  # Reverse the characters in a string

### 20. FORMAT
- `FORMAT(string, format)`  # Format a string according to a specified format

## Common SQL Date and Time Functions

### 1. CURRENT_DATE
- `CURRENT_DATE`  # Get the current date

### 2. CURRENT_TIME
- `CURRENT_TIME`  # Get the current time

### 3. CURRENT_TIMESTAMP
- `CURRENT_TIMESTAMP`  # Get the current date and time

### 4. DATE
- `DATE(expression)`  # Extract the date part of a date or datetime expression

### 5. TIME
- `TIME(expression)`  # Extract the time part of a date or datetime expression

### 6. YEAR
- `YEAR(date)`  # Extract the year from a date

### 7. MONTH
- `MONTH(date)`  # Extract the month from a date

### 8. DAY
- `DAY(date)`  # Extract the day from a date

### 9. HOUR
- `HOUR(time)`  # Extract the hour from a time

### 10. MINUTE
- `MINUTE(time)`  # Extract the minute from a time

### 11. SECOND
- `SECOND(time)`  # Extract the second from a time

### 12. DATE_ADD
- `DATE_ADD(date, INTERVAL value unit)`  # Add an interval to a date

### 13. DATE_SUB
- `DATE_SUB(date, INTERVAL value unit)`  # Subtract an interval from a date

### 14. DATEDIFF
- `DATEDIFF(date1, date2)`  # Calculate the difference between two dates

### 15. TIMESTAMPDIFF
- `TIMESTAMPDIFF(unit, datetime1, datetime2)`  # Calculate the difference between two timestamps

### 16. DATE_FORMAT
- `DATE_FORMAT(date, format)`  # Format a date according to a specified format

### 17. STR_TO_DATE
- `STR_TO_DATE(string, format)`  # Convert a string to a date according to a specified format

### 18. UNIX_TIMESTAMP
- `UNIX_TIMESTAMP(date)`  # Convert a date to a Unix timestamp

### 19. FROM_UNIXTIME
- `FROM_UNIXTIME(timestamp)`  # Convert a Unix timestamp to a date

### 20. EXTRACT
- `EXTRACT(unit FROM date)`  # Extract a part of a date (e.g., year, month, day)

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

## Common SQL Functions for Working with NULL Values

### 1. IS NULL
- `column_name IS NULL`  # Check if a column value is NULL

### 2. IS NOT NULL
- `column_name IS NOT NULL`  # Check if a column value is not NULL

### 3. COALESCE
- `COALESCE(expression1, expression2, ...)`  # Return the first non-NULL expression

### 4. NULLIF
- `NULLIF(expression1, expression2)`  # Return NULL if the two expressions are equal, otherwise return the first expression

### 5. IFNULL
- `IFNULL(expression, value)`  # Return the value if the expression is NULL (MySQL specific)

### 6. NVL
- `NVL(expression, value)`  # Return the value if the expression is NULL (Oracle specific)

### 7. NVL2
- `NVL2(expression, value_if_not_null, value_if_null)`  # Return different values depending on whether the expression is NULL (Oracle specific)

### 8. ISNULL
- `ISNULL(expression, value)`  # Return the value if the expression is NULL (SQL Server specific)

### 9. LNNVL
- `LNNVL(condition)`  # Return TRUE if the condition is FALSE or UNKNOWN (Oracle specific)

### 10. DECODE
- `DECODE(expression, search, result, ..., default)`  # Return different results based on the value of the expression, with handling for NULL (Oracle specific)

## Common SQL Mathematical Functions

### 1. ABS
- `ABS(number)`  # Return the absolute value of a number

### 2. CEIL / CEILING
- `CEIL(number)` or `CEILING(number)`  # Round a number up to the nearest integer

### 3. FLOOR
- `FLOOR(number)`  # Round a number down to the nearest integer

### 4. ROUND
- `ROUND(number, decimals)`  # Round a number to a specified number of decimal places

### 5. TRUNC / TRUNCATE
- `TRUNC(number, decimals)` or `TRUNCATE(number, decimals)`  # Truncate a number to a specified number of decimal places

### 6. MOD
- `MOD(number, divisor)`  # Return the remainder of a division operation

### 7. POWER
- `POWER(base, exponent)`  # Raise a number to the power of another number

### 8. SQRT
- `SQRT(number)`  # Return the square root of a number

### 9. EXP
- `EXP(number)`  # Return e raised to the power of a number

### 10. LN
- `LN(number)`  # Return the natural logarithm of a number

### 11. LOG
- `LOG(base, number)`  # Return the logarithm of a number with a specified base

### 12. LOG10
- `LOG10(number)`  # Return the base-10 logarithm of a number

### 13. PI
- `PI()`  # Return the value of π (pi)

### 14. SIN
- `SIN(number)`  # Return the sine of a number (in radians)

### 15. COS
- `COS(number)`  # Return the cosine of a number (in radians)

### 16. TAN
- `TAN(number)`  # Return the tangent of a number (in radians)

### 17. ASIN
- `ASIN(number)`  # Return the arcsine of a number

### 18. ACOS
- `ACOS(number)`  # Return the arccosine of a number

### 19. ATAN
- `ATAN(number)`  # Return the arctangent of a number

### 20. ATAN2
- `ATAN2(y, x)`  # Return the arctangent of the two numbers y and x

### 21. RADIANS
- `RADIANS(degrees)`  # Convert degrees to radians

### 22. DEGREES
- `DEGREES(radians)`  # Convert radians to degrees

### 23. SIGN
- `SIGN(number)`  # Return the sign of a number (-1, 0, 1)

## Common SQL Aggregate Functions

### 1. COUNT
- `COUNT(column_name)`  # Count the number of non-NULL values in a column
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