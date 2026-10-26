## Login Page Cheatsheet
This is a reusable template for login page!

### Install Once:

```bash
npm install react-icons
```

### Imports

``` jsx
import { FcGoogle } from "react-icons/fc";
import { FaKey } from "react-icons/fa6";
import { Link } from "react-router";
```

---

### 1. Login Card

``` jsx
<div className="bg-white p-6 sm:p-10 rounded-3xl border border-green-200">
  <h1 className="text-4xl font-semibold">Welcome Back</h1>
  <p className="font-medium text-lg text-gray-500 mt-3"> Welcome back! Please enter your details.</p>
</div>
```

---

### 2. Form

``` jsx
<form className="mt-8">
  {/* Form sections go here */}
</form>
```

---

### 3. Email

``` jsx
<div>
  <label className="text-lg font-medium">Email</label>
  <input type="email" placeholder="Email Address"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

---

### 4. Password

``` jsx
<div className="mt-4">
  <label className="text-lg font-medium">Password</label>
  <input type="password" placeholder="Password"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

---


### 5. Remember Me + Forgot Password

``` jsx
<div className="mt-5 lg:flex justify-between items-center">
  <div>
    <input type="checkbox" id="remember" />
    <label className="ml-2 font-medium text-base">Remember me</label>
  </div>
  <button className="flex items-center gap-1 font-medium text-base text-violet-500 hover:text-violet-400"><FaKey size={15} /> Forget Password?</button>
</div>
```

---


### 6. Sign In + Google

``` jsx
<div className="mt-6 flex flex-col gap-y-4">
  <button className="w-full rounded-xl py-2 text-lg font-medium text-white bg-violet-500 transition hover:scale-105">Sign in</button>
  <button className="w-full rounded-xl py-2 flex items-center justify-center gap-2 border-2 border-gray-100 transition hover:scale-105"><FcGoogle /> Sign in with Google</button>
</div>
```

---


### 7. Sign Up Link

``` jsx
<div className="flex mt-5 justify-center items-center">
  <p className="font-medium text-base">Don't have an account?</p>
  <Link to="/signup" className="text-violet-500 text-base font-medium ml-2 hover:text-violet-400">Sign Up</Link>
</div>
```


## Signup Page Cheatsheet

This is a reusable template for a signup page!

### Install Once

``` bash
npm install react-icons
```

### Imports

``` jsx
import { FcGoogle } from "react-icons/fc";
```

---

### 1. Signup Card

``` jsx
<div className="bg-white p-6 sm:p-10 rounded-3xl border border-green-200">
  <h1 className="text-4xl font-semibold">Create an Account</h1>
  <p className="font-medium text-lg text-gray-500 mt-3">
    Create your account to get started.
  </p>
</div>
```

---

### 2. Form

``` jsx
<form className="mt-8">
  {/* Form sections go here */}
</form>
```

---

### 3. Full Name

``` jsx
<div>
  <label className="text-lg font-medium">Full Name</label>
  <input type="text" placeholder="Full Name"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

---

### 4. Email

``` jsx
<div className="mt-4">
  <label className="text-lg font-medium">Email</label>
  <input type="email" placeholder="Email Address"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

---

### 5. Password

``` jsx
<div className="mt-4">
  <label className="text-lg font-medium">Password</label>
  <input type="password" placeholder="Create Password"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

---

### 6. Confirm Password

``` jsx
<div className="mt-4">
  <label className="text-lg font-medium">Confirm Password</label>
  <input type="password" placeholder="Confirm Password"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

---

### 7. Sign Up + Google

``` jsx
<div className="mt-6 flex flex-col gap-y-4">
  <button className="w-full rounded-xl py-2 text-lg font-medium text-white bg-violet-500 transition hover:scale-105">
    Sign Up
  </button>
  <button className="w-full rounded-xl py-2 flex items-center justify-center gap-2 border-2 border-gray-100 transition hover:scale-105">
    <FcGoogle /> Sign up with Google
  </button>
</div>
```

---

### 8. Log In Link

``` jsx
<div className="flex mt-5 justify-center items-center">
  <p className="font-medium text-base">Already have an account?</p>
  <Link to="/login" className="text-violet-500 text-base font-medium ml-2 hover:text-violet-400">Log In</Link>
</div>
```

---

### 9. App.jsx (Login and SignUp Routing)

``` jsx
import { Routes, Route, Navigate } from "react-router";
import Login from "./components/Login";
import Signup from "./components/Signup";

function App() {
  return (
    <div className="flex min-h-screen w-full bg-linear-to-tr from-green-900 to-green-400">
      
      {/* Login / Signup Section */}
      <div className="flex w-full items-center justify-center p-4 lg:w-1/2">
        <Routes>
          <Route path="/login" element={<Login />} />
          <Route path="/signup" element={<Signup />} />
          <Route path="*" element={<Navigate to="/login" replace />} />
        </Routes>
      </div>

      {/* Image Section */}
      <div className="hidden h-screen w-1/2 p-4 lg:block">
        <img src="/logo.jpg" alt="Login illustration" className="h-full w-full rounded-3xl object-cover"/>
      </div>
    </div>
  );
}
export default App;
```

---

### 10. main.jsx (Login and SignUp Routing)

```jsx

import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { BrowserRouter } from 'react-router'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
)
```
