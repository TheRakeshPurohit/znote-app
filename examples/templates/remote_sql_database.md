# 🔗 Query a Remote DB
- 🚀 **Easily query a remote SQL database over SSH**
- 👉 **Make sure you have installed the** 🧩 **Remote SQL plugin**

## 🔑 Step 1: Generate an SSH Key
Run the following command to generate an SSH key:
```bash 
ssh-keygen -t rsa -N '' -f my-ssh-key
```
This will create two files:

- `my-ssh-key` (private key)
- `my-ssh-key.pub` (public key)


## 📤 Step 2: Copy Your SSH Key to the Server
Run the following command in a terminal and enter your server password when prompted:
```bash 
ssh-copy-id -i my-ssh-key user@XXX.ovh.net
```
This allows passwordless authentication when connecting to your remote database.


## 🛠️ Step 3: Query the Remote SQL Database
Use the following script to execute an SQL query over SSH:
```js 
//exec:node
const query = "SELECT * FROM TABLE;";

const sshKey = "my-ssh-key"; // Path to your SSH private key
const remoteHost = "user@XXX.ovh.net"; // SSH user and host
const localPort = 3307; // Local port where the remote database is accessible
const dbDialect = "mysql"; // Options: 'mysql' | 'postgres' | 'mssql'
const dbPort = 3306; // Default ports: MySQL/MariaDB=3306, PostgreSQL=5432, MSSQL=1433

const results = await getRemoteSQL(query, sshKey, localPort, dbPort, remoteHost, dbDialect, "user", "password", "database");

printJSON(results);
```
✅ **You're now ready to securely query your remote database over SSH!**
📖 More details available in the **Remote SQL plugin documentation**.
