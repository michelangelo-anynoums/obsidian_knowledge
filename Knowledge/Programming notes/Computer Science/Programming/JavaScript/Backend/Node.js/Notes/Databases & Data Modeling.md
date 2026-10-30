# 🗄️ 07 — Databases & Data Modeling

> An API becomes useful when it can **store, retrieve, update, and delete data** reliably.

## 🐘 1. SQL & Relational Databases

Start with **PostgreSQL**.

> [!abstract] Data is organized into tables, rows, and columns.

![[Pasted image 20261030071731.png|618]]

### Basic structure

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE
);

CREATE TABLE tasks (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    user_id INTEGER REFERENCES users(id)
);
```

- **Table** → Collection of data.
- **Row** → One record.
- **Column** → One property.
- **Data type** → INTEGER, TEXT, BOOLEAN, DATE.
- **PRIMARY KEY** → Unique record identifier.
- **FOREIGN KEY** → Connects two tables.
- **NOT NULL** → Value is required.
- **UNIQUE** → No duplicate values.

### 🔗 Relationships

```sql
-- One user can have many tasks.

users.id → tasks.user_id
```

Common relationships:

- One-to-One (1:1)
- One-to-Many (1:N)
- Many-to-Many (N:N)

### ⚡ Essential SQL

```sql
-- READ
SELECT * FROM users;

-- CREATE
INSERT INTO users (name, email)
VALUES ('Alex', 'alex@mail.com');

-- UPDATE
UPDATE users
SET name = 'John'
WHERE id = 1;

-- DELETE
DELETE FROM users
WHERE id = 1;
```

### JOIN — combine related tables

```sql
SELECT users.name, tasks.title
FROM users
JOIN tasks
ON users.id = tasks.user_id;
```

### Aggregations

```sql
SELECT user_id, COUNT(*) AS total_tasks
FROM tasks
GROUP BY user_id;
```

Useful functions:

- `COUNT()` → Count records.
- `SUM()` → Add values.
- `AVG()` → Calculate average.
- `MIN()` / `MAX()` → Find extremes.

## 🧱 2. Database Design

### Normalization

Organize data to avoid unnecessary duplication.

❌ Bad design:

```text
tasks
--------------------------------
id | title | username | email
```

✅ Better design:

```text
users
id | username | email

tasks
id | title | user_id
```

Store user information once and reference it using `user_id`.

### Indexes

Indexes make searching faster.

```sql
CREATE INDEX idx_tasks_user
ON tasks(user_id);
```

Useful for frequently searched or joined columns.

> [!question] Indexes improve reads but add storage and write overhead.

### Query execution plans

```sql
EXPLAIN ANALYZE
SELECT * FROM tasks
WHERE user_id = 1;
```

Shows how PostgreSQL executes a query and where performance costs occur.

## 🔒 3. Transactions & ACID

A transaction groups multiple SQL operations into one logical operation.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE id = 2;

COMMIT;
```

If something fails:

```sql
ROLLBACK;
```

**ACID properties:**

- **Atomicity** → All operations succeed or none do.
- **Consistency** → Data remains valid.
- **Isolation** → Concurrent transactions don't interfere incorrectly.
- **Durability** → Committed changes persist.

Also understand:

- Isolation levels → Control transaction visibility.
- Locks → Protect data during concurrent updates.
- Deadlocks → Transactions wait on each other's locks.

## 🟢 4. Node.js + PostgreSQL

Install the PostgreSQL driver:

```bash
npm install pg
```

### Database connection

```js
// db.js
const { Pool } = require("pg");

const pool = new Pool({
  connectionString: process.env.DATABASE_URL
});

module.exports = pool;
```

`Pool` manages reusable database connections.

> [!important] Don't create a new connection for every request.

### Query from Node.js

```js
const db = require("./db");

const result = await db.query(
  "SELECT * FROM users WHERE id = $1",
  [1]
);

console.log(result.rows);
```

`$1` is a parameter placeholder.

