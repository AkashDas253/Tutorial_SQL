## PostgreSQL – Set Operations

### Overview

**Set operations** in PostgreSQL combine the results of two or more queries into a **single result set**. They are used to perform operations like **union, intersection, and difference** on query results.

### Key Concepts

* **Purpose**

  * Combine multiple SELECT queries into one result.
  * Eliminate or include duplicates based on requirements.
  * Simplify complex queries and reporting across multiple tables.

* **Types of Set Operations**

  * **UNION**

    * Combines results of two queries and **removes duplicates** by default.
    * Syntax:

      ```sql
      SELECT column1 FROM table1
      UNION
      SELECT column1 FROM table2;
      ```
    * **UNION ALL** – Combines results and **keeps duplicates**.
  * **INTERSECT**

    * Returns only rows **common to both queries**.
    * Syntax:

      ```sql
      SELECT column1 FROM table1
      INTERSECT
      SELECT column1 FROM table2;
      ```
    * **INTERSECT ALL** – Keeps duplicates in the intersection.
  * **EXCEPT**

    * Returns rows from the **first query that are not in the second**.
    * Syntax:

      ```sql
      SELECT column1 FROM table1
      EXCEPT
      SELECT column1 FROM table2;
      ```
    * **EXCEPT ALL** – Keeps duplicates in the difference.

* **Rules and Considerations**

  * Queries must have the **same number of columns**.
  * Corresponding columns must have **compatible data types**.
  * Column names in the result are taken from the **first query**.
  * Order can be controlled using `ORDER BY` at the end of the combined query.
  * Parentheses can be used to **control precedence** of multiple set operations.

* **Use Cases**

  * Combine datasets from multiple tables or queries.
  * Filter out overlapping or duplicate data.
  * Perform comparisons and differences between datasets.

### Summary

Set operations in PostgreSQL allow **combining query results logically**:

* UNION / UNION ALL – combine results with or without duplicates
* INTERSECT / INTERSECT ALL – get common rows
* EXCEPT / EXCEPT ALL – get rows in one set but not the other
* Requires **matching column counts and compatible types**
* Useful for **data comparison, aggregation, and reporting**

---
