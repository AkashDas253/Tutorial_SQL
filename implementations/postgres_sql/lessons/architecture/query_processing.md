## PostgreSQL – Query Processing

### Overview

PostgreSQL processes queries using a **multi-stage pipeline**, involving parsing, planning, optimization, and execution. Its **query planner and optimizer** ensure efficient execution while leveraging indexes, caching, and available system statistics.

### Query Processing Stages

* **Parsing**

  * SQL statement is parsed into a **parse tree**.
  * Syntax and semantic checks are performed.
  * Errors are reported if the query is invalid.

* **Rewrite System**

  * Applies **rules and views** to transform the parse tree.
  * View expansion and rule rewrites occur here.

* **Planning & Optimization**

  * **Query Planner** generates multiple possible execution plans.
  * **Cost-based Optimizer** evaluates plans using:

    * Estimated I/O and CPU costs
    * Table and index statistics
    * Join order, join type, and available indexes
  * Selects the **least-cost plan** for execution.
  * Supports **parallel queries** for large data processing.

* **Execution Engine**

  * Executes the chosen plan using **executor nodes**.
  * Handles data retrieval, joins, aggregations, sorting, and filtering.
  * Performs **tuple visibility checks** according to MVCC rules.
  * Returns results to the client or intermediate processes.

### Index Usage

* The planner decides which **indexes** to use:

  * B-tree, Hash, GiST, GIN, BRIN
* Supports **index-only scans** when data can be retrieved from indexes without accessing the table.

### Caching in Query Execution

* Uses **shared buffers** and OS cache for table and index pages.
* Query results from repeated queries may benefit from **prepared statements and plan caching**.

### Statistics & Optimization

* **pg\_statistic** tables provide:

  * Column distribution
  * Null counts
  * Distinct values
* **ANALYZE** updates statistics to improve planner accuracy.
* **EXPLAIN / EXPLAIN ANALYZE** helps understand chosen execution plans.

### Parallel Execution

* Large queries may use multiple worker processes.
* Parallel scans, joins, and aggregates improve performance on multi-core systems.
* Controlled via parameters like `max_parallel_workers_per_gather`.

### Summary

PostgreSQL query processing is **robust, cost-aware, and extensible**, leveraging:

* Parsing and rewrite rules
* Cost-based planning and optimization
* Efficient execution with MVCC and caching
* Parallelism for high-performance queries

---
