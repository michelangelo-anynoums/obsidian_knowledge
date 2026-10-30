# 🐘 Node.js — `pg` (PostgreSQL)

> Connect Node.js to PostgreSQL and perform basic database operations.

## 1. 📦 Installation

```bash
npm install pg
```

`pg` is the official PostgreSQL client for Node.js.

## 2. 🗄️ Database setup

Create a database in PostgreSQL:

```js
CREATE DATABASE my_database;
```

Create a table:

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    age INTEGER
);
```

## 3. 🔌 Create a connection

Create a file called `db.js`:

```js
const { Pool } = require('pg');

const pool = new Pool({
    user: 'postgres',
    host: 'localhost',
    database: 'my_database',
    password: 'your_password',
    port: 5432,
});

module.exports = pool;
```

**Why** **Pool****?**

- Manages multiple database connections.
- Reuses connections automatically.
- Ideal for most Node.js applications.

## 4. ⚡ Basic query

Import the database connection:

```js
const pool = require('./db');

async function getUsers() {
    const result = await pool.query(
        'SELECT * FROM users'
    );

    console.log(result.rows);
}

getUsers();
```

- `pool.query()` executes SQL.
- `result.rows` contains the returned records.

## 5. 🛠️ CRUD Operations

### 🟢 CREATE — Insert data


```js
const result = await pool.query(
    `INSERT INTO users (name, email, age)
     VALUES ($1, $2, $3)
     RETURNING *`,
    ['John', 'john@email.com', 25]
);

console.log(result.rows[0]);
```

`$1`, `$2`, `$3` are parameter placeholders. They help prevent SQL injection.

### 🔵 READ — Get data

**Get all users:**

```js
const result = await pool.query(
    'SELECT * FROM users'
);

console.log(result.rows);
```

**Get one user by ID:**

```js
const result = await pool.query(
    'SELECT * FROM users WHERE id = $1',
    [1]
);

console.log(result.rows[0]);
```

### 🟡 UPDATE — Modify data

```js
const result = await pool.query(
    `UPDATE users
     SET name = $1, age = $2
     WHERE id = $3
     RETURNING *`,
    ['Mike', 30, 1]
);

console.log(result.rows[0]);
```

Updates the user with ID `1`.

### 🔴 DELETE — Remove data

```js
const result = await pool.query(
    'DELETE FROM users WHERE id = $1 RETURNING *',
    [1]
);

console.log(result.rows[0]);
```

Deletes the user with ID `1`.

## 6. 🧹 Close the connection pool

When your application shuts down:

```js
await pool.end();
```

This closes all connections managed by the pool.

## 7. 📁 Suggested project structure

```text
my-project/
│
├── db.js
├── index.js
├── package.json
└── .env
```

**💡 Important:** Store database credentials in environment variables instead of hardcoding them.

Install dotenv:

```bash
npm install dotenv
```

`.env`:

```env
DB_USER=postgres
DB_HOST=localhost
DB_NAME=my_database
DB_PASSWORD=your_password
DB_PORT=5432
```

Update `db.js`:

```js
require('dotenv').config();

const { Pool } = require('pg');

const pool = new Pool({
    user: process.env.DB_USER,
    host: process.env.DB_HOST,
    database: process.env.DB_NAME,
    password: process.env.DB_PASSWORD,
    port: process.env.DB_PORT,
});

module.exports = pool;
```

---

## 🧠 Quick Reference

|Operation|SQL|Purpose|
|---|---|---|
|CREATE|`INSERT`|Add records|
|READ|`SELECT`|Retrieve records|
|UPDATE|`UPDATE`|Modify records|
|DELETE|`DELETE`|Remove records|

**Remember:**

- `Pool` → Manages database connections.
- `pool.query()` → Executes SQL queries.
- `result.rows` → Returns query results.
- `$1, $2...` → Parameterized queries.
- `RETURNING *` → Returns affected records.

🔗 **Official resource:** https://node-postgres.com/

---
