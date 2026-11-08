# 🏗️ 10 — Architecture & Maintainable Code

> Good architecture makes code easier to understand, test, change, and grow.

## 📁 1. Layered Architecture

Organize code by responsibility. Each layer should have one clear job.

```js
src/
├── routes/          # URLs and HTTP methods
├── controllers/     # Handle requests and responses
├── services/        # Business logic
├── repositories/    # Database operations
├── middleware/      # Shared request processing
├── schemas/         # Input validation
├── config/          # Environment configuration
└── errors/          # Custom error handling
```

### 🔹 Routes — Where requests go

Connect HTTP endpoints to controllers.

```js
router.post("/tasks", taskController.create);
```

### 🔹 Controllers — Handle HTTP

Receive requests, call services, return responses.

```js
export async function create(req, res, next) {
  try {
    const task = await taskService.create(req.body);
    res.status(201).json(task);
  } catch (error) {
    next(error);
  }
}
```

### 🔹 Services — Business logic

Contain application rules. Should not depend on Express.

```js
export async function create(data) {
  if (!data.title) {
    throw new Error("Title is required");
  }

  return taskRepository.create(data);
}
```

### 🔹 Repositories — Database access

Keep database queries separate from business logic.

```js
export async function create(data) {
  return db.task.create({ data });
}
```

### 🔹 Middleware — Shared request logic

Runs between receiving a request and handling it.

```js
app.use(express.json());
app.use(authMiddleware);
```

### 🔹 Schemas — Validate input

Define what valid data looks like.

```js
const taskSchema = z.object({
  title: z.string().min(1),
  completed: z.boolean().default(false)
});
```

### 🔹 Config — Environment settings

Keep configuration in one place.

```js
export const config = {
  port: process.env.PORT || 3000,
  databaseUrl: process.env.DATABASE_URL
};
```

### 🔹 Errors — Consistent error handling

Centralize how application errors become HTTP responses.

```js
app.use((err, req, res, next) => {
  res.status(err.status || 500).json({
    error: err.message || "Internal Server Error"
  });
});
```

---

## 🧠 2. Important Architecture Concepts

### 1️⃣ Separation of Concerns

Each part handles a different responsibility.

❌ Everything in one controller:

```js
app.post("/tasks", async (req, res) => {
  // Validate input
  // Apply business rules
  // Query database
  // Return response
});
```

✅ Separate responsibilities:

```js
// Route → Controller → Service → Repository
```

### 2️⃣ Dependency Inversion

High-level business logic should depend on abstractions, not specific implementations.

```js
function createTaskService(repository) {
  return {
    create: (data) => repository.create(data)
  };
}
```

Now the service doesn't care whether the repository uses PostgreSQL, MongoDB, or a mock.

### 3️⃣ Dependency Injection (DI)

Pass dependencies into a function instead of creating them inside it.

```js
const taskService = createTaskService(taskRepository);
```

**Why?** Easier testing, flexibility, and less coupling.

### 4️⃣ Composition Over Inheritance

Build functionality by combining smaller objects or functions.

```js
const canLog = {
  log: (message) => console.log(message)
};

const canSave = {
  save: (data) => console.log("Saved:", data)
};

const taskManager = {
  ...canLog,
  ...canSave
};
```

Prefer combining behavior when inheritance would create unnecessary complexity.

---

## 🏛️ 3. Advanced Architecture

|Concept|Meaning|
|---|---|
|**DDD**|Organize code around business domains and rules.|
|**Bounded Contexts**|Separate areas with their own domain models and language.|
|**Modular Monolith**|One application divided into independent modules.|
|**Domain Events**|Events describing something that happened in the business.|
|**Message Brokers**|Allow services to communicate asynchronously.|
|**CQRS**|Separate reading data from changing data.|
|**Event Sourcing**|Store changes as events instead of only the latest state.|
|**Microservices**|Split an application into independently deployable services.|

### 🔸 Domain Events

Represent something that happened.

```js
{
  type: "TaskCreated",
  payload: { taskId: 123 }
}
```

Other parts of the application can react to this event.

### 🔸 Message Brokers

Tools such as RabbitMQ or Kafka help systems exchange messages asynchronously.

```js
Order Service
     ↓
Message Broker
     ↓
Email Service
```

### 🔸 CQRS

Separate operations:

```js
// Command: change data
await taskService.create(data);

// Query: read data
const tasks = await taskService.getAll();
```

Useful when reading and writing have very different requirements.

### 🔸 Event Sourcing

Instead of storing only the current state:

```js
{ balance: 100 }
```

Store the events that produced it:

```js
[
  { type: "MoneyDeposited", amount: 150 },
  { type: "MoneyWithdrawn", amount: 50 }
]
```

Current state is reconstructed from events.

### 🔸 Microservices

Split an application into independently running services.

```js
        API Gateway
             |
    ┌────────┼────────┐
    ↓        ↓        ↓
  Users    Tasks    Payments
```

Each service can have its own database and deployment.

⚠️ Distributed systems introduce network failures, latency, retries, and data consistency challenges.

---

## ⭐ 4. The Golden Rule

**Start with a well-structured monolith.**

Don't introduce complexity before you need it.

- Modular monolith → simpler development and deployment.
- Microservices → more independent scaling, but more operational complexity.
- CQRS and Event Sourcing → powerful patterns, but not necessary for most applications.

**Good architecture isn't about using more patterns. It's about keeping responsibilities clear and changes easy.**

---

## 🎯 Key Takeaway

```js
Routes       → Where does the request go?
Controllers  → What does HTTP need?
Services     → What should the application do?
Repositories → How is data stored?
Middleware   → What happens across requests?
Schemas      → Is the input valid?
Config       → Where are settings defined?
Errors       → How are failures handled?
```

**Remember:** Business logic should be independent of Express and the database. That's what makes an application easier to test and maintain.

---
