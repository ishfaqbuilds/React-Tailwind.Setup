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

In Terminal (macOS) or PowerShell (Windows), run:

```bash
npm create vite@latest my-frontend-project -- --template react
cd my-frontend-project
npm install
```

Replace `my-frontend-project` with your project name. This creates a React project using JavaScript.

Open in VS Code:

```bash
code .
```

If `code .` does not work, open VS Code and select **File → Open Folder**.

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

Create components as you need them. A public image referenced as `/logo.png` belongs at `public/logo.png`.

## 6. Starter templates

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

## 7. Run the development server

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

## 8. Use the project on another computer

After copying or cloning the project:
1. Install Node.js LTS.
2. Open a terminal in the project folder.
3. Run:

```bash
npm install
npm run dev
```

You usually do not need to install React, Vite, or Tailwind globally. `npm install` reads the project's `package.json`.

## 9. Troubleshooting

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
