# 🛠️ Express.js Fundamentals

> [!abstract] The idea **Express.js** is a lightweight Node.js framework for building web servers and REST APIs.
> 
> `Request → Middleware → Route → Response`

## 01 · Create a server

Install Express:

```bash
npm init -y
npm install express
```

Create `app.js`:

```js
const express = require('express');
const app = express();

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

`express()` creates the application. `listen()` starts the server.

## 02 · Routing

A **route** defines how the server responds to an HTTP method and URL.

```js
app.get('/tasks', (req, res) => {
  res.json({ message: 'All tasks' });
});

app.post('/tasks', (req, res) => {
  res.status(201).json({ message: 'Task created' });
});

app.put('/tasks/:id', (req, res) => {
  res.json({ message: 'Task replaced' });
});

app.patch('/tasks/:id', (req, res) => {
  res.json({ message: 'Task updated' });
});

app.delete('/tasks/:id', (req, res) => {
  res.status(204).end();
});
```

`GET` reads · `POST` creates · `PUT` replaces · `PATCH` updates · `DELETE` removes.

## 03 · Request data

Express provides three common ways to access incoming data.

**Route parameters** identify a specific resource.

```js
app.get('/users/:id', (req, res) => {
  res.json({ userId: req.params.id });
});
```

`GET /users/42` → `{ "userId": "42" }`

**Query strings** filter or customize a request.

```js
app.get('/tasks', (req, res) => {
  const { status } = req.query;
  res.json({ status });
});
```

`GET /tasks?status=done` → `{ "status": "done" }`

**Request bodies** contain data sent by the client.

```js
app.use(express.json());

app.post('/tasks', (req, res) => {
  const { title } = req.body;
  res.status(201).json({ title });
});
```

`express.json()` parses incoming JSON. Place it before routes that use `req.body`.

## 04 · Responses

Use `res` to send data and control the HTTP status.

```js
res.send('Hello!');                    // Text
res.json({ success: true });           // JSON
res.status(404).json({ error: 'Not found' });
res.status(201).json({ id: 1, title: 'Learn Express' });
res.status(204).end();                 // No response body
```

**Remember:** `200` = OK · `201` = Created · `204` = No Content · `400` = Bad Request · `401` = Unauthenticated · `403` = Forbidden · `404` = Not Found · `500` = Server Error.

## 05 · Middleware

Middleware is a function that runs during the request-response lifecycle. It can inspect a request, modify it, send a response, or pass control onward.


```js
function logger(req, res, next) {
  console.log(req.method, req.url);
  next();
}

app.use(logger);
```

`next()` continues to the next middleware or route handler.

**Order matters.** Middleware runs in the order it is registered.

```js
app.use(express.json()); // Parse JSON
app.use(logger);         // Log requests

app.get('/tasks', (req, res) => {
  res.json([]);
});
```

### Common middleware

```js
app.use(express.json());                    // JSON bodies
app.use(express.urlencoded({ extended: true })); // Form bodies
app.use(express.static('public'));           // Static files
```

For example, `public/index.html` becomes available at `/index.html`.

### Authentication & authorization

Authentication asks **who are you?** Authorization asks **what can you access?**

```js
function requireAuth(req, res, next) {
  if (!req.user) {
    return res.status(401).json({
      error: 'Authentication required'
    });
  }

  next();
}

app.get('/profile', requireAuth, (req, res) => {
  res.json({ message: 'Private profile' });
});
```

`req.user` must be populated by a trusted authentication layer before this middleware runs. This example illustrates the pattern, not a complete authentication system.

### Validation & sanitization

Never assume client input is valid.

```js
app.post('/tasks', (req, res, next) => {
  const { title } = req.body;

  if (typeof title !== 'string' || !title.trim()) {
    return res.status(400).json({
      error: 'A valid title is required'
    });
  }

  req.body.title = title.trim();
  next();
});
```

> [!important] Validation checks input. Sanitization normalizes or cleans it. Use schema validation for more complex data.

## 06 · Routers

`express.Router()` separates endpoints into reusable modules.

Project structure:

```js
src/
  app.js
  routes/
    tasks.js
    users.js
