# ⚛️ Deploying a React App with Vite + GitHub Pages

> 🚀 GitHub Pages allows you to host your Vite + React app for free.

## 1. Install GitHub Pages

```bash
npm install gh-pages --save-dev
```

## 2. Configure Vite

In `vite.config.js`, set the repository name as the base path.

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  base: '/my-project/'
})
```

💡 Replace `my-project` with your GitHub repository name.

## 3. Configure package.json

Add the deployment scripts:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
}
```

- `predeploy` → Builds the app.
- `deploy` → Publishes the `dist` folder.

## 4. Deploy 🚀

Run:

```bash
npm run deploy
```

GitHub Pages will publish your app using the `gh-pages` branch.

## 5. Enable GitHub Pages

1. Open your GitHub repository.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, select:
    - Source: Deploy from a branch.
    - Branch: `gh-pages`.
    - Folder: `/ (root)`.
4. Click **Save**.

## 🌐 Your app URL


```
https://USERNAME.github.io/my-project/
```

Replace `USERNAME` and `my-project` with your GitHub username and repository name.

## 💡 Remember

| Command          | Purpose                 |
| ---------------- | ----------------------- |
| `npm run dev`    | Run locally             |
| `npm run build`  | Create production build |
| `npm run deploy` | Deploy to GitHub Pages  |

⚠️ **Important:** Whenever you make changes, run `npm run deploy` again.

---

✨ **Workflow:**

`Code → Build → Deploy → GitHub Pages → Online!` 🚀

---
