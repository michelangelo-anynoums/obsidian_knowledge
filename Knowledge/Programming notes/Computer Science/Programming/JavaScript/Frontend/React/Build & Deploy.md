# ⚛️ React — Build & Deploy

> [!abstract] The idea **Build** your React app to turn your source code into production files. **Deploy** those files so people can access your app on the internet.

## 1. Create a React project

First, install [Node.js](https://nodejs.org/) if you haven't already. Then open your terminal and run:

```bash
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```

Open the local URL shown in your terminal, usually `http://localhost:5173`.

**What just happened?**

- `npm create vite@latest` creates a React project using Vite.
- `cd my-react-app` enters your project folder.
- `npm install` installs the required dependencies.
- `npm run dev` starts a local development server.

## 2. Write a little React

Open `src/App.jsx` and replace its contents with:

```jsx
function App() {
  return (
    <main>
      <h1>Hello, world! 👋</h1>
      <p>My first React application.</p>
    </main>
  );
}

export default App;
```

**Understand it:**

- `App` is a React component.
- `return` describes the UI using JSX.
- `<h1>` and `<p>` are the elements displayed on the page.
- `export default App` lets another file import this component.

Save the file. Vite updates your browser automatically.

## 3. Build for production

When your app is ready, run:

```bash
npm run build
```

Vite creates a `dist/` folder containing the optimized files for deployment.

To preview the production build locally:

```bash
npm run preview
```

> [!tip] Remember `npm run dev` is for development. `npm run build` prepares the app for deployment. You normally deploy the contents generated in `dist/`, not your source files directly.

## 4. Deploy to GitHub Pages

GitHub Pages can host static React apps for free.

### Step 1 — Push your project to GitHub

Create a new repository on GitHub, for example `my-react-app`.

Then, from your project folder:

```bash
git init
git add .
git commit -m "Initial React app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/my-react-app.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

### Step 2 — Configure the base path

For a project hosted at:

`https://YOUR_USERNAME.github.io/my-react-app/`

Vite needs to know that the app lives inside `/my-react-app/`.

Open `vite.config.js` and set the `base` option:

```js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  base: '/my-react-app/',
});
```

**Why?** Without the correct base path, your deployed page may load without its JavaScript or CSS because the browser looks in the wrong location.

If your repository is instead named `YOUR_USERNAME.github.io`, the base path is normally `/`.

### Step 3 — Add automatic deployment

Create this file in your project:

`.github/workflows/deploy.yml`

```yml
name: Deploy React App

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: npm

      - run: npm ci

      - run: npm run build

      - uses: actions/configure-pages@v5

      - uses: actions/upload-pages-artifact@v3
        with:
          path: dist

      - id: deployment
        uses: actions/deploy-pages@v4
```

This workflow automatically installs dependencies, builds your app, and publishes `dist/` whenever you push to `main`.

> [!info] One-time GitHub setup Open your repository → **Settings → Pages** → set the build and deployment source to **GitHub Actions**.

### Step 4 — Deploy!

Commit and push the workflow:

```bash
git add .
git commit -m "Configure GitHub Pages deployment"
git push
```

Go to the **Actions** tab in your GitHub repository. Wait for the deployment workflow to finish successfully.

Your app should then be available at:

`https://YOUR_USERNAME.github.io/my-react-app/`

## 5. Your everyday workflow

Once everything is configured, your normal workflow is simple:

```text
Edit code
   ↓
Test locally: npm run dev
   ↓
Commit and push to GitHub
   ↓
GitHub Actions builds and deploys
   ↓
Your website is updated 🌍
```

For example:

```bash
git add .
git commit -m "Update homepage"
git push
```

You don't need to manually run the build before every push; GitHub Actions does that for you.

## 6. Quick troubleshooting

|Problem|What to check|
|---|---|
|Blank page after deployment|Check `base` in `vite.config.js`.|
|Workflow fails|Inspect the failed step in GitHub Actions.|
|Changes aren't visible|Wait for deployment to finish, then refresh.|
|`npm ci` fails|Check that `package-lock.json` is committed.|
|Refreshing a nested URL gives 404|Check your routing setup; GitHub Pages needs special handling for some client-side routes.|

## 🧠 The essential takeaway

- **React** builds the user interface.
- **Vite** runs and bundles your project.
- **npm** manages packages and scripts.
- **Git** tracks your changes.
- **GitHub** stores your code.
- **GitHub Actions** automates the build and deployment.
- **GitHub Pages** serves your website.

> [!quote] The mental model **Write → Test → Build → Deploy → Share.**
> 
> Learn this cycle once, and you can use it for countless small React projects.

---
