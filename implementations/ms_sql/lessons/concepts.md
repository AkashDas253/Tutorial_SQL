
## Microsoft SQL Server — Concepts and Subconcepts

### Overview and Fundamentals

* SQL Server introduction

  * Definition and purpose
  * History and versions
  * Client-server model
  * ANSI SQL compliance
* SQL Server editions

  * Express
  * Standard
  * Enterprise
  * Developer
  * Web
* SQL Server services

  * Database Engine
  * SQL Server Agent
  * SQL Browser
  * Integration Services (SSIS)
  * Analysis Services (SSAS)
  * Reporting Services (SSRS)

---

### SQL Server Architecture

* Database Engine

  * Relational Engine (Query Processor)
  * Storage Engine
* SQL OS (Operating System Layer)

  * Memory Manager
  * Scheduler
  * I/O Manager
  * Resource Monitor
  * Deadlock Detector
* Protocol Layer

  * TDS (Tabular Data Stream) protocol
* File structure

  * Primary Data File (.mdf)
  * Secondary Data File (.ndf)
  * Log File (.ldf)
  * TempDB structure
* Buffer Management

  * Buffer Pool
  * Lazy Writer
  * Checkpoint process
* Transaction Management

  * Write-Ahead Logging
  * Log records and checkpoints
  * Recovery models
* Concurrency Control

  * Lock Manager
  * Isolation levels
  * Row versioning
  * Deadlock handling

---

### Databases and Storage

* System Databases

  * master
  * model
  * msdb
  * tempdb
  * resource
* User Databases

  * Filegroups
  * Data files and log files
* Data Storage

  * Pages and Extents
  * Heaps and B-trees
  * Row storage and compression
  * Columnstore indexes
* Database options

  * Collation
  * Compatibility level
  * Recovery model

---

### Transact-SQL (T-SQL)

* T-SQL language fundamentals

  * Syntax and statements
  * Batches and scripts
  * Variables and data types
* T-SQL categories

  * DDL (Data Definition Language)
  * DML (Data Manipulation Language)
  * DCL (Data Control Language)
  * TCL (Transaction Control Language)
* Procedural constructs

  * IF...ELSE, WHILE loops
  * TRY...CATCH blocks
  * GOTO, RETURN, WAITFOR
* Functions

  * Aggregate functions
  * String functions
  * Date and time functions
  * Mathematical functions
  * Conversion functions
  * System functions
* Programmable objects

  * Stored Procedures
  * User-Defined Functions (UDFs)
  * Triggers
  * Views
  * Cursors
* Temporary objects

  * Local temporary tables (#)
  * Global temporary tables (##)
  * Table variables

---

### Query Processing and Optimization

* Query lifecycle

  * Parsing
  * Algebrizer
  * Optimization
  * Execution
* Query Optimizer

  * Logical vs. physical plans
  * Cost-based optimization
  * Plan caching and reuse
* Execution Engine

  * Iterators
  * Operators (Scan, Join, Sort, Filter)
* Execution Plans

  * Estimated plan
  * Actual plan
  * Plan cache
* Performance tuning

  * Query hints
  * Statistics and histograms
  * Parameter sniffing

---

### Indexing and Performance

* Index fundamentals

  * Clustered index
  * Non-clustered index
  * Columnstore index
  * Filtered index
  * Full-text index
* Index storage

  * B-tree structure
  * Page splits and fragmentation
* Index management

  * Rebuild and reorganize
  * Fill factor and maintenance
* Performance monitoring tools

  * Execution Plan Viewer
  * SQL Profiler
  * Database Engine Tuning Advisor
  * Dynamic Management Views (DMVs)

---

### Transactions and Concurrency

* Transaction concepts

  * ACID properties
  * Transaction states
* Transaction control commands

  * BEGIN TRANSACTION
  * COMMIT
  * ROLLBACK
* Isolation levels

  * Read Uncommitted
  * Read Committed
  * Repeatable Read
  * Serializable
  * Snapshot
* Locking

  * Lock types (Shared, Exclusive, Update, Intent)
  * Lock granularity (Row, Page, Table)
* Deadlocks

  * Detection and prevention
  * Deadlock graphs

---

### Security and Authentication

* Security architecture

  * Authentication modes (Windows, SQL Server)
  * Authorization and permissions
* Logins and Users

  * Server logins
  * Database users
  * Roles and schemas
* Encryption

  * Transparent Data Encryption (TDE)
  * Always Encrypted
  * Column-level encryption
* Auditing

  * SQL Audit
  * Login auditing
* Security best practices

  * Least privilege principle
  * Securing connections and endpoints

---

### High Availability and Disaster Recovery (HADR)

* Backup and Restore

  * Full, differential, and log backups
  * Point-in-time recovery
  * Backup compression and encryption
* Log Shipping

  * Configuration and monitoring
* Database Mirroring

  * Synchronous and asynchronous modes
* Always On Availability Groups

  * Primary and secondary replicas
  * Read-only routing
* Replication

  * Snapshot, transactional, merge
* Clustering

  * Windows Server Failover Clustering (WSFC)

---

### Integration and Analytics Services

* SQL Server Integration Services (SSIS)

  * ETL workflows
  * Control flow and data flow
  * Package deployment and configuration
* SQL Server Reporting Services (SSRS)

  * Report design and deployment
  * Report Builder and subscriptions
* SQL Server Analysis Services (SSAS)

  * OLAP cubes
  * Tabular models
  * Data mining models
* Machine Learning Services

  * Integration with R and Python
  * External script execution

---

### Tools and Utilities

* SQL Server Management Studio (SSMS)
* Azure Data Studio
* sqlcmd utility
* bcp utility
* Profiler and Trace
* SQL Server Configuration Manager
* Database Mail and SQL Agent Jobs

---

### Monitoring and Maintenance

* Dynamic Management Views (DMVs)
* Performance counters
* Extended Events
* SQL Trace
* Maintenance Plans

  * Index optimization
  * Database integrity checks
  * Backup automation
* Resource Governor

  * Workload classification
  * Resource pools and caps

---

### Cloud and Hybrid Deployment

* Azure SQL Database

  * Managed instance
  * Elastic pools
* Hybrid integration

  * Azure Arc-enabled SQL
  * Backup to Azure
* Cloud security and monitoring

---

### Miscellaneous Advanced Concepts

* Service Broker

  * Message-based communication
  * Queues and dialogs
* Linked Servers and Distributed Queries
* PolyBase for external data sources
* Data compression and partitioning
* Temporal tables (system-versioned)
* JSON and XML support

  * FOR JSON, OPENJSON
  * FOR XML, OPENXML
* Graph database features

  * Nodes and edges
* In-Memory OLTP (Hekaton)

  * Memory-optimized tables
  * Natively compiled stored procedures

---
