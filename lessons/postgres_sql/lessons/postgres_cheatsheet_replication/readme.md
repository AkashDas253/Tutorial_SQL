## **PostgreSQL High Availability & Replication: Comprehensive Cheatsheet**  

---

## **1. Replication Methods**  
| Replication Type | Description |
|------------------|-------------|
| **Streaming Replication** | Asynchronous or synchronous replication of WAL (Write-Ahead Log) data to standby servers. |
| **Logical Replication** | Table-level replication using `PUBLICATION` and `SUBSCRIPTION`. |
| **Slony-I** | Third-party trigger-based replication for complex replication needs. |
| **BDR (Bi-Directional Replication)** | Multi-master replication for distributed databases. |

---

## **2. Streaming Replication**  
| Mode | Description |
|------|-------------|
| **Asynchronous** | Faster but potential data loss during failure. |
| **Synchronous** | No data loss, but higher latency. |

### **Configuring Primary Server** (`postgresql.conf`)  
```ini
wal_level = replica
max_wal_senders = 10
synchronous_commit = on   # Set 'off' for async replication
```

### **Configuring Standby Server** (`recovery.conf` / `standby.signal`)  
```ini
standby_mode = 'on'
primary_conninfo = 'host=primary_host user=replication password=replica_pass'
```

---

## **3. Logical Replication**  
| Feature | Description |
|---------|-------------|
| **Per-table replication** | Allows replication of specific tables instead of the entire database. |
| **Supports writes on both sides** | Unlike streaming replication, allows updates on subscriber. |

### **Setting Up Logical Replication**  
#### **On Primary (Publisher)**
```sql
CREATE PUBLICATION my_pub FOR TABLE users, orders;
```
#### **On Standby (Subscriber)**
```sql
CREATE SUBSCRIPTION my_sub 
CONNECTION 'host=primary_host dbname=mydb user=replication password=replica_pass' 
PUBLICATION my_pub;
```

---

## **4. Failover & High Availability Tools**  
| Tool | Description |
|------|-------------|
| **Patroni** | Automates failover and HA using etcd or Consul. |
| **Repmgr** | Simplifies streaming replication management and failover. |
| **Pgpool-II** | Load balancing and connection pooling. |
| **PgBouncer** | Lightweight connection pooler to reduce load on the database. |

---

## **5. Load Balancing**  
| Method | Description |
|--------|-------------|
| **Pgpool-II** | Distributes read queries among replicas. |
| **HAProxy** | TCP load balancing for PostgreSQL connections. |

### **Pgpool-II Configuration Example**  
```ini
backend_hostname0 = 'primary_host'
backend_port0 = 5432
backend_weight0 = 1
backend_hostname1 = 'standby_host'
backend_port1 = 5432
backend_weight1 = 1
load_balance_mode = on
```

---

## **6. Backup & Disaster Recovery**  
| Backup Method | Description |
|--------------|-------------|
| **pg_dump** | Logical backup (per database or per table). |
| **pg_basebackup** | Physical backup for streaming replication. |
| **Continuous Archiving (WAL Archiving)** | Enables point-in-time recovery (PITR). |

### **Example: Creating a Physical Backup**  
```sh
pg_basebackup -D /var/lib/postgresql/backup -Fp -Xs -P -R
```