✅ Always parameterize queries to prevent SQL injection.

❌ Never do this:

```js
const query =
  `SELECT * FROM users WHERE id = ${req.params.id}`;
```

### Separate database logic

```text
src/
├── routes/
│   └── task.routes.js
├── controllers/
│   └── task.controller.js
├── services/
│   └── task.service.js
├── repositories/
│   └── task.repository.js
└── db.js
```

Example repository:

```js
// task.repository.js
const db = require("../db");

async function getTasksByUser(userId) {
  const result = await db.query(
    "SELECT * FROM tasks WHERE user_id = $1",
    [userId]
  );

  return result.rows;
}

module.exports = { getTasksByUser };
```

**Separation of concerns:**

- Routes → Define endpoints.
- Controllers → Handle HTTP requests.
- Services → Business logic.
- Repositories → Database queries.
- Database → Manage connections.

### ⚠️ Handle database errors


```js
try {
  const result = await db.query(
    "INSERT INTO users (email) VALUES ($1) RETURNING *",
    [email]
  );

  return result.rows[0];

} catch (error) {
  if (error.code === "23505") {
    throw new Error("Email already exists");
  }

  throw error;
}
```

Common PostgreSQL errors:

- `23505` → Unique constraint violation.
- `23503` → Foreign key violation.
- `23502` → NOT NULL violation.

## 🔄 5. Migrations & Seed Data

### Migrations

Migrations track changes to your database schema.

```sql
-- 001_create_tasks.sql

CREATE TABLE tasks (
    id SERIAL PRIMARY KEY,
    title TEXT NOT NULL,
    completed BOOLEAN DEFAULT FALSE
);
```

Think of migrations as **version control for your database structure**.

Popular tools:

- Prisma Migrate
- Drizzle Kit
- Knex Migrations

### Seed data

Insert initial development data:

```sql
INSERT INTO tasks (title, completed)
VALUES
('Learn PostgreSQL', false),
('Build Node API', false);
```

Useful for development and testing.

## 🔷 6. ORM — Prisma & Drizzle

An ORM helps interact with databases using JavaScript/TypeScript instead of writing every SQL query manually.

### Prisma example


```bash
npm install prisma @prisma/client
npx prisma init
```

Define a model:

```js
model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  tasks Task[]
}

model Task {
  id     Int    @id @default(autoincrement())
  title  String
  userId Int
  user   User   @relation(fields: [userId], references: [id])
}
```

Query with Prisma:

```js
const users = await prisma.user.findMany({
  include: { tasks: true }
});
```

### Prisma vs Drizzle

|Prisma|Drizzle|
|---|---|
|Higher-level ORM|SQL-like ORM|
|Schema-first|TypeScript-first|
|Easy abstractions|More SQL control|

> [!abstract] Both are useful. Learn basic SQL first.

## 🍃 7. NoSQL — MongoDB

Relational databases use tables.

MongoDB uses **collections and documents**.

Example document:

```json
{
  "_id": "123",
  "name": "Alex",
  "tasks": [
    { "title": "Learn Node.js" },
    { "title": "Build an API" }
  ]
}
```

Important concepts:

- Collection → Group of documents.
- Document → JSON-like record (BSON internally).
- Index → Faster queries.
- Schema validation → Rules for document structure.

### SQL vs MongoDB

|SQL|MongoDB|
|---|---|
|Tables|Collections|
|Rows|Documents|
|Columns|Fields|
|Foreign keys|References / embedded data|
|Structured relationships|Flexible document modeling|

**When to choose:**

- PostgreSQL → Relationships, transactions, structured data.
- MongoDB → Document-oriented data and flexible structures.

> [!question] Don't choose NoSQL just because it's popular.

## ⚡ 8. Redis — Caching

Redis is an in-memory data store.

Useful for:

- Caching frequently requested data.
- Sessions.
- Rate-limit counters.
- Temporary data.
- Distributed coordination.

### Basic example

Install:

```bash
npm install redis
```

Use:

