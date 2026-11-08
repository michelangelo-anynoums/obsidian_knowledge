# ☁️ 12 — Deployment & DevOps

> 🚀 **Goal:** Prepare, deploy, monitor, and recover a Node.js application in production.

## 🐧 1. Linux & Networking

Understand the server environment.

```bash
# Current directory
pwd

# List files
ls -la

# Running processes
ps aux

# Find process using port 3000
lsof -i :3000

# File permissions
chmod 600 .env
```

- **Processes:** Running applications.
- **Permissions:** Who can read, write, or execute files.
- **Networking:** Ports, IPs, DNS, HTTP and HTTPS.

## 🌿 2. Git & Collaboration

Track changes and collaborate safely.

```bash
git checkout -b feature/auth
git add .
git commit -m "Add authentication"
git push origin feature/auth
```

- **Branch:** Independent development line.
- **Pull Request:** Propose changes for review.
- **Code Review:** Check code before merging.

## 🐳 3. Docker

Package your application with its dependencies.

**Dockerfile**

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

**Build & run**


```bash
docker build -t my-api .
docker run -p 3000:3000 my-api
```

- **Image:** Application template.
- **Container:** Running image.
- **Volume:** Persistent data storage.
- **Network:** Communication between containers.

## 🧩 4. Docker Compose

Run multiple services together.

**compose.yaml**


```yaml
services:
  api:
    build: .
    ports:
      - "3000:3000"
    env_file:
      - .env
    depends_on:
      - db

  db:
    image: postgres:17
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```


```bash
docker compose up -d
docker compose logs -f
docker compose down
```

💡 One command starts your API and database.

## 🔐 5. Environment Variables & Secrets

Never hardcode passwords, API keys, or database credentials.

**.env**



```env
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/app
JWT_SECRET=your-secret
```

**Node.js**



```js
const port = process.env.PORT || 3000;
const secret = process.env.JWT_SECRET;
```

Validate required configuration at startup:



```js
if (!process.env.JWT_SECRET) {
  throw new Error("JWT_SECRET is required");
}
```

⚠️ Never commit `.env` to Git. Use hosting-platform secret management in production.

## ⚙️ 6. CI/CD Pipelines

Automate testing and deployment.

Typical pipeline:


```
Push Code
    ↓
Install Dependencies
    ↓
Run Tests
    ↓
Build Application
    ↓
Deploy
```

**Example GitHub Actions workflow**

`.github/workflows/ci.yml`


```yaml
name: Node.js CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 22

      - run: npm ci
      - run: npm test
```

- **CI:** Automatically test code changes.
- **CD:** Automatically deliver or deploy code.

## 🌐 7. Reverse Proxy & HTTPS

A reverse proxy receives external requests and forwards them to your Node.js server.


```
Client
  ↓ HTTPS
Nginx (Port 443)
  ↓ HTTP
Node.js (Port 3000)
```

Example Nginx configuration:


```nginx
server {
    listen 443 ssl;
    server_name example.com;

    location / {
        proxy_pass http://localhost:3000;
    }
}
```

🔒 HTTPS encrypts communication between clients and your server.

## 🗄️ 8. Databases & Backups

Production databases need persistent storage and recovery plans.

**PostgreSQL backup:**


```bash
pg_dump -U postgres app > backup.sql
```

**Restore:**

```bash
psql -U postgres app < backup.sql
```

Important concepts:

- **Managed Database:** Cloud provider handles database infrastructure.
- **Backup:** Copy of persistent data.
- **Restore:** Recover data from a backup.
- **Migration:** Safely change database structure.

Example migration:

```sql
ALTER TABLE users
ADD COLUMN avatar_url TEXT;
```

💡 Always consider database compatibility when deploying new application versions.

## 🔄 9. Process Management & Graceful Shutdown

A production server should close connections safely.

```js
const server = app.listen(3000);

process.on("SIGTERM", () => {
  console.log("Shutting down...");

  server.close(() => {
    console.log("Server closed");
    process.exit(0);
  });
});
```

- **Process Manager:** Keeps applications running.
- **Graceful Shutdown:** Finishes existing requests before stopping.
- **Logs:** Record errors and application events.

## ☁️ 10. Cloud Fundamentals

Understand the basic building blocks of cloud infrastructure.

|Concept|Purpose|
|---|---|
|Compute|Run Node.js applications|
|Storage|Store files and backups|
|Networking|Connect services|
|Identity & Access|Control permissions|
|Managed Database|Host database services|

Examples: AWS, Google Cloud and Azure.

## 📊 11. Monitoring & Health Checks

Know whether your application is running correctly.

**Health endpoint (Express):**

```js
app.get("/health", (req, res) => {
  res.status(200).json({
    status: "ok",
    uptime: process.uptime()
  });
});
```

**Useful metrics:**

- CPU and memory usage.
- Error rates.
- Request latency.
- Database availability.
- Application logs.

```js
console.error("Database connection failed");
```

## 🚀 12. Deployment Strategies

Different ways to release application updates.

|Strategy|Description|
|---|---|
|Rolling|Update instances gradually|
|Blue-Green|Switch between two environments|
|Canary|Release to a small percentage first|
|Rollback|Return to a previous version|

💡 Zero downtime means users can continue using the service during deployment.

---

## 🛡️ Production Essentials

A production-ready Node.js application should:

- 🔐 Validate configuration and protect secrets.
- 🔒 Use HTTPS.
- 📦 Limit request sizes and validate inputs.
- ❤️ Provide health endpoints.
- 📊 Monitor errors, logs and latency.
- 🗄️ Back up persistent data.
- 🔄 Support graceful shutdown.
- ⏪ Have a tested rollback and recovery strategy.

**Remember:**

> Deployment gets your application online. DevOps keeps it reliable, observable, secure, and recoverable.

---
