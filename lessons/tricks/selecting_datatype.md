
## General Principles for Data Type Selection

* **Store data in its smallest valid type** → saves space, improves performance.
* **Use exact types for precision** (e.g., `INT`, `DECIMAL`) and approximate for scientific values (e.g., `FLOAT`).
* **Choose fixed-length vs variable-length** based on expected size variation.
* **Consider NULL allowance** → influences storage and constraints.
* **Portability** → some DBMS have unique types (e.g., `NUMBER` in Oracle vs `DECIMAL` in SQL Server).

---

## Numeric Data Types

| Type                                      | Usage                   | Notes                                         |
| ----------------------------------------- | ----------------------- | --------------------------------------------- |
| `TINYINT` / `SMALLINT` / `INT` / `BIGINT` | Whole numbers           | Select based on range required.               |
| `DECIMAL(p,s)` / `NUMERIC(p,s)`           | Exact precision numbers | Use for money, financial values.              |
| `FLOAT` / `REAL` / `DOUBLE PRECISION`     | Approximate numbers     | Use for scientific or imprecise calculations. |
| `BIT` / `BOOLEAN`                         | Logical true/false      | Some DBMS emulate with `CHAR(1)` or `INT`.    |

---

## Character Data Types

| Type            | Usage                   | Notes                                             |
| --------------- | ----------------------- | ------------------------------------------------- |
| `CHAR(n)`       | Fixed-length strings    | Better for uniform-length data (e.g., codes).     |
| `VARCHAR(n)`    | Variable-length strings | General text, up to defined limit.                |
| `TEXT` / `CLOB` | Very large text         | Non-standard handling, use for long descriptions. |

---

## Date and Time Data Types

| Type                     | Usage                   | Notes                                     |
| ------------------------ | ----------------------- | ----------------------------------------- |
| `DATE`                   | Stores year, month, day | Standard.                                 |
| `TIME`                   | Stores time of day      | Precision may vary by DBMS.               |
| `DATETIME` / `TIMESTAMP` | Full date + time        | Common for logs, transactions.            |
| `INTERVAL`               | Time span               | Useful in ANSI SQL, limited DBMS support. |

---

## Binary Data Types

| Type           | Usage                  | Notes                     |
| -------------- | ---------------------- | ------------------------- |
| `BINARY(n)`    | Fixed-length binary    | For keys, hashes.         |
| `VARBINARY(n)` | Variable-length binary | For encoded binary data.  |
| `BLOB`         | Large binary objects   | Images, media, documents. |

---

## Special / Advanced Types

| Type                     | Usage                  | Notes                                                 |
| ------------------------ | ---------------------- | ----------------------------------------------------- |
| `ENUM`                   | Restricted string list | MySQL/PostgreSQL; enforces controlled values.         |
| `SET`                    | Multiple-choice list   | MySQL-specific.                                       |
| `UUID`                   | Unique identifiers     | Preferred over large strings for IDs.                 |
| `JSON`                   | Structured semi-data   | Native in PostgreSQL, MySQL; use for flexible schema. |
| `XML`                    | Semi-structured data   | Supported in some DBMS.                               |
| `GEOMETRY` / `GEOGRAPHY` | Spatial data           | GIS support in modern RDBMS.                          |

---

## Choosing Between Similar Types

* **CHAR vs VARCHAR**:

  * Use `CHAR` for fixed-length (e.g., country codes).
  * Use `VARCHAR` for variable-length (e.g., names).
* **DECIMAL vs FLOAT**:

  * Use `DECIMAL` for money/accuracy.
  * Use `FLOAT` for scientific approximations.
* **DATETIME vs TIMESTAMP**:

  * `TIMESTAMP` often auto-updates and supports time zones (DBMS-specific).
  * `DATETIME` more general.
* **TEXT vs VARCHAR**:

  * Use `VARCHAR` unless storing extremely large text.

---

## Constraints and Nullability

* Add `NOT NULL` where appropriate for integrity.
* Use `CHECK` constraints for valid ranges (e.g., `CHECK (age >= 0)`).
* Define defaults (`DEFAULT GETDATE()`, `DEFAULT 0`).

---

## Performance Considerations

* Indexing works best on smaller, fixed-size types.
* Avoid indexing large text/blob fields.
* Prefer numeric keys (`INT`, `BIGINT`) over string keys for joins and primary keys.
* Consider storage engine handling of NULLs (may add overhead).

---

## Flowchart

```mermaid
flowchart TD;
    A[Start: What kind of data?] --> B[Numeric];
    A --> C[Text/String];
    A --> D[Date/Time];
    A --> E[Binary/Files];
    A --> F[Special/Advanced];

    %% Numeric Branch
    B --> B1{Whole numbers?};
    B1 -->|Yes| B2[Range small? → TINYINT/SMALLINT];
    B1 -->|Yes, large| B3[INT/BIGINT];
    B1 -->|No| B4{Need exact precision?};
    B4 -->|Yes| B5[DECIMAL/NUMERIC];
    B4 -->|No| B6[FLOAT/REAL/DOUBLE];
    B --> B7[Logical values → BOOLEAN/BIT];

    %% Text Branch
    C --> C1{Fixed or variable length?};
    C1 -->|Fixed| C2[CHAR(n)];
    C1 -->|Variable| C3{Max size needed?};
    C3 -->|Small/Medium| C4[VARCHAR(n)];
    C3 -->|Large text| C5[TEXT/CLOB];

    %% Date/Time Branch
    D --> D1{What precision needed?};
    D1 -->|Date only| D2[DATE];
    D1 -->|Time only| D3[TIME];
    D1 -->|Date+Time| D4[DATETIME/TIMESTAMP];
    D1 -->|Duration| D5[INTERVAL];

    %% Binary Branch
    E --> E1{Size fixed or variable?};
    E1 -->|Fixed| E2[BINARY(n)];
    E1 -->|Variable| E3[VARBINARY(n)];
    E1 -->|Large object| E4[BLOB];

    %% Special Types
    F --> F1[ENUM/SET → Restricted values];
    F --> F2[UUID → Unique identifiers];
    F --> F3[JSON/XML → Semi-structured data];
    F --> F4[GEOMETRY/GEOGRAPHY → Spatial data];


```