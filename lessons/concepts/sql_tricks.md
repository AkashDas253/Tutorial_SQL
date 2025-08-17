## SQL Tricks - Comprehensive Concepts List

#### **Query Optimization Tricks**

* Index usage

  * Covering indexes
  * Composite indexes
  * Partial indexes
* Query rewriting

  * Using `EXISTS` vs `IN`
  * Avoiding `SELECT *`
  * Using `JOIN` instead of subquery
* Execution plan analysis

  * `EXPLAIN` / `EXPLAIN ANALYZE`
  * Query cost interpretation

#### **Conditional Logic & Shortcuts**

* `CASE` expressions

  * Inline conditional transformations
  * Aggregating conditional counts
* Boolean logic tricks

  * `AND` / `OR` short-circuiting
  * `COALESCE` for default values
  * `NULLIF` for avoiding division by zero

#### **String & Text Tricks**

* Concatenation techniques

  * `||` operator, `CONCAT()`
* Pattern matching

  * `LIKE` with wildcards
  * `SIMILAR TO` / regex matching
* String manipulation

  * `SUBSTRING`, `LEFT`, `RIGHT`
  * `TRIM`, `REPLACE`, `TRANSLATE`

#### **Date & Time Tricks**

* Current date/time functions

  * `NOW()`, `CURRENT_DATE`, `CURRENT_TIMESTAMP`
* Date arithmetic

  * Adding/subtracting intervals
  * `AGE()` function
* Extracting parts

  * `EXTRACT(YEAR FROM date_column)`
  * `DATE_PART()` / `DATE_TRUNC()`

#### **Aggregate & Window Tricks**

* Window functions

  * `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`
  * `LEAD()` / `LAG()` for previous/next values
  * `SUM() OVER (PARTITION BY ...)`
* Conditional aggregation

  * `COUNT(CASE WHEN ...)`
  * `SUM(CASE WHEN ...)`
* Grouping sets

  * `ROLLUP`, `CUBE`, `GROUPING SETS`

#### **Join & Subquery Tricks**

* Lateral joins

  * `LATERAL` / `CROSS APPLY`
* Self-joins for hierarchical data
* Anti-joins

  * `NOT EXISTS` / `LEFT JOIN ... IS NULL`
* Inline subqueries

  * Using subqueries in `SELECT` or `FROM`
  * Correlated subqueries

#### **Set & Mathematical Tricks**

* `UNION` vs `UNION ALL`
* `INTERSECT`, `EXCEPT`
* Modulo operations

  * `MOD()` / `%` for cycling or pattern-based selection
* Generating sequences

  * `GENERATE_SERIES()`
  * Recursive CTEs

#### **CTEs & Recursive Tricks**

* Common Table Expressions (CTEs)

  * Breaking complex queries
  * Materializing results
* Recursive CTEs

  * Hierarchies / trees
  * Factorials or cumulative sequences

#### **Pivoting & Unpivoting Tricks**

* Dynamic pivot

  * `crosstab()` in PostgreSQL
* Manual pivot

  * `CASE WHEN` aggregation for rows-to-columns
* Unpivot

  * `UNION ALL` for columns-to-rows

#### **JSON & Array Tricks**

* JSON handling

  * `JSON_AGG()`, `JSON_OBJECT_AGG()`
  * `->` / `->>` / `#>` operators
* Array operations

  * `ARRAY_AGG()`
  * `UNNEST()` for flattening

#### **Temporary / Inline Tricks**

* Temporary tables

  * `CREATE TEMP TABLE`
* Inline tables

  * `VALUES` clause for ad-hoc data
* Using `WITH` for modular query parts

#### **Performance / Miscellaneous Tricks**

* Upsert / merge

  * `INSERT ... ON CONFLICT DO UPDATE`
  * `MERGE` statement
* Limiting results efficiently

  * `LIMIT` / `TOP`
  * Using `FETCH FIRST n ROWS ONLY`
* Random sampling

  * `TABLESAMPLE`, `ORDER BY RANDOM()`
* Index hints (implementation-specific)

  * Force index usage or avoidance

#### **Data Cleaning & Transformation Tricks**

* Removing duplicates

  * `DISTINCT ON` / `ROW_NUMBER()` filtering
* Pivoted null handling

  * `COALESCE`, `NULLIF`
* Normalization shortcuts

  * String trimming, case conversion
  * `UPPER()` / `LOWER()` for matching

---
