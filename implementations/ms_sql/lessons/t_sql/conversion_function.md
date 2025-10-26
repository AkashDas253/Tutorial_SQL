## Conversion Functions in T-SQL

**Conversion functions** in T-SQL are used to change data from one data type to another — for example, converting strings to numbers, dates to strings, or integers to decimals.
They are essential for data formatting, comparisons, aggregation, and interoperability between data types.

---

### Categories of Conversion Functions

| Category              | Description                         | Examples                                     |
| --------------------- | ----------------------------------- | -------------------------------------------- |
| Explicit Conversion   | Manual data type conversion         | `CAST()`, `CONVERT()`, `PARSE()`             |
| Safe Conversion       | Conversion with failure protection  | `TRY_CAST()`, `TRY_CONVERT()`, `TRY_PARSE()` |
| Implicit Conversion   | Automatic by SQL Server when needed | Automatic conversions in expressions         |
| Formatting Conversion | Converts to formatted string output | `FORMAT()`                                   |

---

### 1. **CAST()** — ANSI Standard Conversion

Used for explicit type conversion; compatible across RDBMS systems.

#### Syntax

```sql
CAST (expression AS data_type [(length)])
```

#### Example

```sql
SELECT 
    CAST('2025-10-24' AS DATE) AS ConvertedDate,
    CAST(123.45 AS INT) AS IntegerValue;
```

| Expression              | Conversion              | Result       |
| ----------------------- | ----------------------- | ------------ |
| `'2025-10-24'` → `DATE` | Converts string to date | `2025-10-24` |
| `123.45` → `INT`        | Truncates decimals      | `123`        |

---

### 2. **CONVERT()** — SQL Server-Specific Conversion

Performs similar conversion to `CAST()` but supports **style codes** for date/time and numeric formatting.

#### Syntax

```sql
CONVERT (data_type [(length)], expression [, style])
```

#### Example

```sql
SELECT 
    CONVERT(VARCHAR(10), GETDATE(), 103) AS FormattedDate,
    CONVERT(INT, 123.45) AS IntegerValue;
```

| Parameter    | Description                                                       |
| ------------ | ----------------------------------------------------------------- |
| `data_type`  | Target data type                                                  |
| `expression` | Source value                                                      |
| `style`      | Optional format style for `datetime`, `smalldatetime`, or `float` |

---

#### Common `style` Codes for Date Formatting

| Style | Format              | Example               |
| ----- | ------------------- | --------------------- |
| 101   | mm/dd/yyyy          | `10/24/2025`          |
| 103   | dd/mm/yyyy          | `24/10/2025`          |
| 112   | yyyymmdd            | `20251024`            |
| 120   | yyyy-mm-dd hh:mi:ss | `2025-10-24 14:45:00` |
| 126   | ISO 8601            | `2025-10-24T14:45:00` |

#### Numeric Style Example

```sql
SELECT CONVERT(VARCHAR, 123456.789, 1);  -- '123,456.8'
```

---

### 3. **PARSE()** — Culture-Aware String Conversion

Used to convert string representations of numbers or dates to actual numeric or date types, using **culture-specific formats**.

#### Syntax

```sql
PARSE (string_value AS data_type [USING culture])
```

#### Example

```sql
SELECT PARSE('24/10/2025' AS DATE USING 'en-GB');  -- British format
SELECT PARSE('10/24/2025' AS DATE USING 'en-US');  -- US format
```

| Feature           | Description                             |
| ----------------- | --------------------------------------- |
| Culture parameter | Optional, defines locale interpretation |
| Throws error      | If input string cannot be parsed        |

> ⚠️ Slower than `CAST()` or `CONVERT()` because it uses CLR (Common Language Runtime).

---

### 4. **TRY_CAST()**, **TRY_CONVERT()**, **TRY_PARSE()** — Safe Conversion Functions

These return `NULL` instead of raising an error when conversion fails — suitable for data cleaning and ETL processes.

| Function                                  | Description                 | Example                                                 | Result       |
| ----------------------------------------- | --------------------------- | ------------------------------------------------------- | ------------ |
| **TRY_CAST(expr AS type)**                | Safe version of `CAST()`    | `SELECT TRY_CAST('abc' AS INT);`                        | `NULL`       |
| **TRY_CONVERT(type, expr [, style])**     | Safe version of `CONVERT()` | `SELECT TRY_CONVERT(DATE, '2025-10-24', 23);`           | `2025-10-24` |
| **TRY_PARSE(expr AS type USING culture)** | Safe version of `PARSE()`   | `SELECT TRY_PARSE('24-10-2025' AS DATE USING 'fr-FR');` | `2025-10-24` |

