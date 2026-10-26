# 🛑 AbortController & AbortSignal

## 💡 What are they?

- 🛑 `AbortController` — Cancels an operation.
- 📡 `AbortSignal` — Communicates the cancellation to that operation.

> [!important] Useful for cancelling `fetch()` requests, handling timeouts, and stopping unnecessary work.

## ⚙️ Basic Example

```js
const controller = new AbortController();

fetch("https://api.example.com/users", {
  signal: controller.signal
});

// Cancel the request
controller.abort();
```

Calling `abort()` signals cancellation. The request's promise rejects, usually with an `AbortError`.

## ⏱️ Timeout Example

```js
fetch("https://api.example.com/users", {
  signal: AbortSignal.timeout(3000)
});
```

⏳ Automatically aborts the request if it takes longer than **3 seconds**.

## 🧠 Remember

- `AbortController` → Cancels.
- `AbortSignal` → Communicates cancellation.
- `controller.abort()` → Triggers cancellation.
- `AbortSignal.timeout(ms)` → Cancels after a time limit.

> 🎯 **Key takeaway:** Use `AbortController` when you need manual cancellation and `AbortSignal.timeout()` when you need a simple timeout.

---
