# 🗂️ Node.js — `readline`

> 💡 The `readline` module allows us to read input line by line, especially from the terminal (CLI).

## 1. Import readline


```js
import readline from 'node:readline'
import { stdin, stdout } from 'node:process'
```

## 2. Create an interface

Connect the terminal input (`stdin`) and output (`stdout`).

```js
const rl = readline.createInterface({
  input: stdin,
  output: stdout
})
```

## 3. Ask for user input

Use `.question()` to display a question and receive an answer.

```js
rl.question('What is your name? ', (name) => {
  console.log(`Hello, ${name}!`)
  rl.close()
})
```

## 4. Read multiple lines

Use the `line` event to listen for input.

```js
rl.on('line', (input) => {
  console.log(`You entered: ${input}`)
})
```

Close the interface with:

```js
rl.close()
```

## 💡 Useful methods

|Method|Purpose|
|---|---|
|`createInterface()`|Creates the input interface|
|`question()`|Asks the user a question|
|`on('line')`|Listens for each input line|
|`close()`|Closes the interface|

## 🚀 Complete example

```js
import readline from 'node:readline'

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
})

rl.question('Enter your age: ', (age) => {
  console.log(`You are ${age} years old.`)
  rl.close()
})
```

Run it:

```bash
node index.js
```

---
