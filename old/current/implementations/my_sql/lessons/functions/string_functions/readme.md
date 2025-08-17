## String Functions in MySQL

**String functions** allow manipulation, analysis, and transformation of text-based data. They are widely used in data formatting, searching, and cleaning tasks.

--- 

### Inner Index

* [Concatenation Functions](#concatenation-functions)
* [Length Functions](#length-functions)
* [Case Conversion Functions](#case-conversion-functions)
* [Substring Functions](#substring-functions)
* [Trimming and Padding Functions](#trimming-and-padding-functions)
* [Search and Replace Functions](#search-and-replace-functions)
* [Encoding Functions](#encoding-functions)
* [Other Useful Functions](#other-useful-functions)
* [Usage Scenarios](#usage-scenarios)

---

### Concatenation Functions

| Function                          | Description            |
| --------------------------------- | ---------------------- |
| `CONCAT(str1, str2, ...)`         | Joins strings together |
| `CONCAT_WS(sep, str1, str2, ...)` | Joins with separator   |

```sql
SELECT CONCAT('My', 'SQL'); -- 'MySQL'
SELECT CONCAT_WS('-', '2025', '04', '13'); -- '2025-04-13'
```

---

### Length Functions

| Function           | Description     |
| ------------------ | --------------- |
| `LENGTH(str)`      | Bytes length    |
| `CHAR_LENGTH(str)` | Character count |

```sql
SELECT LENGTH('Résumé'); -- 7 (bytes)
SELECT CHAR_LENGTH('Résumé'); -- 6 (characters)
```

---

### Case Conversion Functions

| Function     | Description           |
| ------------ | --------------------- |
| `UPPER(str)` | Converts to uppercase |
| `LOWER(str)` | Converts to lowercase |

```sql
SELECT UPPER('mysql'); -- 'MYSQL'
```

---

### Substring Functions

| Function                        | Description          |
| ------------------------------- | -------------------- |
| `SUBSTRING(str, start, length)` | Extract substring    |
| `LEFT(str, length)`             | Leftmost characters  |
| `RIGHT(str, length)`            | Rightmost characters |

```sql
SELECT SUBSTRING('Database', 2, 4); -- 'atab'
SELECT LEFT('MySQL', 2); -- 'My'
SELECT RIGHT('MySQL', 2); -- 'QL'
```

---

### Trimming and Padding Functions

| Function                 | Description     |                             |                      |
| ------------------------ | --------------- | --------------------------- | -------------------- |
| \`TRIM(\[BOTH            | LEADING         | TRAILING] chars FROM str)\` | Removes spaces/chars |
| `LPAD(str, len, padstr)` | Pads left side  |                             |                      |
| `RPAD(str, len, padstr)` | Pads right side |                             |                      |

```sql
SELECT TRIM('   MySQL   '); -- 'MySQL'
SELECT LPAD('5', 3, '0'); -- '005'
SELECT RPAD('5', 3, '0'); -- '500'
```

---

### Search and Replace Functions

| Function                         | Description           |
| -------------------------------- | --------------------- |
| `INSTR(str, substr)`             | Position of substring |
| `LOCATE(substr, str)`            | Same as INSTR         |
| `REPLACE(str, from_str, to_str)` | Replace substring     |

```sql
SELECT INSTR('Database', 'base'); -- 5
SELECT REPLACE('2025-04-13', '-', '/'); -- '2025/04/13'
```

---

### Encoding Functions

| Function     | Description                   |
| ------------ | ----------------------------- |
| `HEX(str)`   | Converts to hexadecimal       |
| `UNHEX(hex)` | Converts hex to string        |
| `ASCII(str)` | ASCII code of first character |
| `CHAR(n)`    | Character from ASCII code     |

```sql
SELECT HEX('A'); -- '41'
SELECT CHAR(65); -- 'A'
```

---

### Other Useful Functions

| Function             | Description                  |
| -------------------- | ---------------------------- |
| `REVERSE(str)`       | Reverses string              |
| `REPEAT(str, count)` | Repeats string               |
| `FORMAT(num, d)`     | Number to string with commas |
| `QUOTE(str)`         | Returns quoted string        |

```sql
SELECT REVERSE('SQL'); -- 'LQS'
SELECT FORMAT(1234567.89, 2); -- '1,234,567.89'
```

---

### Usage Scenarios

* **Combine first and last names:**

  ```sql
  SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employees;
  ```

* **Email domain extraction:**

  ```sql
  SELECT SUBSTRING(email, LOCATE('@', email) + 1) AS domain FROM users;
  ```

* **Capitalize first letter only:**

  ```sql
  SELECT CONCAT(UPPER(LEFT(name, 1)), LOWER(SUBSTRING(name, 2))) FROM people;
  ```

---

### Conclusion

String functions in MySQL provide powerful tools for processing and transforming textual data efficiently. They are essential for formatting output, validating entries, and building clean reports or user interfaces.

---
