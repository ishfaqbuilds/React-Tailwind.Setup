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

------------------------------------------------------------------------

### 1. Signup Card

``` jsx
<div className="bg-white p-6 sm:p-10 rounded-3xl border border-green-200">
  <h1 className="text-4xl font-semibold">Create an Account</h1>
  <p className="font-medium text-lg text-gray-500 mt-3">
    Create your account to get started.
  </p>
</div>
```

------------------------------------------------------------------------

### 2. Form

``` jsx
<form className="mt-8">
  {/* Form sections go here */}
</form>
```

------------------------------------------------------------------------

### 3. Full Name

``` jsx
<div>
  <label className="text-lg font-medium">Full Name</label>
  <input type="text" placeholder="Full Name"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

------------------------------------------------------------------------

### 4. Email

``` jsx
<div className="mt-4">
  <label className="text-lg font-medium">Email</label>
  <input type="email" placeholder="Email Address"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

------------------------------------------------------------------------

### 5. Password

``` jsx
<div className="mt-4">
  <label className="text-lg font-medium">Password</label>
  <input type="password" placeholder="Create Password"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

------------------------------------------------------------------------

### 6. Confirm Password

``` jsx
<div className="mt-4">
  <label className="text-lg font-medium">Confirm Password</label>
  <input type="password" placeholder="Confirm Password"
    className="w-full border-2 border-gray-100 rounded-xl p-2 mt-1 bg-transparent" />
</div>
```

------------------------------------------------------------------------

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

------------------------------------------------------------------------

### 8. Log In Link

``` jsx
<div className="flex mt-5 justify-center items-center">
  <p className="font-medium text-base">Already have an account?</p>
  <button className="text-violet-500 text-base font-medium ml-2 hover:text-violet-400">
    Log In
  </button>
</div>
```

For switching forms with React state, accept `onSwitch` as a prop and
add `onClick={onSwitch}` to the Log In button.

------------------------------------------------------------------------

### 9. App Layout + Image (App.jsx)

``` jsx
<div className="flex h-screen w-full overflow-hidden bg-linear-to-tr from-green-900 to-green-400">
  <div className="flex w-full items-center justify-center lg:w-1/2">
    <Signup />
  </div>
  <div className="hidden h-full w-1/2 p-4 lg:block">
    <img src="/logo.jpg" alt="Signup illustration" className="h-full w-full rounded-3xl object-cover" />
  </div>
</div>
```
