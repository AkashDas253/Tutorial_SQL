## SQL 

---

### Concepts
- [SQL Concepts](lessons/concepts/sql.md)
- [SQL Internal Architectural Concept](lessons/concepts/sql_architecture.md)

---



---

### **SQL Architecture Overview**

#### **High-Level Layers**

* [Client Layer](lessons/architecture/client_layer.md)
  * [SQL query submission](lessons/architecture/client_layer/sql_query_submission.md)
  * [Applications, BI tools, CLI interfaces](lessons/architecture/client_layer/applications_bi_cli.md)
  * [Drivers & connectors (ODBC, JDBC)](lessons/architecture/client_layer/drivers_connectors.md)
* [SQL Engine Layer](lessons/architecture/sql_engine_layer.md)
  * [Core processing of queries](lessons/architecture/sql_engine_layer/core_processing.md)
  * [Components](lessons/architecture/sql_engine_layer/components.md)
    * [Parser](lessons/architecture/sql_engine_layer/parser.md)
    * [Query Optimizer](lessons/architecture/sql_engine_layer/query_optimizer.md)
    * [Query Executor](lessons/architecture/sql_engine_layer/query_executor.md)
    * [Transaction Manager](lessons/architecture/sql_engine_layer/transaction_manager.md)
* [Storage Layer](lessons/architecture/storage_layer.md)
  * [Physical storage of data](lessons/architecture/storage_layer/physical_storage.md)
  * [Indexes, tables, partitions](lessons/architecture/storage_layer/indexes_tables_partitions.md)
  * [Buffer management, caching, file management](lessons/architecture/storage_layer/buffer_caching_file.md)

#### **SQL Engine Internal Architecture**

* [Parser](lessons/architecture/parser.md)
  * [Syntax check & validation](lessons/architecture/parser/syntax_validation.md)
  * [Parse tree generation](lessons/architecture/parser/parse_tree.md)
  * [Query decomposition](lessons/architecture/parser/query_decomposition.md)
* [Query Optimizer](lessons/architecture/query_optimizer.md)
  * [Logical optimization](lessons/architecture/query_optimizer/logical_optimization.md)
    * [Expression simplification](lessons/architecture/query_optimizer/expression_simplification.md)
    * [Subquery unnesting](lessons/architecture/query_optimizer/subquery_unnesting.md)
    * [Predicate pushdown](lessons/architecture/query_optimizer/predicate_pushdown.md)
  * [Physical optimization](lessons/architecture/query_optimizer/physical_optimization.md)
    * [Join strategy selection](lessons/architecture/query_optimizer/join_strategy.md)
    * [Index usage & access path determination](lessons/architecture/query_optimizer/index_access_path.md)
  * [Cost estimation & plan selection](lessons/architecture/query_optimizer/cost_plan_selection.md)
* [Query Executor](lessons/architecture/query_executor.md)
  * [Executes the optimized plan](lessons/architecture/query_executor/optimized_plan.md)
  * [Accesses storage via storage engine](lessons/architecture/query_executor/storage_access.md)
  * [Implements operators: scan, join, aggregation, sort](lessons/architecture/query_executor/operators.md)
  * [Handles pipelining and materialization](lessons/architecture/query_executor/pipelining_materialization.md)
* [Transaction Manager](lessons/architecture/transaction_manager.md)
  * [Ensures ACID properties](lessons/architecture/transaction_manager/acid.md)
    * [Atomicity: Rollback on failure](lessons/architecture/transaction_manager/atomicity.md)
    * [Consistency: Constraints enforcement](lessons/architecture/transaction_manager/consistency.md)
    * [Isolation: Locking & MVCC](lessons/architecture/transaction_manager/isolation.md)
    * [Durability: Write-ahead logs](lessons/architecture/transaction_manager/durability.md)
  * [Concurrency control & deadlock management](lessons/architecture/transaction_manager/concurrency_deadlock.md)
* [Storage Engine](lessons/architecture/storage_engine.md)
  * [Physical storage & retrieval](lessons/architecture/storage_engine/physical_storage.md)
  * [Data structures: heap, clustered tables](lessons/architecture/storage_engine/data_structures.md)
  * [Indexes: B-Tree, Hash, GiST](lessons/architecture/storage_engine/indexes.md)
  * [Logging, checkpoints, recovery](lessons/architecture/storage_engine/logging_recovery.md)

#### **Execution Flow**

1. [Client submits SQL query](lessons/architecture/execution_flow/client_submit.md)
2. [Parser validates & generates parse tree](lessons/architecture/execution_flow/parser_validate.md)
3. [Query Optimizer selects execution plan](lessons/architecture/execution_flow/optimizer_plan.md)
4. [Executor executes plan](lessons/architecture/execution_flow/executor_execute.md)
5. [Storage engine reads/writes data](lessons/architecture/execution_flow/storage_engine_rw.md)
6. [Transaction manager handles ACID and concurrency](lessons/architecture/execution_flow/transaction_manager.md)
7. [Result returned to client](lessons/architecture/execution_flow/result_return.md)

#### **Key Components Interaction**

* [Optimizer uses statistics & metadata for plan decisions](lessons/architecture/key_interaction/optimizer_stats.md)
* [Executor interacts with buffer pool & storage engine](lessons/architecture/key_interaction/executor_buffer_storage.md)
* [Transaction manager coordinates logging, locks, MVCC](lessons/architecture/key_interaction/transaction_logging_locks_mvcc.md)
* [Storage engine provides persistent storage and caching](lessons/architecture/key_interaction/storage_persistence_caching.md)

#### **Additional Considerations**

* [Indexing & partitioning improve query performance](lessons/architecture/additional/indexing_partitioning.md)
* [Caching & memory management reduce I/O overhead](lessons/architecture/additional/caching_memory.md)
* [Replication & sharding for distributed databases](lessons/architecture/additional/replication_sharding.md)
* [Query plan caching & adaptive execution improve repeated query performance](lessons/architecture/additional/plan_caching_adaptive.md)

---

#### SQL Implementations

- [ANSI SQL(Standard)](implementations/ansi_sql/readme.md)
- [My SQL](implementations/my_sql/readme.md)
- [Oracle SQL](implementations/oracle_sql/readme.md)
- [PL/SQL](implementations/pl_sql/readme.md)
- [Postgres SQL](implementations/postgres_sql/readme.md)


---  

