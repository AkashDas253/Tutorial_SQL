## PostgreSQL – Process Architecture

### Overview

PostgreSQL uses a **process-based architecture**, meaning each client connection is handled by a separate server process rather than threads. This architecture enhances stability, isolation, and reliability.

### Key Processes

* **Postmaster Process**

  * Main server process
  * Manages incoming client connections
  * Starts new backend processes for each client
  * Handles configuration reloads and background process management
* **Backend Processes**

  * Created for each client connection
  * Handles SQL execution, transaction management, and query processing
  * Independent from other backend processes, ensuring isolation
* **Background Processes**

  * **WAL Writer**

    * Writes transaction logs (Write-Ahead Logging) to disk
    * Ensures durability and crash recovery
  * **Checkpointer**

    * Periodically writes dirty pages from memory to disk
    * Reduces recovery time after a crash
  * **Autovacuum Daemon**

    * Cleans up dead tuples and maintains table health
    * Prevents table bloat
  * **Stats Collector**

    * Gathers runtime statistics for queries and tables
    * Used by the query planner for optimization
  * **Archiver**

    * Archives WAL files if WAL archiving is enabled
  * **Background Worker Processes**

    * Custom or extension-specific tasks (e.g., logical replication, monitoring tools)

### Connection Handling

* Each client connection spawns a dedicated **backend process**.
* Process isolation provides robustness: one crashing backend does not affect others.
* Resource consumption is managed at the OS level per process.

### Inter-Process Communication (IPC)

* Processes communicate via:

  * Shared memory (e.g., buffers, locks)
  * Semaphores
  * Sockets (for client connections)
* IPC ensures consistency, coordination, and MVCC enforcement across backends.

### Advantages of Process Architecture

* **Stability**: Process crashes are isolated.
* **Security**: Each connection runs in its own memory space.
* **Predictability**: Simplifies management of memory and locks.

### Considerations

* **Memory usage**: Each process has its own stack and buffers.
* **Connection scalability**: High number of connections may require connection pooling (e.g., pgBouncer).

---
