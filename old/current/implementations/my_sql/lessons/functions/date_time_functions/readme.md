## Date and Time Functions in MySQL

**Date and Time functions** in MySQL handle operations involving date and time values, such as retrieval, formatting, conversion, and arithmetic.

---
 
### 🔹 Inner Index

* [Current Date and Time](#current-date-and-time)
* [Extraction Functions](#extraction-functions)
* [Formatting Functions](#formatting-functions)
* [Arithmetic Functions](#arithmetic-functions)
* [Conversion Functions](#conversion-functions)
* [Difference and Comparison Functions](#difference-and-comparison-functions)
* [Other Useful Functions](#other-useful-functions)
* [Usage Scenarios](#usage-scenarios)

---

### Current Date and Time

| Function     | Description                                   |
| ------------ | --------------------------------------------- |
| `NOW()`      | Current date and time (`YYYY-MM-DD HH:MM:SS`) |
| `CURDATE()`  | Current date only                             |
| `CURTIME()`  | Current time only                             |
| `SYSDATE()`  | Returns time of function execution            |
| `UTC_DATE()` | UTC date                                      |
| `UTC_TIME()` | UTC time                                      |

```sql
SELECT NOW(); -- '2025-04-13 10:45:12'
```

---

### Extraction Functions

| Function          | Description                  |
| ----------------- | ---------------------------- |
| `YEAR(date)`      | Extracts year                |
| `MONTH(date)`     | Extracts month               |
| `DAY(date)`       | Extracts day of month        |
| `HOUR(time)`      | Extracts hour                |
| `MINUTE(time)`    | Extracts minute              |
| `SECOND(time)`    | Extracts second              |
| `DAYNAME(date)`   | Day name (e.g., Sunday)      |
| `MONTHNAME(date)` | Month name (e.g., April)     |
| `DAYOFWEEK(date)` | 1 = Sunday, 2 = Monday, etc. |
| `WEEK(date)`      | Week number                  |
| `QUARTER(date)`   | Quarter of year              |

```sql
SELECT MONTH('2025-04-13'); -- 4
SELECT DAYNAME('2025-04-13'); -- 'Sunday'
```

---

### Formatting Functions

| Function                    | Description            |
| --------------------------- | ---------------------- |
| `DATE_FORMAT(date, format)` | Formats date as string |
| `TIME_FORMAT(time, format)` | Formats time as string |

```sql
SELECT DATE_FORMAT(NOW(), '%W, %M %d %Y'); -- 'Sunday, April 13 2025'
SELECT TIME_FORMAT(NOW(), '%H:%i'); -- '10:45'
```

---

### Arithmetic Functions

| Function                             | Description              |
| ------------------------------------ | ------------------------ |
| `DATE_ADD(date, INTERVAL expr unit)` | Adds time to date        |
| `DATE_SUB(date, INTERVAL expr unit)` | Subtracts time from date |
| `ADDDATE(date, INTERVAL expr unit)`  | Alias of `DATE_ADD`      |
| `SUBDATE(date, INTERVAL expr unit)`  | Alias of `DATE_SUB`      |

```sql
SELECT DATE_ADD('2025-04-13', INTERVAL 10 DAY); -- '2025-04-23'
SELECT SUBDATE('2025-04-13', INTERVAL 2 MONTH); -- '2025-02-13'
```

---

### Conversion Functions

| Function                   | Description                    |
| -------------------------- | ------------------------------ |
| `STR_TO_DATE(str, format)` | Converts string to date        |
| `UNIX_TIMESTAMP(date)`     | Converts to UNIX time          |
| `FROM_UNIXTIME(unix)`      | Converts UNIX time to datetime |
| `CAST(expr AS DATE)`       | Casts to DATE                  |

```sql
SELECT STR_TO_DATE('13-04-2025', '%d-%m-%Y'); -- '2025-04-13'
```

---

### Difference and Comparison Functions

| Function                      | Description                        |
| ----------------------------- | ---------------------------------- |
| `DATEDIFF(date1, date2)`      | Difference in days (date1 - date2) |
| `TIMEDIFF(time1, time2)`      | Time difference (hh\:mm\:ss)       |
| `TIMESTAMPDIFF(unit, d1, d2)` | Diff by unit (e.g., DAY, HOUR)     |
| `TIMESTAMP(date, time)`       | Combines date and time             |

```sql
SELECT DATEDIFF('2025-04-20', '2025-04-13'); -- 7
SELECT TIMESTAMPDIFF(MINUTE, '10:00:00', '10:45:00'); -- 45
```

---

### Other Useful Functions

| Function                  | Description                        |
| ------------------------- | ---------------------------------- |
| `LAST_DAY(date)`          | Returns last day of the month      |
| `MAKEDATE(year, day)`     | Creates date from year and day     |
| `MAKETIME(h, m, s)`       | Creates time                       |
| `EXTRACT(unit FROM date)` | Extracts part like `MONTH`, `YEAR` |

```sql
SELECT LAST_DAY('2025-02-11'); -- '2025-02-28'
SELECT EXTRACT(YEAR FROM NOW()); -- 2025
```

---

### Usage Scenarios

* **Get employees hired this year:**

  ```sql
  SELECT * FROM employees WHERE YEAR(hire_date) = YEAR(CURDATE());
  ```

* **Add 7 days to current date:**

  ```sql
  SELECT DATE_ADD(CURDATE(), INTERVAL 7 DAY);
  ```

* **Get age of a person:**

  ```sql
  SELECT TIMESTAMPDIFF(YEAR, birthdate, CURDATE()) AS age FROM persons;
  ```

* **Format timestamp for UI:**

  ```sql
  SELECT DATE_FORMAT(order_date, '%d-%m-%Y %h:%i %p') FROM orders;
  ```

---

### Conclusion

Date and Time functions are vital in any time-sensitive application. MySQL provides a wide set of functions for formatting, arithmetic, parsing, and analyzing dates and times effectively.

---
