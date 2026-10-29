# 🔒 Node.js — Crypto

> [!abstract] 🎯 Goal Learn how Node.js protects data using hashing, passwords, random values, and encryption.

`crypto` is a built-in Node.js module. You don't need to install it.


```js
import crypto from "node:crypto";
```

## 🧠 1. The 3 Main Concepts

### Hashing

Transforms data into a fixed-length result.

```bash
"hello" → "2cf24dba..."
```

- One-way: you cannot directly recover the original text.
- The same input produces the same hash with the same algorithm.
- Used for checking data and creating fingerprints.

### 🔐 Encryption

Hides data so it can be recovered using the correct key.


```bash
"my secret" → "x8F2k..." → "my secret"
                 🔑
```

- Reversible with the correct key and encryption settings.
- Used to protect sensitive information.

### 🎲 Random values

Generate unpredictable values for security purposes.

```bash
Generate → "a81f93..."
```

- Used for temporary tokens and cryptographic keys.
- Security-sensitive values must be generated with secure randomness.

---

##  2. `createHash()` — Hash Data

Creates a hash using a chosen algorithm.

```bash
const hash = crypto
  .createHash("sha256")
  .update("hello")
  .digest("hex");

console.log(hash);
```

### 🔍 Understand every method

> [!important] **createHash("sha256")**
> Chooses SHA-256, a hashing algorithm.

> [!important] **.update("hello")**
> Provides the data you want to hash.

> [!important]  **.digest("hex")**
> Finishes the hash and returns it as hexadecimal text.

Hexadecimal uses `0–9` and `a–f` to represent bytes.

### 🧪 Example

```js
crypto.createHash("sha256").update("hello").digest("hex");
crypto.createHash("sha256").update("hello").digest("hex");
// Same result
```

Changing the input produces a different hash.

📌 **Use it for:** file checksums and data fingerprints.

> [!question] Don't use ordinary SHA-256 alone for passwords.

---

## 🔑 3. Passwords — `scrypt()`

A password should never be stored as plain text.

❌ Bad database record:


```js
{ username: "alex", password: "mypassword123" }
```

✅ Better idea:

```js
{ username: "alex", salt: "...", hash: "..." }
```

The database stores a password hash instead of the original password.

### 🧂 What is a salt?

> [!important] A salt is random data added to the password-hashing process.
Two users can have the same password but different salts and therefore different stored hashes.

### 🛠️ Create a password hash

```js
import { scrypt, randomBytes } from "node:crypto";
import { promisify } from "node:util";

const scryptAsync = promisify(scrypt);

async function hashPassword(password) {
  const salt = randomBytes(16).toString("hex");

  const result = await scryptAsync(password, salt, 64);

  return {
    salt,
    hash: result.toString("hex"),
  };
}

const savedPassword = await hashPassword("hello123");

console.log(savedPassword);
```

### 🔍 Understand the methods

- `randomBytes(16)` → Generates 16 secure random bytes.
- `.toString("hex")` → Converts bytes into readable hexadecimal text.
- `scrypt(password, salt, 64)` → Derives a 64-byte value from the password and salt.
- `await` → Waits for the asynchronous operation to finish.
- `promisify()` → Converts the callback-based `scrypt()` API into one that works with `await`.
- `async` → Allows a function to use `await`.
- `return` → Gives the generated salt and hash back to the caller.

### 🧩 What is a `Buffer`?

> [!important] A `Buffer` is a Node.js object that stores raw bytes — the numeric data computers use to represent text, files, and cryptographic results.

For example:

```js
const bytes = Buffer.from("hello");

console.log(bytes.toString("hex"));
```

- `Buffer.from("hello")` → Converts text into bytes.
- `.toString("hex")` → Converts those bytes into hexadecimal text.

In the password example, `scrypt()` returns a `Buffer`. We convert it to hexadecimal so it can easily be stored as text.

### ✅ Verify a password

When a user logs in, hash their submitted password using the **original salt** and compare the result with the stored hash.

```js
import { timingSafeEqual } from "node:crypto";

async function verifyPassword(password, saved) {
  const result = await scryptAsync(password, saved.salt, 64);

  const expected = Buffer.from(saved.hash, "hex");

  return (
    result.length === expected.length &&
    timingSafeEqual(result, expected)
  );
}

console.log(await verifyPassword("hello123", savedPassword));
// true

console.log(await verifyPassword("wrong", savedPassword));
// false
```

**timingSafeEqual()** compares two equal-length byte sequences in a way designed to reduce timing leaks.

> [!important] **Remember:** store the salt and hash, never the original password. Use a maintained password-hashing library or carefully configured `scrypt` implementation in real applications.

---

## 🎲 4. `randomBytes()` — Secure Random Data

Generates cryptographically secure random bytes.

```js
const token = crypto.randomBytes(32).toString("hex");

console.log(token);
```

