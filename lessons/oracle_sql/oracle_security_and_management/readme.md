## Oracle Security and Management

### 1. **User Management**

User management in Oracle helps control access to the database, managing user accounts and their privileges.

#### 1.1 **Creating Users**
Creating a user involves defining a username and password and optionally assigning tablespaces and system privileges.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Defines a new user in the database                            | `CREATE USER username IDENTIFIED BY password;`                 |

#### Example:
```sql
CREATE USER john_doe IDENTIFIED BY password123;
```

| **Optional**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Default Tablespace**   | Defines the default tablespace for the user                   | `DEFAULT TABLESPACE tablespace_name;`                          |
| **Temporary Tablespace** | Specifies the temporary tablespace for the user               | `TEMPORARY TABLESPACE temp_tablespace_name;`                   |

#### Example with Optional Parameters:
```sql
CREATE USER john_doe IDENTIFIED BY password123
DEFAULT TABLESPACE users
TEMPORARY TABLESPACE temp;
```

#### 1.2 **Altering Users**
Altering a user allows modifying attributes such as password, tablespace, or granting system privileges.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Modify existing user attributes                                | `ALTER USER username IDENTIFIED BY new_password;`              |

#### Example:
```sql
ALTER USER john_doe IDENTIFIED BY new_password123;
```

| **Optional**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Default Tablespace**   | Change the user's default tablespace                          | `DEFAULT TABLESPACE new_tablespace;`                            |
| **Quota**                | Define or change the user's quota on tablespace               | `QUOTA 10M ON tablespace_name;`                                 |

#### Example with Optional Parameters:
```sql
ALTER USER john_doe DEFAULT TABLESPACE new_data QUOTA 50M ON users;
```

#### 1.3 **Dropping Users**
Dropping a user permanently removes the user from the database, including their schema objects unless specified otherwise.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Removes the user and their objects from the database          | `DROP USER username;`                                          |

| **Optional**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **CASCADE**             | Removes all objects owned by the user                         | `DROP USER username CASCADE;`                                  |

#### Example:
```sql
DROP USER john_doe CASCADE;
```

---

### 2. **Privileges and Roles**

Privileges grant access to perform certain actions, while roles are collections of privileges.

#### 2.1 **System Privileges**
System privileges allow users to perform administrative operations on the database.

| **Privilege**            | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **CREATE SESSION**       | Allows the user to log in to the database                     | `GRANT CREATE SESSION TO username;`                            |
| **CREATE TABLE**         | Allows creating tables in the database                        | `GRANT CREATE TABLE TO username;`                              |
| **ALTER DATABASE**       | Allows altering the database                                  | `GRANT ALTER DATABASE TO username;`                            |

#### Example:
```sql
GRANT CREATE SESSION, CREATE TABLE TO john_doe;
```

#### 2.2 **Object Privileges**
Object privileges are granted on specific database objects like tables, views, and procedures.

| **Privilege**            | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **SELECT**               | Allows querying data from a table or view                     | `GRANT SELECT ON table_name TO username;`                      |
| **INSERT**               | Allows inserting data into a table                            | `GRANT INSERT ON table_name TO username;`                      |
| **UPDATE**               | Allows updating data in a table                               | `GRANT UPDATE ON table_name TO username;`                      |
| **DELETE**               | Allows deleting data from a table                             | `GRANT DELETE ON table_name TO username;`                      |

#### Example:
```sql
GRANT SELECT, INSERT ON employees TO john_doe;
```

#### 2.3 **Roles**
Roles are collections of system and object privileges that can be granted to users.

| **Role**                 | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **DBA**                   | Provides full administrative access                           | `GRANT DBA TO username;`                                        |
| **CONNECT**               | Allows basic user connections                                 | `GRANT CONNECT TO username;`                                    |
| **RESOURCE**              | Allows the user to create objects like tables and views       | `GRANT RESOURCE TO username;`                                   |

#### Example:
```sql
GRANT DBA TO john_doe;
```

---

### 3. **Auditing**

Auditing helps track user activities and can be done at a standard or fine-grained level to monitor database access and changes.

#### 3.1 **Standard Auditing**
Standard auditing records database actions such as login attempts, DDL operations, and access to sensitive data.

| **Audit Action**         | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **SELECT**               | Audits SELECT statements on specified objects                | `AUDIT SELECT ON employees BY ACCESS;`                         |
| **INSERT**               | Audits INSERT operations on tables or views                   | `AUDIT INSERT ON employees BY ACCESS;`                         |
| **UPDATE**               | Audits UPDATE operations on tables or views                   | `AUDIT UPDATE ON employees BY ACCESS;`                         |

#### Example:
```sql
AUDIT SELECT, INSERT ON employees BY ACCESS;
```

#### 3.2 **Fine-Grained Auditing**
Fine-grained auditing (FGA) provides more granular control over which actions are audited by evaluating specific conditions.

| **Property**             | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**               | Audits actions based on specified conditions (e.g., specific column values) | `BEGIN DBMS_FGA.ADD_POLICY(...); END;`                          |

#### Example:
```sql
BEGIN
   DBMS_FGA.ADD_POLICY(
      object_schema   => 'HR',
      object_name     => 'employees',
      policy_name     => 'emp_audit_policy',
      audit_condition => 'salary > 10000',
      audit_column    => 'salary'
   );
END;
```

---
