# 🧪 Node.js — assert

**assert** — Check conditions and verify expected results in tests and debugging.


```js
import assert from 'node:assert/strict';

assert.equal(2 + 2, 4);
assert.ok(true);
assert.deepEqual(
  { name: 'John' },
  { name: 'John' }
);
```

### ⚡ Common methods

|Method|Purpose|
|---|---|
|`assert.ok(value)`|Check if truthy|
|`assert.equal(a, b)`|Compare values|
|`assert.strictEqual(a, b)`|Strict comparison|
|`assert.deepEqual(a, b)`|Compare objects|
|`assert.throws(fn)`|Check if function throws|
|`assert.fail()`|Force assertion failure|

### 💡 Example

```js
const age = 20;

assert.ok(age >= 18, 'Must be an adult');
```

**Note:** Node.js includes `assert` as a built-in module. No installation required.

---
