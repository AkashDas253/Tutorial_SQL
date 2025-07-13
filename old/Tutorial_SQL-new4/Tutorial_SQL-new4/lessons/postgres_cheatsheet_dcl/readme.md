## **PostgreSQL DCL (Data Control Language) Cheatsheet**  

#### **1. User Management**  
| Action | Command |
|--------|---------|
| Create User | `CREATE USER username WITH PASSWORD 'password';` |
| Alter User Password | `ALTER USER username WITH PASSWORD 'new_password';` |
| Drop User | `DROP USER username;` |

#### **2. Role Management**  
| Action | Command |
|--------|---------|
| Create Role | `CREATE ROLE role_name;` |
| Grant Role to User | `GRANT role_name TO username;` |
| Revoke Role from User | `REVOKE role_name FROM username;` |
| Drop Role | `DROP ROLE role_name;` |

#### **3. Granting Privileges**  
| Privilege | Command Example |
|-----------|----------------|
| Grant Privileges | `GRANT SELECT, INSERT ON table_name TO username;` |
| Grant All Privileges | `GRANT ALL PRIVILEGES ON table_name TO username;` |
| Grant Schema Usage | `GRANT USAGE ON SCHEMA schema_name TO username;` |

#### **4. Revoking Privileges**  
| Privilege | Command Example |
|-----------|----------------|
| Revoke Specific Privileges | `REVOKE SELECT, INSERT ON table_name FROM username;` |
| Revoke All Privileges | `REVOKE ALL PRIVILEGES ON table_name FROM username;` |
