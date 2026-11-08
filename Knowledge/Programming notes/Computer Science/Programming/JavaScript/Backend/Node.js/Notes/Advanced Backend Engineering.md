# 📡 11 — Advanced Backend Engineering

> 🎯 **Goal:** Move from building functional APIs to building reliable, scalable, and observable backend systems.

## 🛡️ 1. Reliability

Keep your API running even when things fail.

### ⏱️ Timeouts & retries

Prevent requests from waiting forever. Retry temporary failures with exponential backoff and jitter.

```js
const delay = ms => new Promise(resolve => setTimeout(resolve, ms));

async function retry(fn, attempts = 3) {
  for (let i = 0; i < attempts; i++) {
    try {
      return await fn();
    } catch (err) {
      if (i === attempts - 1) throw err;

      const backoff = 500 * 2 ** i;
      const jitter = Math.random() * 200;

      await delay(backoff + jitter);
    }
  }
}
```

### 🔁 Idempotency

Repeated requests should not create duplicate operations.

```js
app.post("/payments", async (req, res) => {
  const { idempotencyKey } = req.body;

  const existing = await Payment.findOne({ idempotencyKey });

  if (existing) return res.json(existing);

  const payment = await Payment.create({
    ...req.body,
    idempotencyKey
  });

  res.json(payment);
});
```

_In production, enforce uniqueness at database level and handle concurrent requests._

### 🔌 Graceful shutdown

Finish active requests before closing connections.

```js
process.on("SIGTERM", async () => {
  console.log("Shutting down...");

  server.close(async () => {
    await db.disconnect();
    process.exit(0);
  });
});
```

### ❤️ Health & readiness checks

```js
app.get("/health", (req, res) => {
  res.json({ status: "ok" });
});

app.get("/ready", async (req, res) => {
  const ready = await db.ping();

  res.status(ready ? 200 : 503).json({ ready });
});
```

- **Health:** Is the process alive?
- **Readiness:** Can it handle requests?

### 🗄️ Transactions & consistency

Keep related database operations together.

```js
await db.transaction(async (tx) => {
  await tx.users.update(...);
  await tx.orders.create(...);
});
```

If an operation fails, the transaction rolls back.

### ⚡ Other reliability patterns

- **Circuit breaker:** Stop calling an unhealthy service temporarily.
- **Bulkhead:** Isolate resources to prevent one failure affecting everything.
- **Partial failure:** Handle situations where one service fails but others continue.
- **Duplicate messages:** Use message IDs and deduplication.

---

## 🚀 2. Performance & Scalability

Make your application faster and capable of handling more traffic.

### 🔍 CPU & memory profiling

Find performance bottlenecks.

```bash
node --inspect server.js
```

Use Chrome DevTools to inspect CPU usage and memory.

### 🗄️ Database indexing

Speed up frequently executed queries.

```sql
CREATE INDEX idx_users_email
ON users(email);
```

### 🔌 Connection pooling

Reuse database connections instead of opening a new one for every request.

```js
const pool = new Pool({
  max: 10,
  idleTimeoutMillis: 30000
});
```

### ⚡ Caching

Store frequently requested data.

```js
const cached = await redis.get("users");

if (cached) return JSON.parse(cached);

const users = await User.find();

await redis.set("users", JSON.stringify(users), {
  EX: 60
});
```

- **Cache invalidation:** Remove outdated cached data.
- **Cache stampede:** Prevent many requests from rebuilding the same cache simultaneously.

### 📊 Load testing

Measure performance under traffic.

```bash
npx autocannon -c 100 -d 10 http://localhost:3000
```

- **Throughput:** Requests per second.
- **Latency:** Time needed to process a request.

### 📈 Horizontal scaling

Run multiple API instances instead of relying on one server.

```
             Load Balancer
                   |
          ┌────────┼────────┐
          ↓        ↓        ↓
        API 1    API 2    API 3
          └────────┼────────┘
                   |
                Database
```

Keep APIs stateless so requests can reach any instance.

### 🌐 Reverse proxies & compression

Use Nginx as a reverse proxy and Express compression for smaller responses.


```js
import compression from "compression";

app.use(compression());
```

### ⚙️ Background processing

Move heavy tasks outside HTTP requests.

```js
await queue.add("send-email", {
  userId: 123
});
```

- **Worker threads:** CPU-intensive JavaScript tasks.
- **Queues:** Background jobs and asynchronous processing.
- **Scheduled jobs:** Tasks executed at specific intervals.

### 🔴 Real-time communication

- **WebSockets:** Two-way real-time communication.
- **SSE:** Server-to-client event streaming.

```js
const ws = new WebSocket("ws://localhost:3000");
ws.send("Hello server!");
```

---

## 📊 3. Observability

Understand what your application is doing and why something fails.

### 📝 Structured logging — Pino

Store logs as structured JSON instead of plain text.

```js
import pino from "pino";

const logger = pino();

logger.info({
  userId: 123,
  action: "login"
}, "User logged in");
```

### 🆔 Request & correlation IDs

Track requests across multiple services.

```js
import { randomUUID } from "node:crypto";

app.use((req, res, next) => {
  req.id = randomUUID();
  res.setHeader("X-Request-ID", req.id);

  next();
});
```

### 📈 Metrics

Monitor four important signals:

|Metric|Meaning|
|---|---|
|Request rate|Requests per second|
|Errors|Failed requests|
|Latency|Response time|
|Resources|CPU and memory usage|

### 🔎 Distributed tracing

Follow one request across multiple services.

```
API Gateway
    |
    ├── User Service
    |
    ├── Order Service
    |
    └── Payment Service
```

Use **OpenTelemetry** to collect traces, metrics, and logs.

### 🚨 Error monitoring & alerting

Detect problems and notify the team.

Common tools:

- Sentry — error monitoring.
- Prometheus — metrics.
- Grafana — dashboards.
- OpenTelemetry — instrumentation.

### 🎯 SLI & SLO

- **SLI:** What you measure.
- **SLO:** The reliability target.

Example:

```
SLI = Successful requests / Total requests

SLO = 99.9% successful requests
```

---

## 🧠 Key idea

|Area|Main question|
|---|---|
|Reliability 🛡️|Does it survive failures?|
|Performance 🚀|Can it handle more traffic?|
|Observability 📊|Can we understand what's happening?|

**Advanced backend engineering = Reliable + Scalable + Observable systems.**

---
