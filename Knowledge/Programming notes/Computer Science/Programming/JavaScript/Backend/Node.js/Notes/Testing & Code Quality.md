# 🧪 09 — Testing & Code Quality

> 💡 Testing ensures our backend works correctly, handles errors and remains reliable as the application grows.

## 1. 🎯 Testing Levels

|Type|Purpose|
|---|---|
|Unit|Test individual functions|
|Integration|Test routes, databases and middleware together|
|End-to-End (E2E)|Test complete user workflows|
|Contract|Verify API matches its defined interface|

## 2. 🛠️ Testing Tools

- **Node.js Test Runner** — Built-in testing tool.
- **Jest** — JavaScript testing framework.
- **Vitest** — Fast testing framework.
- **Supertest** — Test HTTP endpoints.

## 3. 🧩 Basic Unit Test

Node.js built-in test runner.

```js
// math.js
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

```js
// math.test.js
const test = require('node:test');
const assert = require('node:assert');
const sum = require('./math');

test('should add two numbers', () => {
  assert.strictEqual(sum(2, 3), 5);
});
```

Run:

```bash
node --test
```

## 4. 🌐 API Integration Test

Use Supertest to test HTTP endpoints.

```js
const request = require('supertest');
const app = require('../app');

test('GET /tasks should return tasks', async () => {
  const response = await request(app)
    .get('/tasks')
    .expect(200);

  console.log(response.body);
});
```

Install:

```bash
npm install --save-dev supertest
```

## 5. 🚨 Test Failure Cases

A good backend must handle errors correctly.

```js
// Unauthorized
await request(app)
  .get('/tasks')
  .expect(401);

// Invalid input
await request(app)
  .post('/tasks')
  .send({})
  .expect(400);

// Missing record
await request(app)
  .get('/tasks/99999')
  .expect(404);
```

Also test:

- Database errors.
- Request timeouts.
- Permission restrictions.
- Unexpected server errors.

## 6. 🧰 Test Helpers

|Technique|Purpose|
|---|---|
|Fixtures|Predefined test data|
|Factories|Generate test objects|
|Mocks|Simulate dependencies|
|Dependency Injection|Replace real services with test versions|
|Test Database|Keep tests isolated|

Example — Mock:

```js
const userService = {
  findUser: async () => ({
    id: 1,
    name: 'John'
  })
};
```

## 7. 📊 Code Quality

**Coverage:** Shows which parts of the code are tested.

**Linting:** Detects potential code problems.

**Formatting:** Keeps code consistent.

Example tools:

```bash
npm install --save-dev eslint prettier
```

## 8. 🚀 Continuous Integration (CI)

Automatically run checks whenever code is pushed.

Typical CI pipeline:

```js
Push Code
   ↓
Install Dependencies
   ↓
Run Linter
   ↓
Run Tests
   ↓
Generate Coverage
   ↓
Build Application
```

## 🧠 Professional Habits

- Keep tests independent and deterministic.
- Test behavior, not internal implementation.
- Test success AND failure cases.
- Use isolated test databases.
- Clean up test data after execution.
- Don't rely only on coverage percentages.
- Run tests automatically through CI.

---

## 📌 Remember

- **Unit** → Does the function work?
- **Integration** → Do components work together?
- **E2E** → Does the complete workflow work?
- **Contract** → Does the API follow its expected interface?
- **Supertest** → Does the HTTP endpoint behave correctly?
- **CI** → Are automated checks running consistently?

> 🎯 Good testing isn't about having more tests. It's about having confidence that your backend behaves correctly, even when things go wrong.

---
