# 📡 Events — Event-Driven Communication

> An event represents something that has already happened. Other parts of the application can listen and react to it.

## 1. 🧠 What Are Events?

Instead of one function directly calling another, an application can publish an event.

```js
User registers
      ↓
UserRegistered event
      ↓
 ┌────┴─────┐
 ↓          ↓
Send Email  Create Profile
```

The user registration logic doesn't need to know who listens to the event.

## 2. 🔑 EventEmitter (Node.js)

Node.js provides a built-in event system through `EventEmitter`.

```js
import { EventEmitter } from "node:events";

const emitter = new EventEmitter();
```

### 🔹 Emit an event

Publish an event with data.

```js
emitter.emit("userRegistered", {
  id: 1,
  name: "Alex"
});
```

### 🔹 Listen for an event

React when an event happens.

```js
emitter.on("userRegistered", (user) => {
  console.log("Welcome:", user.name);
});
```

### 🔹 Complete example

```js
import { EventEmitter } from "node:events";

const emitter = new EventEmitter();

// Listener
emitter.on("taskCreated", (task) => {
  console.log("New task:", task.title);
});

// Publisher
function createTask(title) {
  const task = { title };

  emitter.emit("taskCreated", task);

  return task;
}

createTask("Learn Node.js");
```

**Output:**

```js
New task: Learn Node.js
```

## 3. 🎧 Important Event Methods

|Method|Purpose|
|---|---|
|`.on()`|Listen every time an event occurs.|
|`.once()`|Listen only once.|
|`.emit()`|Trigger an event.|
|`.off()`|Remove a listener.|
|`.removeAllListeners()`|Remove all listeners for an event.|

```js
// Listen once
emitter.once("paymentCompleted", () => {
  console.log("Payment received");
});

// Remove a listener
emitter.off("taskCreated", myListener);
```

## 4. ⚡ Async Event Listeners

Listeners can be asynchronous.

```js
emitter.on("userRegistered", async (user) => {
  await sendWelcomeEmail(user);

  console.log("Email sent!");
});
```

⚠️ Important: `emit()` does not wait for asynchronous listeners to finish.

If you need to coordinate asynchronous work, explicitly await it or use a suitable async event pattern.

## 5. 🏗️ Event-Driven Architecture

Applications can use events to connect different modules.

```js
        Order Service
              |
        OrderCreated
              |
        Message Broker
         /          \
        ↓            ↓
  Email Service  Stock Service
```

### 🔹 EventEmitter vs Message Broker

|EventEmitter|Message Broker|
|---|---|
|Inside one Node.js process|Communicates across processes|
|Simple and lightweight|Supports distributed systems|
|No built-in persistence|Can provide message persistence|
|Local listeners|Independent consumers|

Popular message brokers:

- **RabbitMQ** — message queues and routing.
- **Apache Kafka** — distributed event streaming.
- **Redis Pub/Sub** — lightweight publish/subscribe messaging.

## 6. 🛡️ Important Concepts

- **Publisher:** produces an event.
- **Subscriber:** listens for an event.
- **Event Payload:** data carried by an event.
- **Decoupling:** components don't need direct knowledge of each other.
- **Event Ordering:** the order in which events are processed.
- **Idempotency:** processing the same event more than once should not cause duplicate effects.
- **Error Handling:** failed event processing must be handled deliberately.

### 🔹 Naming Events

Use past-tense names because events describe something that happened.

```js
"UserRegistered"
"TaskCreated"
"PaymentCompleted"
"OrderCancelled"
```

## ⭐ Key Takeaway

```js
emit()       → Publish an event
on()         → Listen for an event
once()       → Listen only once
off()        → Remove a listener

EventEmitter → Communication inside one process
Broker       → Communication between services
```

**Remember:** Events reduce coupling. One part of your application announces what happened, and other parts decide what to do about it.

---
