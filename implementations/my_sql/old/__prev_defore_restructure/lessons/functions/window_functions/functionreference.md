
# MySQL Window Functions Cheatsheet

| **Category**  | **Function**     | **Syntax**                                     | **Parameters (default values)** | **Description**                           |
| ------------- | ---------------- | ---------------------------------------------- | ------------------------------- | ----------------------------------------- |
| **Aggregate** | `SUM`            | `SUM(expr) OVER (...)`                         | `expr`                          | Sum of values                             |
|               | `AVG`            | `AVG(expr) OVER (...)`                         | `expr`                          | Average of values                         |
|               | `MIN`            | `MIN(expr) OVER (...)`                         | `expr`                          | Minimum value                             |
|               | `MAX`            | `MAX(expr) OVER (...)`                         | `expr`                          | Maximum value                             |
|               | `COUNT`          | `COUNT(expr) OVER (...)`                       | `expr`                          | Count of values                           |
|               | `BIT_AND`        | `BIT_AND(expr) OVER (...)`                     | `expr`                          | Bitwise AND of values                     |
|               | `BIT_OR`         | `BIT_OR(expr) OVER (...)`                      | `expr`                          | Bitwise OR of values                      |
|               | `BIT_XOR`        | `BIT_XOR(expr) OVER (...)`                     | `expr`                          | Bitwise XOR of values                     |
|               | `STDDEV_POP`     | `STDDEV_POP(expr) OVER (...)`                  | `expr`                          | Population standard deviation             |
|               | `STDDEV_SAMP`    | `STDDEV_SAMP(expr) OVER (...)`                 | `expr`                          | Sample standard deviation                 |
|               | `VAR_POP`        | `VAR_POP(expr) OVER (...)`                     | `expr`                          | Population variance                       |
|               | `VAR_SAMP`       | `VAR_SAMP(expr) OVER (...)`                    | `expr`                          | Sample variance                           |
| **Ranking**   | `ROW_NUMBER`     | `ROW_NUMBER() OVER (...)`                      | none                            | Sequential row number                     |
|               | `RANK`           | `RANK() OVER (...)`                            | none                            | Rank with gaps                            |
|               | `DENSE_RANK`     | `DENSE_RANK() OVER (...)`                      | none                            | Rank without gaps                         |
|               | `PERCENT_RANK`   | `PERCENT_RANK() OVER (...)`                    | none                            | Relative rank between 0–1                 |
|               | `CUME_DIST`      | `CUME_DIST() OVER (...)`                       | none                            | Cumulative distribution                   |
|               | `NTILE`          | `NTILE(n) OVER (...)`                          | `n` (no default, must specify)  | Divides rows into n buckets               |
| **Value**     | `FIRST_VALUE`    | `FIRST_VALUE(expr) OVER (...)`                 | `expr`                          | First value in frame                      |
|               | `LAST_VALUE`     | `LAST_VALUE(expr) OVER (...)`                  | `expr`                          | Last value in frame                       |
|               | `NTH_VALUE`      | `NTH_VALUE(expr, n) OVER (...)`                | `expr`, `n` (no default)        | nth value in frame                        |
|               | `LEAD`           | `LEAD(expr [, offset [, default]]) OVER (...)` | `offset=1`, `default=NULL`      | Value from following row                  |
|               | `LAG`            | `LAG(expr [, offset [, default]]) OVER (...)`  | `offset=1`, `default=NULL`      | Value from preceding row                  |
| **Special**   | `JSON_ARRAYAGG`  | `JSON_ARRAYAGG(expr) OVER (...)`               | `expr`                          | Aggregates values as JSON array           |
|               | `JSON_OBJECTAGG` | `JSON_OBJECTAGG(key, value) OVER (...)`        | `key`, `value`                  | Aggregates key-value pairs as JSON object |

---

# Window Definition Components

| **Clause**           | **Syntax**                                                                                | **Options**               | **Default**         | **Purpose**                    |                                                                      |                                               |
| -------------------- | ----------------------------------------------------------------------------------------- | ------------------------- | ------------------- | ------------------------------ | -------------------------------------------------------------------- | --------------------------------------------- |
| **PARTITION**        | `PARTITION BY expr_list`                                                                  | Any valid expression list | Entire result set   | Splits rows into partitions    |                                                                      |                                               |
| **ORDER**            | \`ORDER BY expr\_list \[ASC                                                               | DESC]\`                   | ASC (default), DESC | Not required                   | Defines row sequence                                                 |                                               |
| **FRAME**            | \`ROWS                                                                                    | RANGE                     | GROUPS\`            | Frame boundaries + exclusions  | `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` (for aggregates) | Defines which rows participate in calculation |
| **Frame Boundaries** | `UNBOUNDED PRECEDING`, `n PRECEDING`, `CURRENT ROW`, `n FOLLOWING`, `UNBOUNDED FOLLOWING` |                           |                     | Defines start and end of frame |                                                                      |                                               |
| **Frame Exclusions** | `EXCLUDE CURRENT ROW`, `EXCLUDE GROUP`, `EXCLUDE TIES`, `EXCLUDE NO OTHERS`               |                           | `EXCLUDE NO OTHERS` | Excludes rows from frame       |                                                                      |                                               |

---
 