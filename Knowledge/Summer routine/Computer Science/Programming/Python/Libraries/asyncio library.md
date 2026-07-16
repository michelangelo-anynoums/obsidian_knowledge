## 🧠 Python **asyncio** — Practical Developer Note

## 1. What is **asyncio** and why should you use it?

`asyncio` is a **built-in Python library** used to write **concurrent code** using `async` and `await`.

In simple terms:

> It lets your program **do multiple things at once without using multiple threads**.

Think of it like this:

- Normal Python = one task at a time (blocking)
- `asyncio` = start a task, pause it, do something else, come back later

This is especially useful for:

- Network requests (APIs, scraping)
- File I/O
- Bots (Discord, Telegram)
- High-performance tools (including security tooling)

---

### 🔎 Explore modules and asyncio in your console

 
```Python
help("modules")        # shows all available modules  
dir(asyncio)           # lists everything inside asyncio  
help(asyncio)          # full documentation of asyncio
```

---

## 2. Core Concepts (Explained Simply)

### ⚡ 1. **async** and **await**

These are the foundation.

- `async` → defines a function that can pause
- `await` → tells Python: “pause here until this finishes”

```Python
import asyncio  
  
async def say_hello():  
    print("Hello")  
    await asyncio.sleep(1)   # pause without blocking everything  
    print("World")  
  
asyncio.run(say_hello())
```

👉 Key idea:

- `time.sleep()` blocks everything ❌
- `asyncio.sleep()` pauses only this task ✅

---

### 🔁 2. Event Loop

The **event loop** is the engine of `asyncio`.

It:

- runs your async tasks
- switches between them when they pause

```Python
import asyncio  
  
async def main():  
    print("Running inside event loop")  
  
asyncio.run(main())   # creates and runs the loop
```

👉 Think of it as a **task scheduler**.

---

### 🧩 3. Coroutines

A coroutine is just:

> an **async def** function that hasn’t run yet

```Python
import asyncio  
  
async def my_task():  
    return "Done"  
  
coro = my_task()   # this does NOT run yet  
print(coro)        # just shows coroutine object  
  
asyncio.run(coro)  # now it runs
```

---

### 🚀 4. Running Multiple Tasks (Concurrency)

This is where `asyncio` shines.

```Python
import asyncio  
  
async def task(name, delay):  
    print(f"Start {name}")  
    await asyncio.sleep(delay)  
    print(f"End {name}")  
  
async def main():  
    await asyncio.gather(  
        task("A", 2),  
        task("B", 1),  
        task("C", 3)  
    )  
  
asyncio.run(main())
```

👉 Output happens **out of order** because tasks run concurrently.

---

### 📌 5. **asyncio.create_task()**

Used to start a task in the background.

```Python
import asyncio  
  
async def background():  
    await asyncio.sleep(2)  
    print("Background finished")  
  
async def main():  
    task = asyncio.create_task(background())  
    print("Main continues...")  
    await task  
  
asyncio.run(main())
```

👉 Useful for:

- parallel jobs
- listeners
- long-running processes

---

### ⏳ 6. Timeouts

Control how long something is allowed to run.

```Python
import asyncio  
  
async def slow_task():  
    await asyncio.sleep(5)  
  
async def main():  
    try:  
        await asyncio.wait_for(slow_task(), timeout=2)  
    except asyncio.TimeoutError:  
        print("Task took too long!")  
  
asyncio.run(main())
```

---

### 🔄 7. **asyncio.Queue** (Producer–Consumer pattern)

Very useful in hacking tools, scanners, etc.

```Python
import asyncio  
  
async def producer(queue):  
    for i in range(3):  
        await queue.put(i)  
        print(f"Produced {i}")  
  
async def consumer(queue):  
    while True:  
        item = await queue.get()  
        print(f"Consumed {item}")  
        queue.task_done()  
  
async def main():  
    queue = asyncio.Queue()  
  
    asyncio.create_task(consumer(queue))  
    await producer(queue)  
  
    await queue.join()  
  
asyncio.run(main())
```

---

## ⚡ Essential `asyncio` Methods (Simple + Practical)

---

## 1. `asyncio.run()`

