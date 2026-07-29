# 🏠 Query a Local DB
- 🚀 **Easily query your local database**
- 👉 **Ensure you have installed the** 🧩 **Local SQL plugin**

## 📦 Supported Database Drivers
- ✅ MySQL / MariaDB
- ✅ PostgreSQL
- ✅ Microsoft SQL Server

## 🔌 Query a Local SQL Database
```js 
//exec:node

// ─────────────────────────────────────────────
// 🧭 Common exploration queries (by dialect)
// ─────────────────────────────────────────────
//
// MySQL / MariaDB
//   SHOW DATABASES;
//   SHOW TABLES;
//   DESCRIBE users;
//
// PostgreSQL
//   SELECT datname FROM pg_database WHERE datistemplate = false;
//   SELECT table_name, table_catalog FROM information_schema.tables WHERE table_schema = 'public';
//   SELECT column_name, data_type, is_nullable FROM information_schema.columns WHERE table_name = 'users';
//
// Microsoft SQL Server (MSSQL)
//   SELECT name FROM sys.databases;
//   SELECT table_name FROM information_schema.tables WHERE table_type = 'BASE TABLE';
//   SELECT column_name, data_type, is_nullable FROM information_schema.columns WHERE table_name = 'users';
//
// ─────────────────────────────────────────────
const query = "show tables;";

const dbDialect = "mysql"; // Options: 'mysql' | 'postgres' | 'mssql'
const dbPort = 3306; // Default ports: MySQL/MariaDB=3306, PostgreSQL=5432, MSSQL=1433

const results = await getSQL(query, "localhost", dbPort, dbDialect, "user", "password", "database");

printTable(results); // Display as a table
//printJSON(results); // Uncomment to see raw JSON output
```

## 🔹 Using SQLite Instead?
```js 
//exec:node

// ─────────────────────────────────────────────
// 🧭 SQLite exploration queries
// ─────────────────────────────────────────────
//
// List tables
//   SELECT name FROM sqlite_master WHERE type='table' AND name NOT LIKE 'sqlite_%';
//
// Describe a table
//   PRAGMA table_info(users);
//
// ─────────────────────────────────────────────
const query = "SELECT name FROM sqlite_master WHERE type='table' AND name NOT LIKE 'sqlite_%'";
const dbPath = "/path/to/database.sqlite";

const results = await getSQLite(query, dbPath);

printTable(results);
```
- ✅ **You're now ready to interact with your local database!**
- 📖 More details available in the **Local SQL plugin documentation**