```

`routes/tasks.js`

```js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.json([]);
});

router.get('/:id', (req, res) => {
  res.json({ id: req.params.id });
});

module.exports = router;
```

`app.js`


```js
const express = require('express');
const app = express();

const taskRoutes = require('./routes/tasks');

app.use(express.json());
app.use('/api/tasks', taskRoutes);

app.listen(3000);
```

`GET /api/tasks` matches `router.get('/')`.

`GET /api/tasks/42` matches `router.get('/:id')`.

## 07 · Error handling

Handle unknown routes and unexpected errors centrally.

### Missing routes

Register this after your valid routes.

```js
app.use((req, res) => {
  res.status(404).json({
    error: 'Route not found'
  });
});
```

### Centralized error handler

Register this after your routes and other middleware.

```js
app.use((err, req, res, next) => {
  console.error(err);

  res.status(err.status || 500).json({
    error: err.status ? err.message : 'Internal server error'
  });
});
```

Pass an error with `next(err)` to reach the error handler.

```js
app.get('/example', (req, res, next) => {
  next(new Error('Something went wrong'));
});
```

> [!important] Avoid exposing stack traces or sensitive error details to clients. In Express 5, rejected promises from route handlers are forwarded to error handling automatically; Express 4 generally needs explicit forwarding or an async wrapper.

## 08 · Request IDs, rate limits & security

Reusable middleware helps protect and monitor an API.

```js
const { randomUUID } = require('node:crypto');

app.use((req, res, next) => {
  req.id = randomUUID();
  res.setHeader('X-Request-ID', req.id);
  next();
});
```

A request ID helps connect a request to its logs.

Install common security middleware:

```bash
npm install helmet express-rate-limit
```

```js
const helmet = require('helmet');
const { rateLimit } = require('express-rate-limit');

app.use(helmet());

app.use(rateLimit({
  windowMs: 15 * 60 * 1000,
  limit: 100
}));
```

> [!abstract] `helmet` sets security-related HTTP headers. Rate limiting restricts repeated requests. Configure limits according to your API and deployment.

For production systems, also consider request timeouts, HTTPS, secure authentication, and input validation.

## 09 · Environment configuration

Keep environment-specific values outside your source code.

```js
const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

Start with a custom port:
```bash
PORT=4000 node app.js
```

Use environment variables for ports, database URLs, and secrets. Never commit real secrets to version control.

## 10 · The request lifecycle

```text
Client Request
     ↓
Request ID / Logger
     ↓
Body Parser
     ↓
Security / Rate Limit
     ↓
Authentication
     ↓
Router
     ↓
Validation
     ↓
Response
```

If something fails:

```text
Route or Middleware
       ↓
   next(err)
       ↓
Error Handler
       ↓
JSON Error Response
```

> [!important] The exact order depends on the application. For example, public routes may not require authentication, and validation usually belongs close to the route that consumes the input.

## 11 · Mini project — Task API

Bring the concepts together.

```js
const express = require('express');
const app = express();

app.use(express.json());

let tasks = [
  { id: 1, title: 'Learn Express', done: false }
];

app.get('/api/tasks', (req, res) => {
  res.json(tasks);
});

app.post('/api/tasks', (req, res) => {
  const { title } = req.body;

  if (typeof title !== 'string' || !title.trim()) {
    return res.status(400).json({
      error: 'Title is required'
    });
  }

  const task = {
    id: tasks.length
      ? Math.max(...tasks.map(t => t.id)) + 1
      : 1,
    title: title.trim(),
    done: false
  };

  tasks.push(task);
  res.status(201).json(task);
});

app.listen(3000);
```

Test it:

```bash
curl http://localhost:3000/api/tasks
```

Create a task:

```bash
curl -X POST http://localhost:3000/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Practice middleware"}'
```

This is an in-memory demo, so tasks disappear when the server restarts. Extend it with `GET`, `PATCH`, and `DELETE` by ID, then split users and tasks into separate routers and add centralized error handling.

---

> [!tip] Mental model **Express = Routes + Middleware + Request/Response**
> 
> Routes define _what happens_. Middleware defines _what happens along the way_. Responses define _what the client receives_.