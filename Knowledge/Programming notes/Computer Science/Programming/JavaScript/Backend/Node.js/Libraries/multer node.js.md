# 📁 Multer — File Uploads in Node.js

> [!abstract] 💡 What is Multer? **Multer** is a Node.js middleware used to handle file uploads through `multipart/form-data`.
> 
> It manages file storage, filenames, file size and upload limits.

---

## 📦 1. Installation

```bash
npm install multer
```

## ⚙️ 2. Basic setup

```js
const multer = require("multer");

// Default storage configuration
const upload = multer({
  dest: "uploads/"
});
```

> Files are automatically saved inside the `uploads/` folder.

## 📤 3. Upload a single file

```js
const express = require("express");
const multer = require("multer");

const app = express();
const upload = multer({ dest: "uploads/" });

app.post("/upload", upload.single("image"), (req, res) => {
  console.log(req.file); // Uploaded file

  res.send("File uploaded!");
});
```

**upload.single("image")** → Accepts one file.

HTML form:

```html
<form action="/upload" method="POST" enctype="multipart/form-data">
  <input type="file" name="image" />
  <button type="submit">Upload</button>
</form>
```

## 📂 4. Multiple files

```js
// Multiple files with the same field name
upload.array("images", 5);

// Multiple files with different field names
upload.fields([
  { name: "avatar", maxCount: 1 },
  { name: "gallery", maxCount: 5 }
]);
```

|Method|Purpose|
|---|---|
|`single()`|One file|
|`array()`|Multiple files|
|`fields()`|Different file fields|
|`none()`|No files, only text fields|

## 💾 5. Custom storage

Use `diskStorage()` to control where files are saved and how they are named.

```js
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, "uploads/");
  },

  filename: (req, file, cb) => {
    cb(null, Date.now() + "-" + file.originalname);
  }
});

const upload = multer({ storage });
```

- `destination` → Folder where files are stored.
- `filename` → Name assigned to the uploaded file.
- `cb` → Callback used to return the result.

## 🛡️ 6. File size and type limits

```js
const upload = multer({
  storage,

  limits: {
    fileSize: 2 * 1024 * 1024 // 2 MB
  },

  fileFilter: (req, file, cb) => {
    if (file.mimetype.startsWith("image/")) {
      cb(null, true);
    } else {
      cb(new Error("Only images are allowed!"));
    }
  }
});
```

- `limits` → Restricts upload size.
- `fileFilter` → Controls which files are accepted.
- `mimetype` → Indicates the uploaded file's declared media type.

> ⚠️ MIME types alone are not reliable security validation. Validate file contents and use safe filenames.

## 🔍 7. Access uploaded data

Inside your route:

```js
req.file   // Single uploaded file
req.files  // Multiple uploaded files
req.body   // Text fields from the form
```

Useful `req.file` properties:

```js
req.file.originalname
req.file.filename
req.file.mimetype
req.file.size
req.file.path
```

## 🧠 Remember

- 📤 `single()` → One file.
- 📂 `array()` → Multiple files.
- 💾 `diskStorage()` → Custom file storage.
- 🛡️ `limits` → Upload restrictions.
- 🔍 `fileFilter` → File acceptance rules.
- 📦 `req.file` → Uploaded file information.

**Multer = Express middleware for handling file uploads.**

---