👉 Starts your async program (entry point)

```Python
import asyncio  
  
async def main():  
    print("Hello async")  
  
asyncio.run(main())
```

---

## 2. `async def` + `await`

👉 Define and pause async functions

```Python
import asyncio  
  
async def task():  
    print("Start")  
    await asyncio.sleep(1)  
    print("End")  
  
asyncio.run(task())
```

---

## 3. `asyncio.sleep()`

👉 Non-blocking delay

```Python
import asyncio  
  
async def wait():  
    print("Waiting...")  
    await asyncio.sleep(2)  
    print("Done")  
  
asyncio.run(wait())
```

---

## 4. `asyncio.gather()`

👉 Run multiple tasks at the same time

```Python
import asyncio  
  
async def job(n):  
    await asyncio.sleep(n)  
    print(f"Job {n} done")  
  
async def main():  
    await asyncio.gather(  
        job(1),  
        job(2),  
        job(3)  
    )  
  
asyncio.run(main())
```

---

## 5. `asyncio.create_task()`

👉 Run a task in the background

```Python
import asyncio  
  
async def background():  
    await asyncio.sleep(2)  
    print("Background finished")  
  
async def main():  
    task = asyncio.create_task(background())  
    print("Doing other things...")  
    await task  
  
asyncio.run(main())
```

---

## 6. `asyncio.wait_for()`

👉 Add a timeout to a task

```Python
import asyncio  
  
async def slow():  
    await asyncio.sleep(5)  
  
async def main():  
    try:  
        await asyncio.wait_for(slow(), timeout=2)  
    except asyncio.TimeoutError:  
        print("Too slow!")  
  
asyncio.run(main())
```

---

## 7. `asyncio.Queue`

👉 Share data between tasks

```Python
import asyncio  
  
async def producer(q):  
    await q.put("data")  
  
async def consumer(q):  
    item = await q.get()  
    print(item)  
  
async def main():  
    q = asyncio.Queue()  
    await asyncio.gather(producer(q), consumer(q))  
  
asyncio.run(main())
```

---

## 8. `asyncio.Semaphore`

👉 Limit how many tasks run at once

```Python
import asyncio  
  
sem = asyncio.Semaphore(2)  
  
async def worker(n):  
    async with sem:  
        print(f"Task {n}")  
        await asyncio.sleep(1)  
  
async def main():  
    await asyncio.gather(*(worker(i) for i in range(5)))  
  
asyncio.run(main())
```

---

## 9. `asyncio.Lock`

👉 Prevent conflicts (race conditions)

```Python
import asyncio  
  
lock = asyncio.Lock()  
counter = 0  
  
async def safe():  
    global counter  
    async with lock:  
        temp = counter  
        await asyncio.sleep(0.1)  
        counter = temp + 1  
  
async def main():  
    await asyncio.gather(*(safe() for _ in range(3)))  
    print(counter)  
  
asyncio.run(main())
```

---

## 10. `asyncio.open_connection()`

👉 Open a network connection

```Python
import asyncio  
  
async def connect():  
    reader, writer = await asyncio.open_connection("example.com", 80)  
    print("Connected")  
    writer.close()  
    await writer.wait_closed()  
  
asyncio.run(connect())
```

---

## 11. `asyncio.create_subprocess_exec()`

👉 Run system commands asynchronously

```Python
import asyncio  
  
async def run():  
    proc = await asyncio.create_subprocess_exec(  
        "echo", "hello",  
        stdout=asyncio.subprocess.PIPE  
    )  
    out, _ = await proc.communicate()  
    print(out.decode())  
  
asyncio.run(run())
```

---

## 12. `loop.run_in_executor()`

👉 Run blocking code safely

```Python
import asyncio  
  
def blocking():  
    return sum(range(1000000))  
  
async def main():  
    loop = asyncio.get_running_loop()  
    result = await loop.run_in_executor(None, blocking)  
    print(result)  
  
asyncio.run(main())
```

---

## 🧠 Quick Memory Trick

If you remember only these, you're good:

- `run()` → start program
- `async/await` → define + pause
- `sleep()` → delay
- `gather()` → run many
- `create_task()` → background
- `wait_for()` → timeout
