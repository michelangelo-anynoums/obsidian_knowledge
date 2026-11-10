# ⏱️ Timers — Node.js

Timers allow you to **schedule code execution** after a delay or repeatedly at specific intervals.

## 1. `setTimeout()`

⏳ Executes a callback **once** after a specified delay.

```js
setTimeout(() => {
  console.log("Hello after 2 seconds!");
}, 2000);
```

## 2. `setInterval()`

🔁 Executes a callback **repeatedly** at a specified interval.

```js
setInterval(() => {
  console.log("Repeating every second");
}, 1000);
```

## 3. `setImmediate()`

⚡ Executes a callback on the next iteration of the Node.js event loop.

```js
setImmediate(() => {
  console.log("Executed immediately");
});
```

## 4. Cancel Timers

🛑 Stop scheduled callbacks using their timer IDs.

```js
const timeout = setTimeout(() => {
  console.log("Hello!");
}, 3000);

clearTimeout(timeout);
```

```js
const interval = setInterval(() => {
  console.log("Running...");
}, 1000);

clearInterval(interval);
```

## 💡 Remember

- `setTimeout()` → Run once after a delay.
- `setInterval()` → Run repeatedly.
- `setImmediate()` → Run on the next event loop iteration.
- `clearTimeout()` → Cancel a timeout.
- `clearInterval()` → Cancel an interval.

> ⚠️ Timer delays are not exact execution times. Node.js runs callbacks when the event loop can process them.

---
