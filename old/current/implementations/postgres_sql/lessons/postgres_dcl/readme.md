## **Data Control Language (DCL) in PostgreSQL**  

DCL manages database permissions and access control. It includes commands like `GRANT` and `REVOKE` to assign or remove privileges from users and roles.

---

### **1. GRANT – Assign Privileges**  
The `GRANT` command provides specific permissions on database objects (tables, schemas, etc.) to users or roles.

#### **Syntax**  
```sql
GRANT privilege(s) ON object TO user/role;
```

#### **Example**  
```sql
GRANT SELECT, INSERT ON employees TO user1;
```
> Allows `user1` to read (`SELECT`) and add (`INSERT`) data to the `employees` table.

#### **Granting ALL Privileges**  
```sql
GRANT ALL PRIVILEGES ON employees TO user1;
```
> Gives `user1` full control over the `employees` table.

#### **Granting Privileges to PUBLIC (All Users)**  
```sql
GRANT SELECT ON employees TO PUBLIC;
```
> Grants `SELECT` to all users.

#### **Granting Privileges with GRANT OPTION**  
```sql
GRANT SELECT ON employees TO user1 WITH GRANT OPTION;
```
> Allows `user1` to grant `SELECT` privilege to others.

---

### **2. REVOKE – Remove Privileges**  
The `REVOKE` command removes previously granted permissions.

#### **Syntax**  
```sql
REVOKE privilege(s) ON object FROM user/role;
```

#### **Example**  
```sql
REVOKE SELECT, INSERT ON employees FROM user1;
```
> Removes `SELECT` and `INSERT` privileges from `user1` on `employees`.

#### **Revoking ALL Privileges**  
```sql
REVOKE ALL PRIVILEGES ON employees FROM user1;
```
> Removes all permissions from `user1`.

#### **Revoking PUBLIC Privileges**  
```sql
REVOKE SELECT ON employees FROM PUBLIC;
```
> Prevents all users from selecting data.

---

### **3. ROLE Management in PostgreSQL**  
Roles in PostgreSQL work as both **users and groups**.

#### **Create a Role**  
```sql
CREATE ROLE manager;
```

#### **Assign a Password to Role**  
```sql
ALTER ROLE manager WITH PASSWORD 'securepass';
```

#### **Grant Role Privileges**  
```sql
GRANT manager TO user1;
```
> Assigns `manager` role to `user1`.

#### **Remove a Role from a User**  
```sql
REVOKE manager FROM user1;
```

#### **Drop a Role**  
```sql
DROP ROLE manager;
```
> Deletes the `manager` role.

---

### **Notes**  
- **Only superusers and role owners can grant/revoke privileges.**  
- **Permissions apply at the database, schema, table, and column levels.**  
- **Privileges cascade when granted to a role assigned to users.**  

---
