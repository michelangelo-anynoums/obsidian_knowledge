# 🗄️ 8 — Database Integration

> 💡 **Goal:** Connect an Express application to a database to store, retrieve, update, and delete data.

## 🍃 1. MongoDB + Mongoose

- **MongoDB:** NoSQL document database.
- **Mongoose:** ODM (Object Document Mapper) for MongoDB.
- Data is stored in collections as documents.

**Connect to MongoDB**


```js
const mongoose = require("mongoose");

mongoose.connect(process.env.MONGO_URI)
  .then(() => console.log("MongoDB connected"))
  .catch(err => console.error(err));
```

**Create a Schema & Model**

```js
const userSchema = new mongoose.Schema({
  name: String,
  email: {
    type: String,
    required: true,
    unique: true
  },
  age: Number
});

const User = mongoose.model("User", userSchema);
```

## 🐘 2. PostgreSQL + Prisma

- **PostgreSQL:** Relational SQL database.
- **Prisma:** ORM (Object Relational Mapper).
- Data is organized into tables and relationships.

**Define a model —** **`schema.prisma`**


```prisma
model User {
  id    Int    @id @default(autoincrement())
  name  String
  email String @unique
  age   Int?
}
```

**Connect Prisma**


```js
const { PrismaClient } = require("@prisma/client");

const prisma = new PrismaClient();
```

**Create a user**

```js
const user = await prisma.user.create({
  data: {
    name: "John",
    email: "john@example.com",
    age: 25
  }
});
```

## 🐬 3. MySQL

- **MySQL:** Relational SQL database.
- Stores data in tables, rows, and columns.
- Commonly used with Node.js through the `mysql2` package.

**Connect to MySQL**
```js
const mysql = require("mysql2/promise");

const db = await mysql.createConnection({
  host: "localhost",
  user: "root",
  password: process.env.DB_PASSWORD,
  database: "myapp"
});
```

**Query data**

```js
const [rows] = await db.execute(
  "SELECT * FROM users WHERE id = ?",
  [1]
);

console.log(rows);
```

💡 Always use parameterized queries to prevent SQL injection.

---

## 🔄 4. CRUD Operations

CRUD represents the four basic database operations.

|Operation|HTTP|Purpose|
|---|---|---|
|Create|POST|Add data|
|Read|GET|Retrieve data|
|Update|PUT / PATCH|Modify data|
|Delete|DELETE|Remove data|

### Example — Express + Mongoose

Assuming the `User` model was defined earlier:

**1. CREATE — Add a user**


```js
app.post("/users", async (req, res) => {
  try {
    const user = await User.create(req.body);

    res.status(201).json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});
```

**2. READ — Get all users**



```js
app.get("/users", async (req, res) => {
  const users = await User.find();

  res.json(users);
});
```

**Get one user**



```js
app.get("/users/:id", async (req, res) => {
  const user = await User.findById(req.params.id);

  if (!user) {
    return res.status(404).json({ error: "User not found" });
  }

  res.json(user);
});
```

**3. UPDATE — Modify a user**



```js
app.patch("/users/:id", async (req, res) => {
  const user = await User.findByIdAndUpdate(
    req.params.id,
    req.body,
    { new: true, runValidators: true }
  );

  if (!user) {
    return res.status(404).json({ error: "User not found" });
  }

  res.json(user);
});
```

**4. DELETE — Remove a user**


```js
app.delete("/users/:id", async (req, res) => {
  const user = await User.findByIdAndDelete(req.params.id);

  if (!user) {
    return res.status(404).json({ error: "User not found" });
  }

  res.json({ message: "User deleted" });
});
```

---

## 🔗 5. Database + Express Architecture

Understand how the pieces communicate.


```
Client (Browser / Postman)
          |
          v
     Express API
          |
          v
     Route Handler
          |
          v
    Controller / Logic
          |
          v
     ORM / ODM
          |
          v
       Database
```

## 🛡️ 6. Important Concepts

- **Schema:** Defines the structure of data.
- **Model:** Provides an interface for database operations.
- **ORM:** Maps relational database tables to application objects.
- **ODM:** Maps document database data to application objects.
- **Relationships:** Connect related records.
- **Validation:** Ensure incoming data is valid.
- **Migrations:** Track changes to database structure.
- **Connection Pool:** Reuse database connections efficiently.
- **Indexes:** Improve query performance.

## ⚖️ 7. Quick Comparison

|Database|Type|Node.js Tool|
|---|---|---|
|MongoDB|NoSQL|Mongoose|
|PostgreSQL|SQL|Prisma|
|MySQL|SQL|mysql2|

## 🎯 Remember

- **MongoDB:** Documents and collections.
- **PostgreSQL:** Tables and relationships.
- **MySQL:** Relational tables.
- **Mongoose:** Work with MongoDB documents.
- **Prisma:** Work with databases through a type-safe ORM.
- **CRUD:** Create, Read, Update, Delete.

> 🧠 Express handles HTTP requests. The database stores the data. The ORM or ODM connects your application logic to the database.

---
