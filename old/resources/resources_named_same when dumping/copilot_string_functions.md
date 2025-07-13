# String Functions

String functions are used to manipulate and transform text values in SQL. They perform operations such as concatenation, trimming, extracting substrings, and more, to facilitate text processing and analysis.


## String Functions

### 1. `CONCAT()`
- **Description**: Concatenates two or more strings into one.
- **Syntax**: `CONCAT(string1, string2, ..., stringN)`
- **Example**:
  ```sql
  SELECT CONCAT('Hello', ' ', 'World') AS result;
  ```

### 2. `SUBSTRING()` / `SUBSTR()`
- **Description**: Extracts a portion of a string starting from a specified position for a specified length.
- **Syntax**: 
  - `SUBSTRING(string, start_position, length)`
  - `SUBSTR(string, start_position, length)` (Oracle and MySQL alias)
- **Example**:
  ```sql
  SELECT SUBSTRING('Hello World', 1, 5) AS result;
  ```

### 3. `CHAR_LENGTH()` / `LENGTH()`
- **Description**: Returns the number of characters in a string.
- **Syntax**:
  - `CHAR_LENGTH(string)`
  - `LENGTH(string)` (MySQL and Oracle alias)
- **Example**:
  ```sql
  SELECT CHAR_LENGTH('Hello World') AS result;
  ```

### 4. `UPPER()` / `LOWER()`
- **Description**: Converts a string to uppercase or lowercase.
- **Syntax**:
  - `UPPER(string)`
  - `LOWER(string)`
- **Example**:
  ```sql
  SELECT UPPER('hello world') AS result;
  ```

### 5. `TRIM()`
- **Description**: Removes leading and trailing spaces or specified characters from a string.
- **Syntax**: 
  - `TRIM([LEADING | TRAILING | BOTH] [characters] FROM string)`
- **Example**:
  ```sql
  SELECT TRIM('   Hello World   ') AS result;
  ```

### 6. `REPLACE()`
- **Description**: Replaces occurrences of a substring with another substring.
- **Syntax**: `REPLACE(string, substring_to_replace, replacement_string)`
- **Example**:
  ```sql
  SELECT REPLACE('Hello World', 'World', 'SQL') AS result;
  ```

### 7. `CONCAT_WS()` (MySQL)
- **Description**: Concatenates strings with a specified separator.
- **Syntax**: `CONCAT_WS(separator, string1, string2, ..., stringN)`
- **Example**:
  ```sql
  SELECT CONCAT_WS('-', '2024', '11', '15') AS result;
  ```

### 8. `LEFT()` / `RIGHT()`
- **Description**: Extracts a specified number of characters from the left or right of a string.
- **Syntax**:
  - `LEFT(string, length)`
  - `RIGHT(string, length)`
- **Example**:
  ```sql
  SELECT LEFT('Hello World', 5) AS result;
  ```

### 9. `POSITION()` / `INSTR()`
- **Description**: Returns the position of the first occurrence of a substring.
- **Syntax**:
  - `POSITION(substring IN string)`
  - `INSTR(string, substring)` (MySQL and Oracle alias)
- **Example**:
  ```sql
  SELECT POSITION('World' IN 'Hello World') AS result;
  ```



## Comparison of String Functions Across SQL Implementations

| Feature/Function       | ANSI SQL   | PostgreSQL | MySQL (8.0+) | SQL Server | Oracle       |
|------------------------|------------|------------|--------------|------------|--------------|
| **CONCAT()**           | Supported  | Supported  | Supported    | Supported  | Supported    |
| **SUBSTRING()**        | Supported  | Supported  | Supported    | Supported  | Supported (`SUBSTR`) |
| **CHAR_LENGTH()**      | Supported  | Supported  | Supported    | Not Supported (use `LEN()`) | Supported    |
| **UPPER() / LOWER()**  | Supported  | Supported  | Supported    | Supported  | Supported    |
| **TRIM()**             | Supported  | Supported  | Supported    | Supported  | Supported    |
| **REPLACE()**          | Supported  | Supported  | Supported    | Supported  | Supported    |
| **CONCAT_WS()**        | Not Supported | Not Supported | Supported | Not Supported | Not Supported |
| **LEFT() / RIGHT()**   | Not Supported | Supported  | Supported    | Supported  | Supported    |
| **POSITION()**         | Supported  | Supported  | Supported    | Not Supported (use `CHARINDEX()`) | Supported (`INSTR`) |

---

### Notes on Differences

1. **CONCAT()**:
   - Universal across most databases.
   - In SQL Server, `+` operator can also be used for concatenation.

2. **SUBSTRING() / SUBSTR()**:
   - Widely supported with minor syntax differences (`SUBSTR` in Oracle and MySQL).

3. **CHAR_LENGTH() / LENGTH()**:
   - SQL Server uses `LEN()` instead of `CHAR_LENGTH()` or `LENGTH()`.

4. **TRIM()**:
   - ANSI standard syntax is supported in all major databases.

5. **CONCAT_WS()**:
   - Specific to MySQL for concatenating with a separator.

6. **LEFT() / RIGHT()**:
   - Not available in ANSI SQL but widely supported in specific database systems.

7. **POSITION() / INSTR()**:
   - Oracle and MySQL use `INSTR()` as an alias for substring search. SQL Server uses `CHARINDEX()` as an alternative.