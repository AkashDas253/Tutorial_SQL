## PostgreSQL – Sequences

### Overview

A **sequence** in PostgreSQL is a **special database object that generates a sequential series of unique numeric values**, commonly used for **auto-incrementing primary keys**. Sequences are independent of tables and can be used in multiple tables or applications.

### Key Concepts

* **Purpose**

  * Generate unique identifiers for table rows.
  * Avoid conflicts in concurrent inserts.
  * Provide customizable numbering sequences.

* **Sequence Properties**

  * **Start Value**: Initial number in the sequence (default 1).
  * **Increment**: Step size between consecutive numbers (default 1, can be negative for descending sequences).
  * **Min/Max Values**: Define lower and upper bounds.
  * **Cycle Option**:

    * **CYCLE**: Sequence restarts when max is reached.
    * **NO CYCLE**: Sequence stops at max value.
  * **Cache**:

    * Number of sequence values preallocated in memory for performance.

* **Sequence Operations**

  * `CREATE SEQUENCE` – Define a new sequence.
  * `ALTER SEQUENCE` – Modify properties (start, increment, min/max, cache, cycle).
  * `DROP SEQUENCE` – Delete a sequence.
  * `NEXTVAL(sequence_name)` – Get the next value and advance the sequence.
  * `CURRVAL(sequence_name)` – Get the current value without incrementing.
  * `SETVAL(sequence_name, value)` – Set the sequence to a specific value.

* **Integration with Tables**

  * Commonly used with `SERIAL` or `BIGSERIAL` column types (auto-created sequences).
  * Can also use `GENERATED AS IDENTITY` columns (SQL standard-compliant approach).
  * Sequences are independent; multiple tables can share a sequence if desired.

* **Concurrency**

  * Sequences are **safe for concurrent access**.
  * Each `NEXTVAL` call is atomic, ensuring unique values even under high concurrency.

* **Storage**

  * Stored in the **system catalog `pg_sequence`**.
  * Values cached in memory for performance; WAL ensures durability.

### Summary

Sequences in PostgreSQL provide a **flexible, high-performance mechanism** for generating unique numeric identifiers:

* Configurable start, increment, min/max, cycle, and cache
* Independent of tables, reusable across multiple objects
* Concurrency-safe, suitable for high-insert scenarios
* Commonly integrated with `SERIAL`, `BIGSERIAL`, and identity columns

---