> ✅ Recommended in production code when invalid data might appear.

---

### 5. **FORMAT()** — Convert to Formatted String

Converts date, time, or numeric expressions to a string in a specified .NET format.

#### Syntax

```sql
FORMAT (value, format [, culture])
```

#### Examples

```sql
SELECT 
    FORMAT(GETDATE(), 'dddd, MMMM dd, yyyy') AS LongDate,
    FORMAT(1234567.89, 'N2') AS NumberFormatted,
    FORMAT(GETDATE(), 'hh:mm tt', 'en-US') AS Time12Hour;
```

| Expression | Format                  | Output                     |
| ---------- | ----------------------- | -------------------------- |
| Date       | `'dddd, MMMM dd, yyyy'` | `Friday, October 24, 2025` |
| Number     | `'N2'`                  | `1,234,567.89`             |
| Time       | `'hh:mm tt'`            | `02:45 PM`                 |

> ⚠️ `FORMAT()` uses CLR and is slower; use only for presentation layers.

---

### 6. Implicit Conversion

SQL Server automatically converts data types when compatible types are used together in an expression.

#### Example

```sql
SELECT 'Value: ' + CAST(100 AS VARCHAR);
```

→ `'Value: 100'`

If implicit conversion occurs:

* **From lower precedence to higher** (string → int → float)
* May cause **performance issues** or **data loss** if automatic truncation happens.

#### Data Type Precedence (Low → High)

`char` → `varchar` → `nchar` → `nvarchar` → `binary` → `varbinary` → `datetime` → `float` → `decimal` → `money` → `int`

> Always explicitly convert to avoid unintended conversions.

---

### 7. Comparison of Conversion Functions

| Function          | Standard  | Error Handling   | Formatting Support   | Performance | Culture Support |
| ----------------- | --------- | ---------------- | -------------------- | ----------- | --------------- |
| **CAST()**        | ANSI      | Error on failure | No                   | Fast        | No              |
| **CONVERT()**     | T-SQL     | Error on failure | Yes (style)          | Fast        | No              |
| **PARSE()**       | CLR-based | Error on failure | Yes                  | Slow        | Yes             |
| **TRY_CAST()**    | ANSI      | Returns NULL     | No                   | Fast        | No              |
| **TRY_CONVERT()** | T-SQL     | Returns NULL     | Yes (style)          | Fast        | No              |
| **TRY_PARSE()**   | CLR-based | Returns NULL     | Yes                  | Slow        | Yes             |
| **FORMAT()**      | .NET      | N/A              | Full .NET formatting | Slow        | Yes             |

---

### 8. Practical Examples

#### Convert Number to String with Format

```sql
SELECT FORMAT(98765.432, 'N2');  -- '98,765.43'
```

#### Convert String to Date with Style

```sql
SELECT CONVERT(DATE, '24/10/2025', 103);  -- '2025-10-24'
```

#### Convert Invalid Value Safely

```sql
SELECT TRY_CAST('NotADate' AS DATE);  -- NULL (safe)
```

#### Combine CAST and CONCAT

```sql
SELECT 'The year is ' + CAST(YEAR(GETDATE()) AS VARCHAR);
```

---

### 9. Concept Diagram

```mermaid
flowchart TD;
    A[Input Expression] --> B{Explicit or Implicit Conversion?};
    B --> C[Explicit: CAST, CONVERT, PARSE];
    B --> D[Implicit: Automatic Engine Conversion];
    C --> E{Safe Version?};
    E --> F[TRY_CAST / TRY_CONVERT / TRY_PARSE];
    E --> G[Standard Conversion];
    G --> H[Formatted Output using FORMAT()];
```

---

### 10. Best Practices

* Use **CAST()** for portability and **CONVERT()** for SQL Server-specific features.
* Use **TRY_*** functions for safe conversions in production ETL scripts.
* Use **FORMAT()** only for final display, not inside heavy computations.
* Avoid implicit conversions in joins or WHERE clauses (can cause index scan).
* Use appropriate **style codes** for consistent date/time representation.

---
