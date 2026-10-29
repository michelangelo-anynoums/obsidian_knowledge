# 🎨 CSS `@property`

> [!abstract] 💡 What is it? `@property` lets you **register custom CSS properties** (`--variables`) with a type, an initial value, and inheritance behavior.
> 
> ✨ Especially useful for animating CSS variables smoothly.

## 🧩 Basic syntax

```css
@property --progress {
  syntax: "<number>";
  inherits: false;
  initial-value: 0;
}
```

- `syntax` → defines the expected value type.
- `inherits` → controls inheritance from the parent.
- `initial-value` → defines the default value.

## 🎨 Example: Animated color

```css
@property --color {
  syntax: "<color>";
  inherits: false;
  initial-value: red;
}

.box {
  background: var(--color);
  transition: --color 1s;
}

.box:hover {
  --color: blue;
}
```

✨ The background color transitions smoothly because `--color` is registered as a `<color>`.

## 📏 Common syntax types

```css
@property --size {
  syntax: "<length>";
  inherits: false;
  initial-value: 20px;
}

@property --angle {
  syntax: "<angle>";
  inherits: false;
  initial-value: 0deg;
}

@property --opacity {
  syntax: "<number>";
  inherits: false;
  initial-value: 1;
}
```

Other useful types include `<percentage>`, `<length-percentage>`, and `<integer>`.

## ⚡ Example: Rotating element

```css
@property --rotation {
  syntax: "<angle>";
  inherits: false;
  initial-value: 0deg;
}

.box {
  transform: rotate(var(--rotation));
  transition: --rotation 1s;
}

.box:hover {
  --rotation: 180deg;
}
```

## 🆚 Regular variables vs. `@property`

|Regular `--variable`|Registered `@property`|
|---|---|
|Accepts almost any token sequence|Has a declared syntax|
|Usually cannot interpolate smoothly|Can animate compatible typed values|
|Inherits by default|Inheritance is configurable|
|No registered initial value|Can define an initial value|

## ⚠️ Important

- `syntax` must match the values you intend to use.
- For non-universal syntax types, `initial-value` must be computationally independent.
- `inherits: false` prevents the property from inheriting from its parent.
- Register a property only once per intended definition.

---
