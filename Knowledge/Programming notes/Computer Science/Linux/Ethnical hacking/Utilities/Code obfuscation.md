# 🔐 Code Obfuscation

> [!abstract] 💡 What is it? Code obfuscation transforms readable source code into a harder-to-understand version without changing its functionality.

## 🌐 Online Obfuscation Tools

|Language|Online service|
|---|---|
|JavaScript|[Obfuscator.io](https://obfuscator.io/)|
|JavaScript|[JS Beautifier / Obfuscator](https://beautifier.io/)|
|HTML / CSS / JS|HTML Minifier|
|Python|[Pyminifier](https://liftoff.github.io/pyminifier/)|

## ⚙️ JavaScript Examples

**1. Original code**

```javascript
function calculatePrice(price) {
    const tax = 0.21;
    return price * (1 + tax);
}

console.log(calculatePrice(100));
```

**2. Obfuscated code**

```javascript
var _0x4a2f = ['log'];
(function(_0x1a2b, _0x3c4d) {
    var _0x5e6f = function(_0x7a8b) {
        while (--_0x7a8b) {
            _0x1a2b.push(_0x1a2b.shift());
        }
    };
    _0x5e6f(++_0x3c4d);
})(_0x4a2f, 0x1);

function _0xabc1(_0x1234) {
    return _0x1234 * 1.21;
}

console[_0x4a2f[0]](_0xabc1(100));
```

## 🧩 Common Obfuscation Techniques

|Technique|Purpose|
|---|---|
|Variable renaming|`username` → `_0x12ab`|
|String encoding|`"Hello"` → `"\x48\x65..."`|
|Dead code injection|Adds unnecessary code|
|Control flow flattening|Makes execution logic harder to follow|
|Minification|Removes spaces and shortens code|

## ⚠️ Important

- Obfuscation ≠ encryption.
- It does not prevent reverse engineering.
- Never embed passwords, API secrets or private keys in client-side code.
- Always keep an unobfuscated source-code backup.

> [!tip] 🛡️ Remember Obfuscation increases the effort required to understand code. It does not make code impossible to inspect.

---
