## PostgreSQL – Installation & Setup

### Overview

Installation and setup involve preparing the PostgreSQL database server for use on different operating systems, configuring its behavior, and ensuring secure and optimal operation. PostgreSQL can run on **Windows, Linux, macOS**, and other UNIX-like systems.

### Installation Methods

* **Package Managers**

  * Linux: `apt`, `yum`, `dnf`, `zypper`
  * macOS: `brew`
  * Windows: Installer packages (EnterpriseDB)
* **Source Compilation**

  * Download source code
  * Compile using `./configure`, `make`, `make install`
  * Offers flexibility and customization
* **Containerized Setup**

  * Docker images (official `postgres` image)
  * Kubernetes deployments for cloud-native environments
* **Cloud Services**

  * Managed PostgreSQL on AWS RDS, GCP Cloud SQL, Azure Database

### Configuration Files

* **postgresql.conf**

  * Controls server parameters: memory, connections, logging, performance tuning
* **pg\_hba.conf**

  * Defines authentication rules and client access policies
* **pg\_ident.conf**

  * Maps system usernames to database roles
* **Environment Variables**

  * `PGDATA`: Data directory
  * `PGPORT`: Port number
  * `PGUSER`: Default user

### Server Initialization

* **Data Directory Setup**

  * `initdb` creates the system catalog and initializes the database cluster
  * Specifies encoding, locale, and authentication method
* **Starting the Server**

  * `pg_ctl start` or system service management (`systemctl`, `service`)
* **Stopping the Server**

  * `pg_ctl stop` or equivalent system command
* **Restarting**

  * For configuration changes to take effect

### Connection and Access

* **Default Port**: 5432
* **Superuser Account**

  * Default `postgres` role created during initialization
* **Client Tools**

  * `psql` (command-line)
  * GUI tools: pgAdmin, DBeaver

### Post-Installation Tasks

* Set up **roles and permissions**
* Configure **network access** (listen addresses in `postgresql.conf` and `pg_hba.conf`)
* Adjust **performance parameters** (shared buffers, work memory)
* Enable **logging and monitoring** for server activity

---
