## **PostgreSQL Installation & Setup Cheatsheet**

### **1. Download & Install**
| Platform | Command / Steps |
|----------|---------------|
| **Windows** | Download from [PostgreSQL official site](https://www.postgresql.org/download/), run the installer, select components, set password, finish installation. |
| **Linux (Debian/Ubuntu)** | `sudo apt update && sudo apt install postgresql postgresql-contrib` |
| **Linux (RHEL/CentOS)** | `sudo dnf install postgresql-server postgresql-contrib` |
| **macOS (Homebrew)** | `brew install postgresql` |

### **2. Start / Stop PostgreSQL**
| Action | Command |
|--------|---------|
| Start Service | `sudo systemctl start postgresql` |
| Stop Service | `sudo systemctl stop postgresql` |
| Restart Service | `sudo systemctl restart postgresql` |
| Check Status | `sudo systemctl status postgresql` |

### **3. Verify Installation**
| Action | Command |
|--------|---------|
| Check Version | `psql --version` |
| Check Running Status | `pg_isready` |

### **4. PostgreSQL User & Database Setup**
| Action | Command |
|--------|---------|
| Switch to PostgreSQL User | `sudo -i -u postgres` |
| Open PostgreSQL Shell | `psql` |
| Create New Database | `CREATE DATABASE dbname;` |
| Create New User | `CREATE USER username WITH PASSWORD 'password';` |
| Grant Privileges | `GRANT ALL PRIVILEGES ON DATABASE dbname TO username;` |
| List Databases | `\l` |
| List Users | `\du` |
| Delete Database | `DROP DATABASE dbname;` |
| Delete User | `DROP USER username;` |

### **5. Configure Remote Access**
| File | Changes |
|------|---------|
| `postgresql.conf` | Set `listen_addresses = '*'` |
| `pg_hba.conf` | Add `host all all 0.0.0.0/0 md5` |

### **6. Enable & Autostart PostgreSQL**
| Action | Command |
|--------|---------|
| Enable on Boot | `sudo systemctl enable postgresql` |
| Disable on Boot | `sudo systemctl disable postgresql` |

### **7. Backup & Restore**
| Action | Command |
|--------|---------|
| Backup Database | `pg_dump dbname > backup.sql` |
| Restore Database | `psql dbname < backup.sql` |
| Backup All Databases | `pg_dumpall > backup.sql` |
| Restore All Databases | `psql -f backup.sql` |

### **8. Essential PostgreSQL Commands**
| Action | Command |
|--------|---------|
| List Tables | `\dt` |
| Describe Table | `\d table_name` |
| Show Current User | `SELECT current_user;` |
| Show Connection Info | `SELECT inet_server_addr(), inet_server_port();` |
| Exit PostgreSQL Shell | `\q` |

### **9. Performance & Maintenance**
| Action | Command |
|--------|---------|
| Analyze Table | `ANALYZE table_name;` |
| Vacuum Database | `VACUUM;` |
| Reindex Table | `REINDEX TABLE table_name;` |
| Check Active Connections | `SELECT * FROM pg_stat_activity;` |

### **10. Troubleshooting**
| Issue | Solution |
|-------|---------|
| Cannot Connect to PostgreSQL | Ensure service is running with `sudo systemctl status postgresql` |
| Permission Denied | Ensure user has correct privileges using `GRANT` |
| Authentication Failure | Check `pg_hba.conf` and authentication settings |
| Port Already in Use | Change `port` in `postgresql.conf` and restart service |
