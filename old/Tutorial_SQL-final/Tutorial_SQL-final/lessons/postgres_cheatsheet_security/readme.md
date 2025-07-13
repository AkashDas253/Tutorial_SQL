## **PostgreSQL Security: Comprehensive Cheatsheet**  

---

## **1. Authentication Methods**  
| Method | Description |
|--------|-------------|
| **md5 / scram-sha-256** | Password-based authentication (recommended for security). |
| **peer** | Uses OS-level user authentication (Linux only). |
| **trust** | No authentication required (not secure). |
| **cert** | SSL certificate-based authentication. |
| **ldap / radius / kerberos** | External authentication mechanisms. |

### **Configuring Authentication (`pg_hba.conf`)**  
```ini
# TYPE  DATABASE  USER  ADDRESS         METHOD
host    all       all   192.168.1.0/24  scram-sha-256
local   all       all                   peer
```

---

## **2. Role-Based Access Control (RBAC)**  
| Role Type | Description |
|-----------|-------------|
| **Superuser** | Full control over the database. |
| **User Role** | Standard database user with specific privileges. |
| **Group Role** | Collection of privileges assigned to multiple users. |

### **Creating & Assigning Roles**  
```sql
CREATE ROLE read_only_user LOGIN PASSWORD 'securepass';
GRANT CONNECT ON DATABASE mydb TO read_only_user;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO read_only_user;
```

---

## **3. Privileges & Access Control**  
| Privilege | Description |
|-----------|-------------|
| **SELECT** | Read access to tables/views. |
| **INSERT, UPDATE, DELETE** | Modify table data. |
| **CREATE, DROP** | Manage schemas, tables, etc. |
| **GRANT, REVOKE** | Assign or remove privileges. |

### **Granting & Revoking Privileges**  
```sql
GRANT SELECT, INSERT ON users TO app_user;
REVOKE DELETE ON users FROM app_user;
```

---

## **4. Secure Connections (SSL/TLS)**  
| Setting | Description |
|---------|-------------|
| `ssl = on` | Enables SSL connections. |
| `ssl_cert_file` | Path to the SSL certificate. |
| `ssl_key_file` | Path to the private key. |

### **Forcing SSL Connection**  
```ini
hostssl all all 0.0.0.0/0 scram-sha-256
```

---

## **5. Row-Level Security (RLS)**  
| Feature | Description |
|---------|-------------|
| **Policy-Based Access** | Restricts data at the row level. |
| **Enforce Per User** | Different users see different data. |

### **Enabling RLS on a Table**  
```sql
ALTER TABLE employees ENABLE ROW LEVEL SECURITY;

CREATE POLICY emp_view_policy 
ON employees 
USING (user_id = current_user);
```

---

## **6. Auditing & Logging**  
| Feature | Description |
|---------|-------------|
| **`log_connections`** | Logs all incoming connections. |
| **`log_statement`** | Logs executed queries. |
| **`pgAudit`** | Advanced auditing extension. |

### **Enabling Query Logging**  
```ini
log_statement = 'all'
log_connections = on
```
