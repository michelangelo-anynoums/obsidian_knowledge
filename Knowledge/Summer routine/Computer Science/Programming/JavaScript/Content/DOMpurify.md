### **YouTube lesson:** https://youtu.be/mJ-qvsxPHpY

### DOMPurify in one sentence

DOMPurify is **the most popular and actively maintained client-side HTML sanitizer** that protects against **XSS** by cleaning untrusted HTML, SVG and MathML — fast, tolerant and DOM-based.

### Core purpose

Prevent **Cross-Site Scripting (XSS)** when you need to display HTML that comes from:

- users (comments, forum posts, profiles…)
- external sources (API responses, imported content…)
- WYSIWYG editors (CKEditor, TinyMCE, Quill…)
- Markdown → HTML conversion

### Key characteristics (2026 status)

- Works **only in browser** (DOM-only) → uses browser's own parser
- Extremely fast compared to most other sanitizers
- Very tolerant (allows a lot of "normal" rich content by default)
- Very good security track record (regular updates after bypass discoveries)
- Actively maintained by Cure53 (security company)
- Current major version: **3.x** (supports modern browsers, dropped IE)

### Basic usage

HTML

```JavaScript
<!-- Usually loaded via CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/dompurify/3.1.6/purify.min.js"></script>
<!-- or 3.2.x / 3.3.x depending on latest stable -->
```

JavaScript

```JavaScript
// Most common & recommended pattern
const dirty = `<img src=x onerror=alert(1)> <script>alert("xss")</script>
               <b>bold</b> <a href="javascript:alert(1)">click</a>`;

const clean = DOMPurify.sanitize(dirty);

console.log(clean);
// → ' <b>bold</b> <a>click</a> '   (or very similar)
// removes script, onerror, javascript: urls...
```

JavaScript

```JavaScript
// Insert into page safely
document.getElementById('content').innerHTML = DOMPurify.sanitize(userHtml);

// React / Vue / Svelte / Angular example
<div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(html) }} />
```

### Most important configuration options

JavaScript

```JavaScript
DOMPurify.sanitize(dirty, {
  // Default = very safe
  ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'a', 'p', 'div', 'br'],   // very restrictive
  ALLOWED_ATTR: ['href', 'target', 'rel'],                           // only these attributes

  // Popular balanced preset (rich text + links + images)
  ADD_TAGS: ['img', 'video', 'iframe'],           // extend default allowed tags
  ADD_ATTR: ['target', 'rel', 'class'],           // extend allowed attributes

  // Very common & useful flags
  FORBID_TAGS: ['script', 'style', 'iframe'],     // explicitly block even if default allows
  FORBID_ATTR: ['on*', 'style'],                  // kill all event handlers & inline styles

  ALLOW_DATA_ATTR: false,       // block data-* attributes (default = true)
  ALLOW_UNKNOWN_PROTOCOLS: false, // only http/https/mailto/... (default = false)

  // When displaying user content in <div> → often useful
  RETURN_DOM_FRAGMENT: true,    // returns DocumentFragment instead of string
  RETURN_DOM: true,             // returns DOM element (Document)

  // For very paranoid use-cases
  USE_PROFILES: { svg: false, mathMl: false },   // disable SVG & MathML completely
});
```

### Quick reference — most common safe presets

JavaScript

```JavaScript
// 1. Very strict (almost no tags)
DOMPurify.sanitize(html, { ALLOWED_TAGS: [] });               // → only text

// 2. Basic rich text + safe links
DOMPurify.sanitize(html, {
  ALLOWED_TAGS: ['p','br','b','i','em','strong','a','ul','ol','li'],
  ALLOWED_ATTR: ['href','target','rel']
});

// 3. Modern comment / article style (very popular)
const clean = DOMPurify.sanitize(html, {
  ADD_TAGS: ['img','h1','h2','h3','blockquote','code','pre'],
  ADD_ATTR: ['class','style','alt','title','src','width','height'],
  ALLOW_DATA_ATTR: true,
  ADD_URI_SAFE_ATTR: ['src']   // sometimes needed for data: urls on images
});
```
---

(Current stable version as of February 2026: **3.3.1**)

### How to get DOMPurify into your project

| Method                                                       | Command / Steps                                                                                       | When to use                                           | Notes                              |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------- | ---------------------------------- |
| **npm** (recommended for modern JS projects)                 | npm install dompurify                                                                                 | Vite, React, Vue, Svelte, bundler-based apps          | ESM / CJS support; types included  |
| **yarn / pnpm**                                              | yarn add dompurify or pnpm add dompurify                                                              | Same as above                                         | Same package                       |
| **CDN** (quick testing / no build step)                      | https://cdnjs.cloudflare.com/ajax/libs/dompurify/3.3.1/purify.min.js                                  | Prototypes, simple HTML pages, Obsidian plugins       | Global DOMPurify available         |
| **Git clone** (want latest dev version or to inspect source) | git clone https://github.com/cure53/DOMPurify.git then cd DOMPurify and npm install                   | Contributing, debugging bypasses, very latest commits | Build with npm run build if needed |
| **curl / wget** (manual single-file download)                | curl -O https://raw.githubusercontent.com/cure53/DOMPurify/main/dist/purify.min.js or wget equivalent | Offline setups, embedded scripts, demos               | Always check version / integrity   |

---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[JavaScript introduction]]