```js
const { createClient } = require("redis");

const redis = createClient();

await redis.connect();

// Store data for 60 seconds
await redis.set("username", "Alex", {
  EX: 60
});

// Retrieve data
const name = await redis.get("username");

console.log(name);
```

Redis reduces repeated database queries.

```text
Client
  ↓
Node.js API
  ↓
Redis Cache ── Cache HIT → Return data
  ↓ Cache MISS
PostgreSQL
  ↓
Store result in Redis
  ↓
Return data
```

---

## 🧠 9. Key Concepts to Remember

|Concept|Purpose|
|---|---|
|PostgreSQL|Relational database|
|SQL|Query language|
|Primary Key|Unique identifier|
|Foreign Key|Relationship|
|JOIN|Combine tables|
|Normalization|Reduce duplication|
|Index|Speed up queries|
|Transaction|Group operations|
|ACID|Transaction reliability|
|Migration|Version database schema|
|Connection Pool|Reuse connections|
|Prisma / Drizzle|Database abstraction|
|MongoDB|Document database|
|Redis|In-memory data store|

### 🎯 The Big Picture

```text
Node.js API
    │
    ├── Routes
    │
    ├── Controllers
    │
    ├── Services
    │
    ├── Repositories
    │       │
    │       ▼
    │    PostgreSQL
    │
    └── Redis (Cache)
```

**Remember:** SQL is the foundation. Learn relational modeling, relationships, queries, transactions, and indexes before moving to ORMs and NoSQL.

---

# 🐘 Node.js — PostgreSQL Libraries

> Learn SQL first, then use an ORM to make database operations easier.

## 🎯 Which library should you learn?

Recommended learning order:

1. **pg** → Direct SQL queries. Understand how Node.js communicates with PostgreSQL.
2. **Prisma** → High-level ORM. Work with database models using JavaScript.
3. **Drizzle** → Lightweight ORM. Write type-safe queries closer to SQL.

**My recommendation:** PostgreSQL + pg first, then Prisma.

---

# 🐘 1. pg — PostgreSQL Driver

`pg` (node-postgres) allows Node.js to execute SQL directly.

It's a driver, NOT an ORM.

### Installation

```bash
npm install pg dotenv
```

### Connection

`.env`

```env
DATABASE_URL=postgresql://postgres:password@localhost:5432/mydb
```

`db.js`

```js
require("dotenv").config();

const { Pool } = require("pg");

const pool = new Pool({
  connectionString: process.env.DATABASE_URL
});

module.exports = pool;
```

`Pool` manages reusable database connections.

### CRUD operations

`task.repository.js`

```js
const db = require("./db");

// CREATE
async function createTask(title) {
  const result = await db.query(
    "INSERT INTO tasks (title) VALUES ($1) RETURNING *",
    [title]
  );

  return result.rows[0];
}

// READ ALL
async function getTasks() {
  const result = await db.query(
    "SELECT * FROM tasks"
  );

  return result.rows;
}

// READ ONE
async function getTask(id) {
  const result = await db.query(
    "SELECT * FROM tasks WHERE id = $1",
    [id]
  );

  return result.rows[0];
}

// UPDATE
async function updateTask(id, title) {
  const result = await db.query(
    "UPDATE tasks SET title = $1 WHERE id = $2 RETURNING *",
    [title, id]
  );

  return result.rows[0];
}

// DELETE
async function deleteTask(id) {
  await db.query(
    "DELETE FROM tasks WHERE id = $1",
    [id]
  );
}

module.exports = {
  createTask,
  getTasks,
  getTask,
  updateTask,
  deleteTask
};
```

### Important concepts

- `db.query()` → Executes SQL.
- `$1`, `$2` → Parameter placeholders.
- `result.rows` → Query results.
- `RETURNING *` → Returns affected records.
- `Pool` → Reuses database connections.

⚠️ Always parameterize SQL queries to prevent SQL injection.

---

# 🔷 2. Prisma — ORM

