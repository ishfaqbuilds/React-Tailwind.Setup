# React + Vite + Tailwind CSS v4 Setup

Reusable setup guide for macOS and Windows using VS Code.

## Stack and documentation

- React: reusable UI components
- Vite: project setup and development server
- Tailwind CSS v4: utility-first styling
- Node.js and npm: run tools and install packages
- Lucide React: optional icons

Official guides: [Node.js](https://nodejs.org/en/download) · [Vite](https://vite.dev/guide/) · [Tailwind CSS v4 with Vite](https://tailwindcss.com/docs/installation/using-vite) · [React](https://react.dev/) · [Lucide React](https://lucide.dev/guide/packages/lucide-react)

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

1. Create an empty folder named `my-frontend-project`.
2. Open that folder in VS Code: **File → Open Folder**.
3. Open the VS Code terminal and run:

```bash
npm create vite@latest . -- --template react
```

Choose ESLint if prompted. If asked to install dependencies and start the server, choose **Yes**. Otherwise run:

```bash
npm install
npm run dev
```

The `.` means Vite creates the project inside the folder you already opened.

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

Replace all contents of `src/index.css` with:

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

## 4. Create component folders and files

Run the command for your terminal from the project root.

**macOS / Linux / Git Bash:**

```bash
mkdir -p src/components src/assets
touch src/components/{Navbar,Hero,Features,Pricing,Testimonials,Footer}.jsx
```

**Windows PowerShell:**

```powershell
New-Item -ItemType Directory -Force src/components, src/assets
'Navbar','Hero','Features','Pricing','Testimonials','Footer' | ForEach-Object { New-Item -ItemType File -Force "src/components/$_.jsx" }
```

These commands create empty component files. Add a React component with a default export to each file before importing it. Create only the components your project needs.

Example `src/components/Footer.jsx`:

```jsx
export default function Footer() {
  return (
    <div>Footer</div>
);
}
```

## 5. Remove unused Vite starter files (optional)

Only run the command for your terminal, and only if you have not added your own code or assets to these files.

**macOS / Linux / Git Bash:**

```bash
rm -f src/App.css src/assets/react.svg public/vite.svg
```

**Windows PowerShell:**

```powershell
Remove-Item src/App.css, src/assets/react.svg, public/vite.svg -ErrorAction SilentlyContinue
```

If `src/App.jsx` imports `./App.css`, remove that import too. Keep `package.json`, `package-lock.json`, `index.html`, `src/main.jsx`, `src/App.jsx`, and `vite.config.js`. Do not delete `node_modules` as part of normal setup.

## 6. Optional: Install Lucide React Icons

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

## 7. Recommended project structure

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

Start the server:

```bash
npm run dev
```

Open the local URL shown in the terminal. Keep the terminal open while working. Stop the server with `Ctrl + C`.

### `src/App.jsx` for a component-based project

Use this version after you have created each component file and each one has a default export.

```jsx
import Navbar from "./components/Navbar";
import Hero from "./components/Hero";
import Features from "./components/Features";
import Pricing from "./components/Pricing";
import Testimonials from "./components/Testimonials";
import Footer from "./components/Footer";

function App() {
  return (
    <div className="min-h-screen bg-slate-950 text-white overflow-hidden">
      <Navbar />
      <Hero />
      <Features />
      <Pricing />
      <Testimonials />
      <Footer />
    </div>
  );
}
export default App;

```

### `src/components/Navbar.jsx`

```jsx
import { Menu, X } from "lucide-react";
import { useState } from "react";
export default function Navbar() {
  const [mobileMenuIsOpen, setMobileMenuIsOpen] = useState(false);
  return (
    <nav className="fixed top-0 w-full z-50 transition-all duration-300 bg-slate-950/20 backdrop-blur-sm">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between items-center h-14 sm:h-16 md:h-20">
          <div className="flex items-center space-x-1 group cursor-pointer">
            <div>
              <img src="/logo.png" alt="IshfaqBuilds" className="w-6 h-6 sm:w-8 sm:h-8" />
            </div>
            <span className="text-lg sm:text-xl md:text-2xl font-medium">
              <span className="text-white">Ishfaq</span>
              <span className="text-blue-400">Builds</span>
            </span>
          </div>

          {/* {Nav Links} */}

          <div className="hidden md:flex items-center space-x-6 lg:space-x-8">
            <a href="#features" className="text-gray-300 hover:text-white text-sm lg:text-base">Features</a>
            <a href="#pricing" className="text-gray-300 hover:text-white text-sm lg:text-base">Pricing</a>
            <a href="#testimonials" className="text-gray-300 hover:text-white text-sm lg:text-base">Testimonials</a>
          </div>

          <button className="md:hidden items-center p-2 text-gray-300 hover:text-white" onClick={() => setMobileMenuIsOpen((prev) => !prev)}>
            {mobileMenuIsOpen ? <X className="w-5 h-5 sm:w-6 sm:h-6" /> : <Menu className="w-5 h-5 sm:w-6 sm:h-6" />}
          </button>
        </div>
      </div>

      {mobileMenuIsOpen && (
        <div className="md:hidden bg-slate-900/95 backdrop-blur-lg border-t border-slate-800 animate-in slide-in-from-top duration-300">
          <div className="px-4 py-4 sm:py-6 space-y-3 sm:space-y-4">
            <a href="#features" onClick={() => setMobileMenuIsOpen(false)} className=" block text-gray-300 hover:text-white text-sm lg:text-base">Features</a>
            <a href="#pricing" onClick={() => setMobileMenuIsOpen(false)} className="block text-gray-300 hover:text-white text-sm lg:text-base">Pricing</a>
            <a href="#testimonials" onClick={() => setMobileMenuIsOpen(false)} className="block text-gray-300 hover:text-white text-sm lg:text-base">Testimonials</a>
          </div>
        </div>
      )}
    </nav>
  );
}
```

This is the reusable Navbar we can use in any project.

### `src/index.css`

```jsx
@import "tailwindcss";

@layer utilities {
  .animate-in {
    animation-fill-mode: both;
  }

  .slide-in-from-top {
    animation-name: slideInFromTop;
  }

  .duration-300 {
    animation-duration: 300ms;
  }
}

@keyframes slideInFromTop {
  from {
    opacity: 0;
    transform: translateY(-1rem);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

```
The index.css has the animation styles we want for the navbar.

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
