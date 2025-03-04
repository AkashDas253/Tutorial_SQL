## **PostgreSQL DCL (Data Control Language) Cheatsheet**  

### **1. User Management**  
| Action | Command |
|--------|---------|
| Create User | `CREATE USER username WITH PASSWORD 'password';` |
| Alter User Password | `ALTER USER username WITH PASSWORD 'new_password';` |
| Drop User | `DROP USER username;` |
| Create Superuser | `CREATE USER username WITH SUPERUSER PASSWORD 'password';` |
| Alter User Role | `ALTER USER username WITH CREATEDB CREATEROLE;` |
| Rename User | `ALTER USER old_username RENAME TO new_username;` |
| Disable User Login | `ALTER USER username NOLOGIN;` |
| Enable User Login | `ALTER USER username LOGIN;` |
| Lock User Account | `ALTER USER username WITH NOLOGIN;` |
| Unlock User Account | `ALTER USER username WITH LOGIN;` |

### **2. Role Management**  
| Action | Command |
|--------|---------|
| Create Role | `CREATE ROLE role_name;` |
| Grant Role to User | `GRANT role_name TO username;` |
| Revoke Role from User | `REVOKE role_name FROM username;` |
| Drop Role | `DROP ROLE role_name;` |
| Create Role with Attributes | `CREATE ROLE role_name WITH LOGIN CREATEDB;` |
| Set Default Privileges for Role | `ALTER DEFAULT PRIVILEGES IN SCHEMA schema_name GRANT SELECT ON TABLES TO role_name;` |
| Grant Role Admin Option | `GRANT role_name TO username WITH ADMIN OPTION;` |
| Revoke Role Admin Option | `REVOKE ADMIN OPTION FOR role_name FROM username;` |
| Alter Role Privileges | `ALTER ROLE role_name WITH CREATEDB CREATEROLE;` |
| Set Role Password | `ALTER ROLE role_name WITH PASSWORD 'new_password';` |

### **3. Granting Privileges**  
| Privilege | Command Example |
|-----------|----------------|
| Grant Privileges | `GRANT SELECT, INSERT ON table_name TO username;` |
| Grant All Privileges | `GRANT ALL PRIVILEGES ON table_name TO username;` |
| Grant Schema Usage | `GRANT USAGE ON SCHEMA schema_name TO username;` |
| Grant Connect to Database | `GRANT CONNECT ON DATABASE db_name TO username;` |
| Grant Privileges on All Tables | `GRANT SELECT, INSERT ON ALL TABLES IN SCHEMA schema_name TO username;` |
| Grant Execute on Functions | `GRANT EXECUTE ON FUNCTION function_name TO username;` |
| Grant Temporary Table Creation | `GRANT TEMPORARY ON DATABASE db_name TO username;` |
| Grant Sequence Privileges | `GRANT USAGE, SELECT ON SEQUENCE sequence_name TO username;` |
| Grant Update on Columns | `GRANT UPDATE (column1, column2) ON table_name TO username;` |
| Grant Role Membership | `GRANT role_name TO username;` |

### **4. Revoking Privileges**  
| Privilege | Command Example |
|-----------|----------------|
| Revoke Specific Privileges | `REVOKE SELECT, INSERT ON table_name FROM username;` |
| Revoke All Privileges | `REVOKE ALL PRIVILEGES ON table_name FROM username;` |
| Revoke Schema Usage | `REVOKE USAGE ON SCHEMA schema_name FROM username;` |
| Revoke Connect to Database | `REVOKE CONNECT ON DATABASE db_name FROM username;` |
| Revoke Execute on Functions | `REVOKE EXECUTE ON FUNCTION function_name FROM username;` |
| Revoke Temporary Table Creation | `REVOKE TEMPORARY ON DATABASE db_name FROM username;` |
| Revoke Sequence Privileges | `REVOKE USAGE, SELECT ON SEQUENCE sequence_name FROM username;` |
| Revoke Role Membership | `REVOKE role_name FROM username;` |

