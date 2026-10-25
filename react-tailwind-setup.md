# React + Vite + Tailwind CSS v4 Setup

Reusable setup guide for macOS and Windows.

## Stack

- HTML and CSS: structure and styling
- JavaScript: programming language
- React: reusable UI components
- Vite: project setup and development server
- Tailwind CSS v4: utility-first styling
- Node.js: runs JavaScript tools locally
- npm: installs packages and runs project scripts
- Lucide React (optional): icons
- VS Code: editor

Official documentation:
- Node.js: https://nodejs.org/en/download
- Vite: https://vite.dev/guide/
- Tailwind v4 with Vite: https://tailwindcss.com/docs/installation/using-vite
- React: https://react.dev/
- Lucide React: https://lucide.dev/guide/packages/lucide-react

## 1. Install Node.js and npm

Node.js is the runtime. npm is the package manager and comes with the Node.js installer.

### macOS

Beginner method:
1. Visit https://nodejs.org/en/download
2. Download the **LTS** macOS installer (`.pkg`).
3. Open it and follow the installer.
4. Reopen Terminal or your VS Code terminal.

If you already use Homebrew, you can instead run:

```bash
brew install node
```

Verify:

```bash
node -v
npm -v
```

Both should print version numbers.

### Windows

Beginner method:
1. Visit https://nodejs.org/en/download
2. Download the **LTS** Windows installer (`.msi`).
3. Run it and follow the installer, keeping the option to add Node to PATH enabled.
4. Reopen PowerShell or your VS Code terminal.

Alternatively, in PowerShell with `winget` installed:

```powershell
winget install OpenJS.NodeJS.LTS
```

Verify:

```powershell
node -v
npm -v
```

Both should print version numbers. If either command is not recognized, restart the terminal and check the installation.

## 2. Create a React project with Vite

Choose either method. Both create the same kind of React project.

### Option A: Let Vite create the project folder

Run these commands from the directory where you want the project folder created:

```bash
npm create vite@latest my-frontend-project -- --template react
cd my-frontend-project
npm install
npm run dev
```

Replace `my-frontend-project` with your preferred project name. When prompted, choose **ESLint** if you want a linter, then choose **Yes** for installing dependencies and starting the dev server. If you choose that option, Vite runs `npm install` and `npm run dev` for you, so you do not need to run those commands again.

To open the project in VS Code, open a second terminal or stop the dev server with **Ctrl + C**, then run this from inside the project folder:

```bash
code .
```

If `code .` does not work, open VS Code and select **File → Open Folder**.

### Option B: Create and open the folder yourself first

1. Create a folder named `my-frontend-project` on your Desktop or wherever you want it.
2. Open that folder in VS Code using **File → Open Folder**.
3. Open the integrated terminal in VS Code. Make sure the terminal is inside `my-frontend-project` and that the folder is empty.
4. Run:

```bash
npm create vite@latest . -- --template react
```

The dot (`.`) tells Vite to scaffold the project in the current folder rather than creating another folder inside it. Choose **ESLint** if prompted. If asked whether to install dependencies and start now, choose **Yes**. Vite will install dependencies and start the dev server automatically. If you choose **No**, run:

```bash
npm install
npm run dev
```

Vite requires a supported recent Node.js version. If Vite reports that Node is too old, install the current LTS version from nodejs.org.

## 3. Install Tailwind CSS v4

From inside the project folder:

```bash
npm install tailwindcss @tailwindcss/vite
```

Replace `vite.config.js` with:

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

Set `src/index.css` to:

```css
@import "tailwindcss";
```

Make sure `src/main.jsx` imports the CSS:

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

For a basic Tailwind v4 setup, you do not need the old v3 directives (`@tailwind base`, `@tailwind components`, `@tailwind utilities`) or a `tailwind.config.js` file.

## 4. Optional: install Lucide React

```bash
npm install lucide-react
```

Example:

```jsx
import { Menu, X, Search } from 'lucide-react'

export default function IconExample() {
  return (
    <div className="flex gap-4">
      <Menu size={24} />
      <X size={24} />
      <Search size={24} />
    </div>
  )
}
```

Browse icons: https://lucide.dev/icons/

## 5. Recommended project structure

