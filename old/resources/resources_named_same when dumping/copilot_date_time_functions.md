# Date and Time Functions

Date and time functions are used to manipulate, format, and extract components from date and time values in SQL. They are essential for scheduling, reporting, and temporal analysis.

## Date and Time Functions

### 1. `CURRENT_DATE` / `CURDATE()`
- **Description**: Returns the current date.
- **Syntax**:
  - ANSI SQL: `CURRENT_DATE`
  - MySQL: `CURDATE()`
- **Example**:
  ```sql
  SELECT CURRENT_DATE AS today;
  ```

### 2. `CURRENT_TIME` / `CURTIME()`
- **Description**: Returns the current time.
- **Syntax**:
  - ANSI SQL: `CURRENT_TIME`
  - MySQL: `CURTIME()`
- **Example**:
  ```sql
  SELECT CURRENT_TIME AS current_time;
  ```

### 3. `CURRENT_TIMESTAMP` / `NOW()`
- **Description**: Returns the current date and time.
- **Syntax**:
  - ANSI SQL: `CURRENT_TIMESTAMP`
  - MySQL: `NOW()`
- **Example**:
  ```sql
  SELECT NOW() AS current_datetime;
  ```

### 4. `EXTRACT()`
- **Description**: Extracts a specific part of a date or time (e.g., year, month, day, hour).
- **Syntax**:
  ```sql
  EXTRACT(part FROM date_value)
  ```
- **Example**:
  ```sql
  SELECT EXTRACT(YEAR FROM '2024-11-15') AS year;
  ```

### 5. `DATE_ADD()` / `ADD_MONTHS()` / `DATEADD()`
- **Description**: Adds a specified interval to a date.
- **Syntax**:
  - MySQL: `DATE_ADD(date, INTERVAL value unit)`
  - Oracle: `ADD_MONTHS(date, number_of_months)`
  - SQL Server: `DATEADD(unit, value, date)`
- **Example**:
  ```sql
  SELECT DATE_ADD('2024-11-15', INTERVAL 10 DAY) AS new_date;
  ```

### 6. `DATE_SUB()`
- **Description**: Subtracts a specified interval from a date.
- **Syntax**:
  ```sql
  DATE_SUB(date, INTERVAL value unit)
  ```
- **Example**:
  ```sql
  SELECT DATE_SUB('2024-11-15', INTERVAL 5 MONTH) AS new_date;
  ```

### 7. `DATEDIFF()`
- **Description**: Calculates the difference between two dates in days.
- **Syntax**:
  ```sql
  DATEDIFF(date1, date2)
  ```
- **Example**:
  ```sql
  SELECT DATEDIFF('2024-11-20', '2024-11-15') AS days_difference;
  ```

### 8. `TIMESTAMPDIFF()` / `DATE_PART()`
- **Description**: Returns the difference between two timestamps in a specified unit.
- **Syntax**:
  - MySQL: `TIMESTAMPDIFF(unit, datetime1, datetime2)`
  - PostgreSQL: `DATE_PART(field, interval)`
- **Example**:
  ```sql
  SELECT TIMESTAMPDIFF(HOUR, '2024-11-15 10:00:00', '2024-11-15 18:00:00') AS hours_difference;
  ```

### 9. `FORMAT()` / `TO_CHAR()`
- **Description**: Formats a date or time according to a specified pattern.
- **Syntax**:
  - MySQL: `DATE_FORMAT(date, format)`
  - Oracle/PostgreSQL: `TO_CHAR(date, format)`
- **Example**:
  ```sql
  SELECT DATE_FORMAT('2024-11-15', '%Y-%m-%d') AS formatted_date;
  ```

### 10. `LAST_DAY()`
- **Description**: Returns the last day of the month for a given date.
- **Syntax**:
  ```sql
  LAST_DAY(date)
  ```
- **Example**:
  ```sql
  SELECT LAST_DAY('2024-11-15') AS end_of_month;
  ```

### 11. `DAYNAME()` / `TO_CHAR()`
- **Description**: Returns the name of the day for a date.
- **Syntax**:
  - MySQL: `DAYNAME(date)`
  - Oracle/PostgreSQL: `TO_CHAR(date, 'Day')`
- **Example**:
  ```sql
  SELECT DAYNAME('2024-11-15') AS day_name;
  ```

### 12. `YEAR()`, `MONTH()`, `DAY()`, etc.
- **Description**: Extracts the year, month, or day from a date.
- **Syntax**:
  ```sql
  YEAR(date), MONTH(date), DAY(date)
  ```
- **Example**:
  ```sql
  SELECT YEAR('2024-11-15') AS year;
  ```

### 13. `STR_TO_DATE()`
- **Description**: Parses a string into a date.
- **Syntax**:
  ```sql
  STR_TO_DATE(string, format)
  ```
- **Example**:
  ```sql
  SELECT STR_TO_DATE('15-11-2024', '%d-%m-%Y') AS parsed_date;
  ```

### 14. `GETDATE()` / `SYSDATE()`
- **Description**: Returns the current date and time (similar to `NOW()`).
- **Syntax**:
  - SQL Server: `GETDATE()`
  - Oracle: `SYSDATE`
- **Example**:
  ```sql
  SELECT GETDATE() AS current_date_time;
  ```

---

## Comparison of Date and Time Functions Across SQL Implementations

| Feature/Function       | ANSI SQL     | PostgreSQL      | MySQL (8.0+) | SQL Server   | Oracle         |
|------------------------|--------------|-----------------|--------------|--------------|----------------|
| **CURRENT_DATE**       | Supported    | Supported       | Supported    | Supported    | Supported      |
| **CURRENT_TIME**       | Supported    | Supported       | Supported    | Supported    | Supported      |
| **NOW()**              | Not Supported | Supported       | Supported    | Supported (`GETDATE()`) | Supported (`SYSDATE`) |
| **EXTRACT()**          | Supported    | Supported       | Supported    | Not Supported (use `DATEPART`) | Supported      |
| **DATEDIFF()**         | Not Supported | Supported (custom) | Supported    | Supported    | Custom Implementation |
| **DATE_FORMAT()**      | Not Supported | Supported (custom) | Supported    | Not Supported | Use `TO_CHAR()`|
| **TO_CHAR()**          | Not Supported | Supported       | Not Supported| Not Supported | Supported      |
| **LAST_DAY()**         | Not Supported | Supported       | Supported    | Not Supported | Supported      |
| **DAYNAME()**          | Not Supported | Supported (custom)| Supported    | Not Supported | Use `TO_CHAR()`|


### Notes on Differences

1. **CURRENT_DATE**: Universally supported with consistent syntax.
2. **DATE_ADD()/DATE_SUB()**:
   - MySQL uses `INTERVAL` keyword for adding or subtracting intervals.
   - SQL Server and Oracle use specific functions like `DATEADD` or `ADD_MONTHS`.
3. **DATEDIFF()**:
   - SQL Server and MySQL have built-in support; others require custom queries.
4. **Formatting**:
   - MySQL uses `DATE_FORMAT`.
   - PostgreSQL and Oracle use `TO_CHAR` for advanced formatting.
5. **EXTRACT vs. DATEPART**:
   - `EXTRACT` is ANSI SQL and broadly supported.
   - SQL Server uses `DATEPART`. 