### 🔍 Understand the method

- `randomBytes(32)` → Generates 32 random bytes.
- `.toString("hex")` → Converts them into 64 hexadecimal characters.

Why 64 characters? Each byte becomes two hexadecimal characters.

### 🔐 Example: Reset token

```js
const resetToken = crypto.randomBytes(32).toString("hex");
```

This token could be included in a password-reset link.

> [!important] The server should store a hash of the token, set an expiration time, and allow it to be used only once.

> [!question] Never use `Math.random()` for security tokens.

---

## 🆔 5. `randomUUID()` — Generate an ID

Creates a random UUID, a standardized identifier.

```js
const id = crypto.randomUUID();

console.log(id);
// Example: "550e8400-e29b-41d4-a716-446655440000"
```

- `randomUUID()` → Generates a UUID using secure randomness.
- Useful for identifying records, requests, and objects.

📌 A UUID is an identifier, not a password or authorization token.

---

## 🔐 6. `createCipheriv()` — Encrypt Data

Encryption transforms readable data into ciphertext.

> [!important] We'll use **AES-256-GCM**, an encryption method that also helps detect tampering.

### 🔑 Basic example

```js
const key = crypto.randomBytes(32);
const iv = crypto.randomBytes(12);

const cipher = crypto.createCipheriv("aes-256-gcm", key, iv);

let encrypted = cipher.update("hello", "utf8", "hex");
encrypted += cipher.final("hex");

const tag = cipher.getAuthTag();

console.log(encrypted);
```

### 🔍 Understand every part

- `key` → The secret key used for encryption and decryption.
- `randomBytes(32)` → Creates a 32-byte key for AES-256.
- `iv` → Initialization vector; extra data needed by the encryption algorithm.
- `randomBytes(12)` → Creates a 12-byte IV suitable for this AES-GCM example.
- `createCipheriv()` → Creates the encryption object.
- `cipher.update()` → Encrypts the input text.
- `"utf8"` → The format of the original text.
- `"hex"` → The format of the encrypted output.
- `cipher.final()` → Finishes encryption.
- `getAuthTag()` → Retrieves the authentication tag used to detect tampering.

### 🧩 Why use `let`?


```js
let encrypted = cipher.update("hello", "utf8", "hex");
encrypted += cipher.final("hex");
```

`let` allows a variable to be updated. The second line adds the final encrypted output to the first part.

---

## 🔓 7. `createDecipheriv()` — Decrypt Data

Decryption converts ciphertext back into readable text using the same key and the original IV.

```js
const decipher = crypto.createDecipheriv(
  "aes-256-gcm",
  key,
  iv
);

decipher.setAuthTag(tag);

let decrypted = decipher.update(encrypted, "hex", "utf8");
decrypted += decipher.final("utf8");

console.log(decrypted);
// hello
```

### 🔍 Understand the methods

- `createDecipheriv()` → Creates the decryption object.
- `setAuthTag(tag)` → Supplies the tag that verifies authenticity.
- `decipher.update()` → Decrypts the data.
- `decipher.final()` → Finishes decryption and verifies authentication.

If the ciphertext, tag, or key is incorrect, decryption should fail.

---

## ✍️ 8. `createHmac()` — Verify Data

> [!important] HMAC creates a value from a message and a shared secret.

```js
const signature = crypto
  .createHmac("sha256", "my-secret")
  .update("user=123")
  .digest("hex");

console.log(signature);
```

### 🔍 Understand the methods

- `createHmac("sha256", secret)` → Creates a keyed hash.
- `update("user=123")` → Provides the message.
- `digest("hex")` → Produces the final signature as hexadecimal text.

The receiver can calculate the HMAC again using the same secret and compare the result.

📌 Useful for webhook verification and checking message authenticity.

> [!question] HMAC does not encrypt the message. Keep the secret private.

---

## 🧰 9. Quick Method Reference

|Method|What it does|
|---|---|
|`createHash()`|#️⃣ Creates a hash|
|`update()`|📥 Supplies data to a hash, cipher, or HMAC|
|`digest()`|✅ Finalizes a hash or HMAC|
|`scrypt()`|🔑 Derives a password hash|
|`randomBytes()`|🎲 Generates secure random bytes|
|`randomUUID()`|🆔 Generates a UUID|
|`createCipheriv()`|🔒 Creates an encryption object|
|`cipher.final()`|✅ Finishes encryption|
|`getAuthTag()`|🛡️ Gets the encryption authentication tag|
|`createDecipheriv()`|🔓 Creates a decryption object|
|`setAuthTag()`|🛡️ Supplies the authentication tag|
|`decipher.final()`|✅ Finishes and authenticates decryption|
|`createHmac()`|✍️ Creates a keyed hash|
|`timingSafeEqual()`|🔍 Compares equal-length buffers with timing-attack resistance|

---