Prisma lets you interact with databases using JavaScript/TypeScript instead of writing SQL for every operation.

### Installation

```bash
npm install prisma @prisma/client
npx prisma init
```

### Define your model

`prisma/schema.prisma`

```js
model Task {
  id        Int      @id @default(autoincrement())
  title     String
  completed Boolean  @default(false)
  createdAt DateTime @default(now())
}
```

Configure your PostgreSQL connection using `DATABASE_URL` in your environment configuration.

### Create database tables

```bash
npx prisma migrate dev --name init
```

### Connection

`db.js`

```js
const { PrismaClient } = require("@prisma/client");

const prisma = new PrismaClient();

module.exports = prisma;
```

Use one shared Prisma client rather than creating one for every request.

### CRUD operations

`task.repository.js`

```js
const prisma = require("./db");

// CREATE
async function createTask(title) {
  return prisma.task.create({
    data: { title }
  });
}

// READ ALL
async function getTasks() {
  return prisma.task.findMany();
}

// READ ONE
async function getTask(id) {
  return prisma.task.findUnique({
    where: { id }
  });
}

// UPDATE
async function updateTask(id, title) {
  return prisma.task.update({
    where: { id },
    data: { title }
  });
}

// DELETE
async function deleteTask(id) {
  return prisma.task.delete({
    where: { id }
  });
}
```

### Important methods

|Method|SQL equivalent|
|---|---|
|`create()`|INSERT|
|`findMany()`|SELECT|
|`findUnique()`|SELECT one|
|`update()`|UPDATE|
|`delete()`|DELETE|

Prisma translates your JavaScript operations into database queries.

---

# 🟠 3. Drizzle — TypeScript ORM

Drizzle is a lightweight ORM that keeps you closer to SQL.

### Installation

```bash
npm install drizzle-orm pg dotenv
npm install -D drizzle-kit
```

### Define your schema

`schema.js`

```js
const {
  pgTable,
  serial,
  text,
  boolean
} = require("drizzle-orm/pg-core");

const tasks = pgTable("tasks", {
  id: serial("id").primaryKey(),
  title: text("title").notNull(),
  completed: boolean("completed").default(false)
});

module.exports = { tasks };
```

### Connection

`db.js`

```js
require("dotenv").config();

const { drizzle } = require("drizzle-orm/node-postgres");
const { Pool } = require("pg");

const pool = new Pool({
  connectionString: process.env.DATABASE_URL
});

const db = drizzle({ client: pool });

module.exports = db;
```

### CRUD operations

`task.repository.js`

```js
const db = require("./db");
const { tasks } = require("./schema");
const { eq } = require("drizzle-orm");

// CREATE
async function createTask(title) {
  const result = await db
    .insert(tasks)
    .values({ title })
    .returning();

  return result[0];
}

// READ ALL
async function getTasks() {
  return db.select().from(tasks);
}

// READ ONE
async function getTask(id) {
  const result = await db
    .select()
    .from(tasks)
    .where(eq(tasks.id, id));

  return result[0];
}

// UPDATE
async function updateTask(id, title) {
  const result = await db
    .update(tasks)
    .set({ title })
    .where(eq(tasks.id, id))
    .returning();

  return result[0];
}

// DELETE
async function deleteTask(id) {
  return db
    .delete(tasks)
    .where(eq(tasks.id, id));
}
```

### Important methods

- `insert()` → INSERT
- `select()` → SELECT
- `update()` → UPDATE
- `delete()` → DELETE
- `eq()` → Equality condition.

Drizzle provides type-safe queries with a SQL-like syntax.

---

# ⚖️ 4. Quick Comparison

|Feature|pg|Prisma|Drizzle|
|---|---|---|---|
|Type|Driver|ORM|ORM|
|SQL queries|Direct SQL|Abstracted|SQL-like|
|TypeScript|Manual|Excellent|Excellent|
|Abstraction|Low|High|Low|
|SQL learning|Excellent|Indirect|Good|
|Complexity|Low|Low|Medium|

---

