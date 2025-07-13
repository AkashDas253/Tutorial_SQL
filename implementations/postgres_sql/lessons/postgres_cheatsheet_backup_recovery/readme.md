## **PostgreSQL Backup & Recovery - Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **Backup** | Creates a copy of database data to restore in case of failure. |
| **Recovery** | Restores database data from a backup. |
| **Physical Backup** | Copies actual data files. |
| **Logical Backup** | Exports SQL statements to recreate the database. |
| **Point-in-Time Recovery (PITR)** | Restores to a specific moment in time. |

---

## **2. Backup Methods**  

| Backup Type | Command | Description |
|------------|---------|-------------|
| **Logical Backup** | `pg_dump` | Exports schema and data as SQL statements. |
| **Cluster Backup** | `pg_dumpall` | Dumps all databases in a PostgreSQL instance. |
| **Physical Backup** | `pg_basebackup` | Copies the entire data directory. |
| **Tablespace Backup** | File System Copy | Copies a specific tablespace directory. |
| **WAL Archiving** | WAL Logs | Logs transactions for continuous recovery. |

---

## **3. Logical Backup Commands**  

### **Single Database Backup**  
```sh
pg_dump -U username -d database_name -F c -f backup_file.dump
```
- `-F c` → Custom format  
- `-f backup_file.dump` → Output file  

### **Single Table Backup**  
```sh
pg_dump -U username -d database_name -t table_name -F c -f table_backup.dump
```

### **All Databases Backup**  
```sh
pg_dumpall -U username -f all_databases_backup.sql
```
- Dumps all databases as SQL.

---

## **4. Logical Restore Commands**  

### **Restore a Single Database**  
```sh
pg_restore -U username -d new_database_name backup_file.dump
```
- Restores a database from `pg_dump`.  

### **Restore All Databases**  
```sh
psql -U username -f all_databases_backup.sql
```
- Restores a cluster from `pg_dumpall`.  

---

## **5. Physical Backup Commands**  

### **Full Physical Backup**  
```sh
pg_basebackup -U postgres -D /backup_directory -Fp -X fetch -P
```
- `-D` → Destination directory  
- `-Fp` → Plain format  
- `-X fetch` → Includes WAL logs  

### **Restoring a Physical Backup**  
1. Stop PostgreSQL  
   ```sh
   systemctl stop postgresql
   ```
2. Replace the existing data directory  
   ```sh
   rm -rf /var/lib/postgresql/data
   cp -r /backup_directory /var/lib/postgresql/data
   ```
3. Restart PostgreSQL  
   ```sh
   systemctl start postgresql
   ```

---

## **6. Point-in-Time Recovery (PITR)**  

### **Enable WAL Archiving**  
Add to `postgresql.conf`:  
```conf
archive_mode = on
archive_command = 'cp %p /var/lib/postgresql/archive/%f'
```

### **Restore to a Specific Point in Time**  
1. Stop PostgreSQL  
   ```sh
   systemctl stop postgresql
   ```
2. Restore base backup  
   ```sh
   cp -r /backup_directory /var/lib/postgresql/data
   ```
3. Create a `recovery.conf` file:  
   ```conf
   restore_command = 'cp /var/lib/postgresql/archive/%f %p'
   recovery_target_time = '2025-02-20 12:00:00'
   ```
4. Restart PostgreSQL  
   ```sh
   systemctl start postgresql
   ```

---

## **7. Common Backup & Restore Issues**  
| Issue | Solution |
|-------|---------|
| **Backup File Too Large** | Use `-j` for parallel dumps: `pg_dump -j 4` |
| **Permission Denied** | Ensure correct PostgreSQL user permissions. |
| **Restoring a Large Database** | Use `pg_restore -j 4` for parallel restore. |
| **Missing WAL Files in PITR** | Ensure `archive_command` is correctly configured. |
