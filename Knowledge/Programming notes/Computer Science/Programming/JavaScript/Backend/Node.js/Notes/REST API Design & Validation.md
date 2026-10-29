# 🧱 06 — REST API Design & Validation

> [!abstract] 🎯 Goal Build predictable APIs. Validate every input. Return consistent responses.

## 🛣️ 1. Resource Design

Use **nouns** for resources and HTTP methods for actions.

|Method|Endpoint|Purpose|
|---|---|---|
|`GET`|`/api/tasks`|📋 List tasks|
|`GET`|`/api/tasks/:id`|🔍 Get one task|
|`POST`|`/api/tasks`|➕ Create task|
|`PATCH`|`/api/tasks/:id`|✏️ Update task|
|`DELETE`|`/api/tasks/:id`|🗑️ Delete task|

```js
app.get("/api/tasks", getTasks);
app.post("/api/tasks", createTask);
app.patch("/api/tasks/:id", updateTask);
app.delete("/api/tasks/:id", deleteTask);
```

## 🚦 2. HTTP Status Codes

|Code|Meaning|
|---|---|
|`200`|✅ Success|
|`201`|➕ Created|
|`204`|✅ Success, no body|
|`400`|⚠️ Invalid request|
|`401`|🔐 Not authenticated|
|`403`|🚫 Forbidden|
|`404`|🔍 Not found|
|`409`|⚔️ Conflict|
|`429`|⏳ Too many requests|
|`500`|💥 Server error|

```js
res.status(201).json({ id: 1, title: "Learn Node.js" });
res.status(404).json({ error: "Task not found" });
```

## 🛡️ 3. Input Validation with Zod

Install:

```bash
npm install zod
```

Define a schema:

```js
import { z } from "zod";

const taskSchema = z.object({
  title: z.string().min(1).max(100),
  completed: z.boolean().default(false),
});
```

Validate incoming data:

```js
const result = taskSchema.safeParse(req.body);

if (!result.success) {
  return res.status(400).json({
    error: "Validation failed",
    details: result.error.issues,
  });
}

const task = result.data;
```

📌 Validate all input sources:

- `req.body` → Submitted data
- `req.params` → URL parameters
- `req.query` → Filters and pagination

## 📦 4. Consistent Responses

Keep response structures predictable.

```js
// ✅ Success
res.status(200).json({
  data: { id: 1, title: "Learn REST" },
});

// ⚠️ Client error
res.status(400).json({
  error: { message: "Invalid task title" },
});

// 💥 Server error
res.status(500).json({
  error: { message: "Internal server error" },
});
```

- `4xx` → Client request problem.
- `5xx` → Server problem.

🔒 Never expose stack traces or secrets to clients.

## 🔎 5. Pagination, Filtering & Sorting

Use query parameters to control collections.


```http
GET /api/tasks?page=2&limit=10&completed=false&sort=title
```


```js
const page = Math.max(1, Number(req.query.page) || 1);
const limit = Math.min(
  100,
  Math.max(1, Number(req.query.limit) || 10)
);

const offset = (page - 1) * limit;
```

- `page` → Page number
- `limit` → Maximum results
- `completed` → Filter
- `sort` → Sort order or field

⚠️ Validate query values and allowlist sortable fields.

## 🔖 6. API Versioning

Use versions when introducing breaking changes.

```js
app.use("/api/v1/tasks", taskRoutes);
```

Example endpoint:

```http
GET /api/v1/tasks
```

📌 Keep existing clients working when possible.

## 📚 7. OpenAPI & Swagger UI

Document endpoints, parameters, and responses.

```yaml
paths:
  /api/tasks:
    get:
      summary: List tasks
      responses:
        "200":
          description: Tasks retrieved
        "500":
          description: Server error
```

- 📘 **OpenAPI** → Describes the API.
- 🖥️ **Swagger UI** → Displays interactive API documentation.

## 🚦 8. Rate Limits & Request Size

⏳ **Rate limiting** — control excessive requests.


```bash
// Example policy:
// 100 requests per 15 minutes per client
```

📦 **Request size limits** — reject oversized payloads.

```js
app.use(express.json({ limit: "100kb" }));
```

🔁 **Idempotency** — prevent duplicate operations when requests are retried.

```http
POST /api/payments
Idempotency-Key: unique-request-id
```

Store the key and original result so repeated requests with the same key do not create duplicate payments.

---

> [!tip] 💡 Remember **Design clearly → Validate early → Handle errors → Respond consistently.**

