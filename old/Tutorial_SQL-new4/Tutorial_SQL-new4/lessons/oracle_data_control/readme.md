## Data Control in Oracle SQL

### 1. **GRANT**
The `GRANT` statement is used to give specific privileges to users or roles on database objects like tables, views, or procedures.

#### 1.1 **Grant Privileges**
It grants permissions to users or roles to perform specific actions on database objects.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Grant SELECT**      | Grants permission to retrieve data from a table/view         | `GRANT SELECT ON employees TO user1;`                          |
| **Grant INSERT**      | Grants permission to insert data into a table                | `GRANT INSERT ON employees TO user2;`                          |
| **Grant UPDATE**      | Grants permission to update data in a table                  | `GRANT UPDATE ON employees TO user3;`                          |
| **Grant DELETE**      | Grants permission to delete data from a table                | `GRANT DELETE ON employees TO user4;`                          |
| **Grant EXECUTE**     | Grants permission to execute a stored procedure or function | `GRANT EXECUTE ON procedure_name TO user1;`                    |
| **Grant All Privileges** | Grants all available privileges on a table or object       | `GRANT ALL PRIVILEGES ON employees TO user1;`                  |

#### Usage Example:
```sql
-- Grant SELECT and INSERT privileges on the 'employees' table to 'user1'
GRANT SELECT, INSERT ON employees TO user1;
```

### 2. **REVOKE**
The `REVOKE` statement is used to remove privileges from users or roles that were previously granted.

#### 2.1 **Revoke Privileges**
It removes specific permissions from users or roles, preventing them from accessing or modifying data.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Revoke SELECT**     | Revokes permission to retrieve data from a table/view        | `REVOKE SELECT ON employees FROM user1;`                        |
| **Revoke INSERT**     | Revokes permission to insert data into a table               | `REVOKE INSERT ON employees FROM user2;`                        |
| **Revoke UPDATE**     | Revokes permission to update data in a table                 | `REVOKE UPDATE ON employees FROM user3;`                        |
| **Revoke DELETE**     | Revokes permission to delete data from a table               | `REVOKE DELETE ON employees FROM user4;`                        |
| **Revoke EXECUTE**    | Revokes permission to execute a stored procedure or function | `REVOKE EXECUTE ON procedure_name FROM user1;`                  |

#### Usage Example:
```sql
-- Revoke SELECT privilege on the 'employees' table from 'user1'
REVOKE SELECT ON employees FROM user1;
```

### 3. **CREATE USER**
The `CREATE USER` statement is used to create a new user account in the database.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Create Basic User** | Creates a new user with basic authentication                  | `CREATE USER new_user IDENTIFIED BY password;`                |
| **Assign Tablespace** | Creates a user and assigns default tablespace for data storage | `CREATE USER new_user IDENTIFIED BY password DEFAULT TABLESPACE users;` |

#### Usage Example:
```sql
-- Create a new user with a password
CREATE USER new_user IDENTIFIED BY password;

-- Create a new user with a default tablespace
CREATE USER new_user IDENTIFIED BY password DEFAULT TABLESPACE users;
```

### 4. **ALTER USER**
The `ALTER USER` statement is used to modify an existing user account’s properties.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Change Password**   | Modifies the password for an existing user                   | `ALTER USER new_user IDENTIFIED BY new_password;`             |
| **Assign Quota**      | Modifies the space quota for a user in a tablespace          | `ALTER USER new_user QUOTA 100M ON users;`                    |
| **Unlock User**       | Unlocks a previously locked user account                     | `ALTER USER new_user ACCOUNT UNLOCK;`                          |

#### Usage Example:
```sql
-- Change password for the user 'new_user'
ALTER USER new_user IDENTIFIED BY new_password;

-- Unlock the user account 'new_user'
ALTER USER new_user ACCOUNT UNLOCK;
```

### 5. **DROP USER**
The `DROP USER` statement is used to remove a user account from the database.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Drop User**         | Deletes a user and its associated schema and objects         | `DROP USER new_user;`                                          |
| **Cascade Option**    | Drops a user along with all associated objects               | `DROP USER new_user CASCADE;`                                  |

#### Usage Example:
```sql
-- Drop a user account 'new_user' and all their objects
DROP USER new_user CASCADE;
```

### 6. **Roles and Privileges**
Roles in Oracle are a way to group multiple privileges together, and they can be granted or revoked as a unit.

#### 6.1 **CREATE ROLE**
The `CREATE ROLE` statement is used to create a role in the database.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Create Role**       | Creates a new role in the database                            | `CREATE ROLE manager_role;`                                    |
| **Assign Privileges to Role** | Grants privileges to a role                             | `GRANT SELECT, INSERT ON employees TO manager_role;`           |

#### Usage Example:
```sql
-- Create a new role 'manager_role'
CREATE ROLE manager_role;

-- Grant privileges to the 'manager_role' role
GRANT SELECT, INSERT ON employees TO manager_role;
```

#### 6.2 **Grant Role to User**
The `GRANT` statement can also be used to assign a role to a user.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Grant Role**        | Grants a role to a user                                      | `GRANT manager_role TO user1;`                                 |

#### Usage Example:
```sql
-- Grant the 'manager_role' role to 'user1'
GRANT manager_role TO user1;
```

#### 6.3 **Revoke Role from User**
The `REVOKE` statement is used to remove a role from a user.

| **Property**         | **Description**                                              | **Usage Example**                                              |
|----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Revoke Role**       | Removes a role from a user                                    | `REVOKE manager_role FROM user1;`                              |

#### Usage Example:
```sql
-- Revoke the 'manager_role' role from 'user1'
REVOKE manager_role FROM user1;
```

### Summary of Data Control Operations:

| **Operation**         | **Description**                                               | **Syntax Example**                                              |
|-----------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **GRANT**             | Grants privileges to users/roles                              | `GRANT SELECT ON employees TO user1;`                          |
| **REVOKE**            | Removes privileges from users/roles                           | `REVOKE SELECT ON employees FROM user1;`                       |
| **CREATE USER**       | Creates a new user                                            | `CREATE USER new_user IDENTIFIED BY password;`                 |
| **ALTER USER**        | Modifies properties of an existing user                        | `ALTER USER new_user IDENTIFIED BY new_password;`              |
| **DROP USER**         | Removes a user from the database                              | `DROP USER new_user CASCADE;`                                  |
| **CREATE ROLE**       | Creates a new role                                            | `CREATE ROLE manager_role;`                                    |
| **GRANT ROLE**        | Grants a role to a user                                       | `GRANT manager_role TO user1;`                                 |
| **REVOKE ROLE**       | Revokes a role from a user                                    | `REVOKE manager_role FROM user1;`                              |

---
