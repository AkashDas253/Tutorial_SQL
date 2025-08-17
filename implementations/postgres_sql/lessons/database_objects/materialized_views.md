## PostgreSQL – Materialized Views

### Overview

A **materialized view** in PostgreSQL is a **physical copy of the result of a query** stored on disk. Unlike regular views, materialized views **persist data**, which improves performance for complex or frequently accessed queries but requires **manual or scheduled refresh** to stay up-to-date.

### Key Concepts

* **Purpose**

  * Improve query performance by storing precomputed results.
  * Avoid recalculating expensive joins, aggregations, or transformations.
  * Provide a snapshot of data for reporting and analytics.

* **Creation**

  * `CREATE MATERIALIZED VIEW view_name AS SELECT ...`
  * Can include joins, aggregations, and complex expressions.
  * Optional `WITH DATA` (default) creates and populates immediately.
  * `WITH NO DATA` creates an empty structure for deferred population.

* **Refresh**

  * **Manual Refresh**: `REFRESH MATERIALIZED VIEW view_name`

    * Recomputes the query result and updates the stored data.
  * **Concurrent Refresh**: `REFRESH MATERIALIZED VIEW CONCURRENTLY view_name`

    * Allows queries to continue using the old data while refreshing.
    * Requires a **unique index** on the materialized view.
  * Refresh can be scheduled via **cron jobs or pgAgent**.

* **Indexes**

  * Materialized views can have **indexes**, including unique indexes.
  * Indexed materialized views improve query performance and enable **incremental lookups**.

* **Access and Usage**

  * Queried like a regular table using `SELECT`.
  * Supports filtering, joining, and aggregating on stored data.
  * Not automatically updated when underlying tables change.

* **Advantages**

  * Speeds up complex queries and reporting workloads.
  * Reduces server load by avoiding repeated expensive computations.
  * Can be indexed for further performance gains.

* **Limitations**

  * Requires manual or scheduled refresh to remain current.
  * Storage overhead since data is physically stored.
  * Cannot be used for real-time transactional operations requiring immediate consistency.

### Summary

Materialized views in PostgreSQL provide a **performance-optimized alternative to regular views**:

* Persist query results on disk
* Support indexing for fast retrieval
* Require refresh to synchronize with underlying data
* Ideal for analytics, reporting, and expensive query caching

---