```text
my-frontend-project/
├── public/
│   └── logo.png
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── Hero.jsx
│   │   ├── Features.jsx
│   │   ├── Pricing.jsx
│   │   ├── Testimonials.jsx
│   │   └── Footer.jsx
│   ├── App.jsx
│   ├── index.css
│   └── main.jsx
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

Create components as you need them. Vite does not create a `components` folder automatically. From the project root, create the folders with:

```bash
mkdir -p src/components src/assets
```

This command works in the macOS/Linux terminal and the VS Code terminal using a Unix-like shell. In Windows PowerShell, use:

```powershell
New-Item -ItemType Directory -Force src/components, src/assets
```

A public image referenced as `/logo.png` belongs at `public/logo.png`.

## 6. What can I remove from the default Vite files?

You do not need to delete the starter files to begin. You can replace the contents of the files listed below with the examples in this guide.

### Safe to replace or remove if unused

- `src/App.jsx`: **Replace its contents** with the `App.jsx` starter below.
- `src/index.css`: **Replace its contents** with `@import "tailwindcss";` as shown above. This removes the default starter styles.
- `src/App.css`: You can delete this if `App.jsx` no longer imports it.
- `src/assets/react.svg`: You can delete this if you are not using the React logo.
- `public/vite.svg`: You can delete this if you are not using the Vite logo.

### Keep these files

- `package.json`: required for project scripts and dependency information.
- `package-lock.json`: keep it to preserve the dependency versions installed by npm.
- `index.html`: Vite uses this as the HTML entry point.
- `src/main.jsx`: keep it, and make sure it imports `./index.css` and `./App.jsx` as shown above.
- `vite.config.js`: keep it and update it with the Tailwind v4 configuration shown above.
- `node_modules/`: do not manually edit it. It contains installed packages and can be recreated with `npm install`.

Do not delete a file just because it is not listed here. If you are unsure whether a file is used, search for its name in your imports first.

## 7. Starter templates

### Minimal `src/App.jsx` to test the setup

Use this first. It does not depend on other component files.

```jsx
export default function App() {
  return (
    <main className="min-h-screen bg-slate-950 p-8 text-white">
      <h1 className="text-3xl font-bold text-blue-400">
        React + Tailwind is ready!
      </h1>
      <p className="mt-4 text-slate-300">
        Start building your next project.
      </p>
    </main>
  )
}
```

### `src/App.jsx` for a component-based project

Use this version after you have created each component file and each one has a default export.

```jsx
import Navbar from './components/Navbar'
import Hero from './components/Hero'
import Features from './components/Features'
import Pricing from './components/Pricing'
import Testimonials from './components/Testimonials'
import Footer from './components/Footer'

export default function App() {
  return (
    <>
      <Navbar />
      <main className="pt-20">
        <Hero />
        <Features />
        <Pricing />
        <Testimonials />
      </main>
      <Footer />
    </>
  )
}
```

### `src/components/Navbar.jsx`

```jsx
import { Menu } from 'lucide-react'

export default function Navbar() {
  return (
    <nav className="fixed top-0 z-50 w-full bg-slate-950/90 text-white backdrop-blur-sm">
      <div className="mx-auto flex h-16 max-w-7xl items-center justify-between px-4 sm:px-6 lg:px-8">
        <a href="/" className="text-xl font-semibold">
          Your<span className="text-blue-400">Brand</span>
        </a>

        <div className="hidden items-center gap-6 md:flex">
          <a href="#features" className="text-slate-300 hover:text-white">Features</a>
          <a href="#pricing" className="text-slate-300 hover:text-white">Pricing</a>
        </div>

        <button
          type="button"
          aria-label="Open navigation menu"
          className="p-2 text-slate-300 hover:text-white md:hidden"
        >
          <Menu size={24} />
        </button>
      </div>
    </nav>
  )
}
```

This button is only a visual starter. To open a mobile menu, add React state and conditional rendering.

### `src/components/Hero.jsx`

```jsx
export default function Hero() {
  return (
    <section className="px-4 py-24 text-center text-white sm:py-32">
      <p className="mb-4 text-sm font-semibold uppercase tracking-widest text-blue-400">
        Welcome
      </p>
      <h1 className="mx-auto max-w-3xl text-4xl font-bold tracking-tight sm:text-6xl">
        Build something great.
      </h1>
      <p className="mx-auto mt-6 max-w-xl text-slate-300">
        A clean, responsive starting point for your next project.
      </p>
      <a
        href="#features"
        className="mt-8 inline-flex rounded-lg bg-blue-500 px-5 py-3 font-semibold text-white hover:bg-blue-400"
      >
        Get started
      </a>
    </section>
  )
}
```

If you use the component-based `App.jsx`, create `Features.jsx`, `Pricing.jsx`, `Testimonials.jsx`, and `Footer.jsx` too, or remove their imports until needed.

## 8. Run the development server

From the project folder:

```bash
npm run dev
```

Open the local URL Vite prints, usually `http://localhost:5173/`. Keep the terminal open while working. Stop the server with **Ctrl + C**.

Useful commands:

```bash
npm run dev       # Start the development server
npm run build     # Create a production build
npm run preview   # Preview the production build locally
```

## 9. Use the project on another computer

After copying or cloning the project:
1. Install Node.js LTS.
2. Open a terminal in the project folder.
3. Run:

```bash
npm install
npm run dev
```

You usually do not need to install React, Vite, or Tailwind globally. `npm install` reads the project's `package.json`.

## 10. Troubleshooting

- **`npm` not found:** install Node.js LTS, restart the terminal, then run `node -v` and `npm -v`.
- **`Missing script: dev`:** make sure you are in the project folder and `package.json` has a `dev` script.
- **Blank white page:** check the browser console and terminal for errors, especially missing imports or files.
- **Tailwind styles do not work:** check `@import "tailwindcss";` in `src/index.css`, its import in `main.jsx`, and `tailwindcss()` in `vite.config.js`. Restart Vite after changing configuration.
- **Module not found:** install the package or correct the import path and capitalization.
- **Logo missing:** a URL like `/logo.png` usually requires `public/logo.png`.

## Checklist

- [ ] Node.js and npm installed
- [ ] Vite React project created
- [ ] `npm install` completed
- [ ] Tailwind v4 Vite plugin configured
- [ ] `src/index.css` imports Tailwind
- [ ] `src/main.jsx` imports `index.css`
- [ ] `npm run dev` opens the site
- [ ] Optional: Lucide React installed
