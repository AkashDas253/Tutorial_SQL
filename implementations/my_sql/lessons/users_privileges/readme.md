## 🧾 Comprehensive Note on **Users and Privileges** in MySQL

---

## 🧑‍💼 User Management

### ✅ Create User

```sql
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```

* `'username'`: Name of the user.
* `'host'`: Host from which user can connect (e.g., `'localhost'`, `'%'`).
* `'password'`: Initial password.

---

### ✅ View Users

```sql
SELECT user, host FROM mysql.user;
```

---

### ✅ Rename User

```sql
RENAME USER 'old_name'@'host' TO 'new_name'@'host';
```

---

### ✅ Delete User

```sql
DROP USER 'username'@'host';
```

---

## 🔐 Privilege Management

### ✅ Grant Privileges

```sql
GRANT privilege_type ON database.table TO 'username'@'host';
```

| Privilege Type                         | Description                               |
| -------------------------------------- | ----------------------------------------- |
| `ALL PRIVILEGES`                       | Grants all permissions                    |
| `SELECT`, `INSERT`, `UPDATE`, `DELETE` | DML permissions                           |
| `CREATE`, `ALTER`, `DROP`              | DDL permissions                           |
| `GRANT OPTION`                         | Allows user to grant privileges to others |
| `RELOAD`, `SHUTDOWN`, `PROCESS`        | Administrative privileges                 |

🔸 Grant global privileges:

```sql
GRANT ALL PRIVILEGES ON *.* TO 'username'@'host';
```

🔸 Grant database-level privileges:

```sql
GRANT SELECT, INSERT ON dbname.* TO 'username'@'host';
```

🔸 Grant table-level privileges:

```sql
GRANT SELECT, UPDATE ON dbname.tablename TO 'username'@'host';
```

---

### ✅ Revoke Privileges

```sql
REVOKE privilege_type ON database.table FROM 'username'@'host';
```

---

### ✅ View Privileges

* For current user:

```sql
SHOW GRANTS;
```

* For specific user:

```sql
SHOW GRANTS FOR 'username'@'host';
```

---

### ✅ Apply Changes Immediately

```sql
FLUSH PRIVILEGES;
```

* Needed if manual changes are made to privilege tables.

---

## 🔄 Password Management

* ✅ Change own password:

```sql
SET PASSWORD = 'new_password';
```

* ✅ Change for another user:

```sql
SET PASSWORD FOR 'username'@'host' = 'new_password';
```

* ✅ Expire password:

```sql
ALTER USER 'username'@'host' PASSWORD EXPIRE;
```

---

## 🔐 Account Locking (MySQL 5.7+)

* ✅ Lock user account:

```sql
ALTER USER 'username'@'host' ACCOUNT LOCK;
```

* ✅ Unlock account:

```sql
ALTER USER 'username'@'host' ACCOUNT UNLOCK;
```

---

## 🛡️ Role Management (MySQL 8+)

* ✅ Create a role:

```sql
CREATE ROLE 'rolename';
```

* ✅ Grant privileges to role:

```sql
GRANT SELECT ON dbname.* TO 'rolename';
```

* ✅ Assign role to user:

```sql
GRANT 'rolename' TO 'username'@'host';
```

* ✅ Set default role:

```sql
SET DEFAULT ROLE 'rolename' TO 'username'@'host';
```

* ✅ Activate role for current session:

```sql
SET ROLE 'rolename';
```

---

### Authentication Plugins

MySQL uses authentication plugins to verify user identities and determine how passwords are handled during login.

#### Common Plugins

| Plugin Name             | Description                                                          |
| ----------------------- | -------------------------------------------------------------------- |
| `mysql_native_password` | Traditional plugin using SHA1 hashing. Deprecated in newer versions. |
| `caching_sha2_password` | Default in MySQL 8.0. Uses SHA-256 with caching for performance.     |
| `sha256_password`       | Uses SHA-256 without caching. More secure but may require SSL.       |
| `auth_socket`           | Allows Linux socket-based authentication (used for local OS users).  |
| `ldap_authentication`   | Integrates MySQL authentication with LDAP (available in Enterprise). |

#### Syntax

```sql
-- Specify plugin at user creation
CREATE USER 'user1'@'localhost'
IDENTIFIED WITH caching_sha2_password
BY 'securePassword';

-- Change plugin for existing user
ALTER USER 'user1'@'localhost'
IDENTIFIED WITH mysql_native_password
BY 'newPassword';
```

#### Notes

* `caching_sha2_password` is recommended unless backward compatibility is needed.
* `auth_socket` allows passwordless login from specific OS accounts.
* Enterprise editions provide plugins for LDAP, Kerberos, PAM, etc.

---

## 🧪 Usage Scenarios

* Restrict read-only access to a reporting user.
* Create an admin user with full control (`ALL PRIVILEGES`).
* Lock accounts after employees leave.
* Assign roles like `auditor`, `developer`, `ops` for scalable security.

---
