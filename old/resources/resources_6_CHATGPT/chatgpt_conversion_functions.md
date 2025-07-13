# Conversion Functions

Conversion functions are used to transform data from one type to another, such as converting strings to numbers, dates to strings, or numbers to other formats. These functions are essential for data compatibility, processing, and formatting across SQL queries.


## Conversion Functions

### 1. `CAST()`
- **Description**: Converts a value from one data type to another.
- **Syntax**:
  ```sql
  CAST(expression AS target_data_type)
  ```
- **Example**:
  ```sql
  SELECT CAST('123' AS INT) AS converted_value;
  ```

### 2. `CONVERT()`
- **Description**: Converts a value from one data type to another (commonly used in SQL Server).
- **Syntax**:
  ```sql
  CONVERT(target_data_type, expression)
  ```
- **Example**:
  ```sql
  SELECT CONVERT(VARCHAR, 123) AS converted_value;
  ```

### 3. `TO_CHAR()`
- **Description**: Converts a date, number, or other data types to a string (commonly used in Oracle and PostgreSQL).
- **Syntax**:
  ```sql
  TO_CHAR(expression, format)
  ```
- **Example**:
  ```sql
  SELECT TO_CHAR(SYSDATE, 'YYYY-MM-DD') AS formatted_date;
  ```

### 4. `TO_DATE()`
- **Description**: Converts a string to a date (commonly used in Oracle and PostgreSQL).
- **Syntax**:
  ```sql
  TO_DATE(string, format)
  ```
- **Example**:
  ```sql
  SELECT TO_DATE('15-11-2024', 'DD-MM-YYYY') AS converted_date;
  ```

### 5. `TO_NUMBER()`
- **Description**: Converts a string or other types to a number (Oracle-specific).
- **Syntax**:
  ```sql
  TO_NUMBER(string)
  ```
- **Example**:
  ```sql
  SELECT TO_NUMBER('123.45') AS converted_number;
  ```

### 6. `STR_TO_DATE()`
- **Description**: Converts a string to a date (MySQL-specific).
- **Syntax**:
  ```sql
  STR_TO_DATE(string, format)
  ```
- **Example**:
  ```sql
  SELECT STR_TO_DATE('15-11-2024', '%d-%m-%Y') AS parsed_date;
  ```

### 7. `FORMAT()`
- **Description**: Converts a number or date to a formatted string (MySQL-specific).
- **Syntax**:
  ```sql
  FORMAT(value, decimal_places)
  ```
- **Example**:
  ```sql
  SELECT FORMAT(1234.567, 2) AS formatted_number;
  ```

### 8. `CONVERT_TZ()`
- **Description**: Converts a datetime value from one time zone to another (MySQL-specific).
- **Syntax**:
  ```sql
  CONVERT_TZ(datetime, from_timezone, to_timezone)
  ```
- **Example**:
  ```sql
  SELECT CONVERT_TZ('2024-11-15 10:00:00', 'UTC', 'Asia/Kolkata') AS local_time;
  ```

### 9. `TRY_CAST()` / `TRY_CONVERT()`
- **Description**: Similar to `CAST` and `CONVERT`, but returns `NULL` if conversion fails (SQL Server-specific).
- **Syntax**:
  ```sql
  TRY_CAST(expression AS target_data_type)
  ```
- **Example**:
  ```sql
  SELECT TRY_CAST('abc' AS INT) AS result; -- Returns NULL
  ```

### 10. `PARSE()`
- **Description**: Parses a string to a specific data type, useful for locales (SQL Server-specific).
- **Syntax**:
  ```sql
  PARSE(expression AS target_data_type USING culture)
  ```
- **Example**:
  ```sql
  SELECT PARSE('15-11-2024' AS DATE USING 'en-GB') AS parsed_date;
  ```

---

## Comparison of Conversion Functions Across SQL Implementations

| Function/Feature      | ANSI SQL      | MySQL              | SQL Server       | Oracle          | PostgreSQL       |
|-----------------------|---------------|--------------------|------------------|-----------------|------------------|
| **CAST()**            | Supported     | Supported          | Supported        | Supported       | Supported        |
| **CONVERT()**         | Not Supported | Not Supported      | Supported        | Not Supported   | Not Supported    |
| **TO_CHAR()**         | Not Supported | Not Supported      | Not Supported    | Supported       | Supported        |
| **TO_DATE()**         | Not Supported | Not Supported      | Not Supported    | Supported       | Supported        |
| **TO_NUMBER()**       | Not Supported | Not Supported      | Not Supported    | Supported       | Custom (CAST)    |
| **FORMAT()**          | Not Supported | Supported          | Supported        | Custom (TO_CHAR)| Custom (TO_CHAR) |
| **STR_TO_DATE()**     | Not Supported | Supported          | Not Supported    | Not Supported   | Custom (TO_DATE) |
| **CONVERT_TZ()**      | Not Supported | Supported          | Not Supported    | Not Supported   | Not Supported    |
| **TRY_CAST()**        | Not Supported | Not Supported      | Supported        | Not Supported   | Not Supported    |
| **PARSE()**           | Not Supported | Not Supported      | Supported        | Not Supported   | Not Supported    |



### Notes on Differences

1. **CAST vs. CONVERT**:
   - `CAST` is ANSI-compliant and widely supported.
   - `CONVERT` is specific to SQL Server.
2. **String to Date Conversion**:
   - MySQL uses `STR_TO_DATE`.
   - Oracle and PostgreSQL rely on `TO_DATE`.
3. **Date/Number to String**:
   - MySQL uses `FORMAT`, Oracle, and PostgreSQL use `TO_CHAR`.
4. **Time Zone Conversion**:
   - MySQL offers `CONVERT_TZ`, while others require custom logic or extensions.
5. **Error Handling**:
   - SQL Server provides `TRY_CAST` and `TRY_CONVERT` for safer conversions.

