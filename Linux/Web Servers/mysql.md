## 🧠 1. How MySQL Works on Linux

When you install MySQL or MariaDB, it runs as a **background service** (`mysqld`) that:

- Listens on a **UNIX socket** (usually `/var/lib/mysql/mysql.sock`) for **local CLI connections**
    
- Also listens on **TCP port 3306** for remote connections (if enabled)
    

You use the `mysql` command-line client to connect to this server process and run **SQL queries**.

### 🔧 MySQL Components on Linux:
|Component|Path / Tool|Purpose|
|---|---|---|
|`mysqld`|Background server process (`systemctl`)|The actual database server|
|`mysql`|Command-line client (`mysql -u root`)|Connects to `mysqld`|
|Socket file|`/var/lib/mysql/mysql.sock`|Local communication channel|
|Config file|`/etc/my.cnf` or `/etc/my.cnf.d/*.cnf`|Configures port, socket, etc.|
|Data storage|`/var/lib/mysql/`|Where databases and tables are stored|

