## Built-in Functions in PL/SQL

PL/SQL provides a rich set of **built-in functions** that can simplify common tasks, such as string manipulation, numeric calculations, date operations, and more. These functions can be used in SQL queries, PL/SQL blocks, and procedural code to perform various operations without needing to write custom logic.

---

### **Categories of Built-in Functions**

| **Category**                  | **Description**                                                              |
|-------------------------------|------------------------------------------------------------------------------|
| **String Functions**           | Functions for manipulating and querying string data.                         |
| **Numeric Functions**          | Functions for performing mathematical operations.                            |
| **Date Functions**             | Functions for working with dates and times.                                  |
| **Conversion Functions**       | Functions for converting between data types.                                 |
| **Aggregate Functions**        | Functions for performing aggregate calculations (e.g., `SUM`, `AVG`).       |
| **General Functions**          | Miscellaneous functions for various purposes, such as handling NULL values. |

---

### **String Functions**

| **Function**           | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `CONCAT(str1, str2)`    | Concatenates two strings.                                                        |
| `LENGTH(str)`           | Returns the length of a string in characters.                                   |
| `SUBSTR(str, start, len)` | Extracts a substring from a string, starting at position `start` for `len` characters. |
| `INSTR(str, substr)`    | Returns the position of the first occurrence of `substr` in `str`.             |
| `TRIM(str)`             | Removes leading and trailing spaces from a string.                             |
| `UPPER(str)`            | Converts a string to uppercase.                                                 |
| `LOWER(str)`            | Converts a string to lowercase.                                                 |
| `REPLACE(str, old, new)` | Replaces all occurrences of `old` with `new` in the string `str`.              |
| `RPAD(str, length, pad)` | Pads the right side of a string with `pad` until the total length is `length`. |
| `LPAD(str, length, pad)` | Pads the left side of a string with `pad` until the total length is `length`.  |

#### **Example**

```plsql
DECLARE
  str VARCHAR2(50) := 'Hello, World!';
BEGIN
  DBMS_OUTPUT.PUT_LINE(SUBSTR(str, 1, 5)); -- Output: Hello
  DBMS_OUTPUT.PUT_LINE(UPPER(str)); -- Output: HELLO, WORLD!
END;
```

---

### **Numeric Functions**

| **Function**           | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `ROUND(number, digits)` | Rounds a number to a specified number of decimal places.                       |
| `TRUNC(number, digits)` | Truncates a number to a specified number of decimal places without rounding.   |
| `MOD(x, y)`            | Returns the remainder when `x` is divided by `y`.                              |
| `CEIL(number)`         | Returns the smallest integer greater than or equal to the specified number.    |
| `FLOOR(number)`        | Returns the largest integer less than or equal to the specified number.        |
| `ABS(number)`          | Returns the absolute value of a number.                                        |
| `POWER(base, exponent)` | Returns the value of `base` raised to the power of `exponent`.                 |

#### **Example**

```plsql
DECLARE
  num NUMBER := -5.67;
BEGIN
  DBMS_OUTPUT.PUT_LINE(ABS(num));   -- Output: 5.67
  DBMS_OUTPUT.PUT_LINE(ROUND(num, 1)); -- Output: -5.7
  DBMS_OUTPUT.PUT_LINE(CEIL(4.2));  -- Output: 5
END;
```

---

### **Date Functions**

| **Function**           | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `SYSDATE`              | Returns the current system date and time.                                        |
| `CURRENT_DATE`         | Returns the current date in the session's time zone.                            |
| `TO_DATE(string, format)` | Converts a string to a date, based on the given format.                         |
| `TO_CHAR(date, format)` | Converts a date to a string based on the given format.                          |
| `ADD_MONTHS(date, months)` | Adds a specified number of months to a date.                                    |
| `MONTHS_BETWEEN(date1, date2)` | Returns the number of months between two dates.                               |
| `NEXT_DAY(date, day)`  | Returns the date of the next specified day after the given date.               |
| `LAST_DAY(date)`       | Returns the last day of the month for the given date.                          |
| `EXTRACT(unit FROM date)` | Extracts a specific component (e.g., year, month, day) from a date.             |

#### **Example**

```plsql
DECLARE
  current_date DATE := SYSDATE;
BEGIN
  DBMS_OUTPUT.PUT_LINE(TO_CHAR(current_date, 'DD-MON-YYYY')); -- Output: 16-JAN-2025
  DBMS_OUTPUT.PUT_LINE(ADD_MONTHS(current_date, 2));          -- Output: 16-MAR-2025
END;
```

---

### **Conversion Functions**

| **Function**           | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `TO_NUMBER(expr)`      | Converts an expression to a numeric value.                                       |
| `TO_CHAR(expr)`        | Converts an expression to a string.                                              |
| `TO_DATE(expr, format)` | Converts a string to a date using the specified format.                         |
| `CAST(expr AS type)`   | Converts an expression to the specified data type.                              |
| `CONVERT(expr, from_charset, to_charset)` | Converts a string from one character set to another.                       |

#### **Example**

```plsql
DECLARE
  str VARCHAR2(20) := '2025-01-16';
  date_value DATE;
BEGIN
  date_value := TO_DATE(str, 'YYYY-MM-DD');
  DBMS_OUTPUT.PUT_LINE(date_value); -- Output: 16-JAN-2025
END;
```

---

### **Aggregate Functions**

These functions are used to calculate summary values from multiple rows of data.

| **Function**           | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `SUM(expr)`            | Returns the sum of a numeric expression.                                        |
| `AVG(expr)`            | Returns the average of a numeric expression.                                    |
| `COUNT(expr)`          | Returns the number of rows in a query result.                                   |
| `MIN(expr)`            | Returns the smallest value of an expression.                                    |
| `MAX(expr)`            | Returns the largest value of an expression.                                     |

#### **Example**

```plsql
DECLARE
  total_salary NUMBER;
BEGIN
  SELECT SUM(salary) INTO total_salary FROM employees WHERE department_id = 10;
  DBMS_OUTPUT.PUT_LINE('Total salary: ' || total_salary);
END;
```

---

### **General Functions**

| **Function**           | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `NVL(expr1, expr2)`    | Returns `expr1` if it is not NULL, otherwise returns `expr2`.                   |
| `COALESCE(expr1, expr2)` | Returns the first non-NULL expression among its arguments.                      |
| `DECODE(expr, search_value, result1, default_result)` | Performs a conditional query. If `expr` equals `search_value`, returns `result1`; otherwise, returns `default_result`. |
| `CASE WHEN`            | A conditional expression that evaluates conditions and returns a value based on the result. |

#### **Example**

```plsql
DECLARE
  value NUMBER := NULL;
BEGIN
  DBMS_OUTPUT.PUT_LINE(NVL(value, 100)); -- Output: 100
  DBMS_OUTPUT.PUT_LINE(COALESCE(value, 200, 300)); -- Output: 200
END;
```

---

### **Summary**

PL/SQL provides a wide range of built-in functions across various categories to streamline data manipulation and processing tasks:

- **String functions**: For text processing and transformation.
- **Numeric functions**: For mathematical operations.
- **Date functions**: For working with date and time.
- **Conversion functions**: For type conversions.
- **Aggregate functions**: For summary calculations.
- **General functions**: For handling NULL values and conditional operations.

These built-in functions help in writing more concise and efficient code. Understanding their usage and applying them appropriately is key to mastering PL/SQL programming.
