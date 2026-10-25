# Tailwind CSS v4 Cheat Sheet

Only the classes and reusable patterns used in your React login/signup pages.

## 1. Classes You Actually Need

| **Purpose** | **Tailwind class** | **What it does** |
| --- | --- | --- |
| Flex layout | `flex` | Places items in a flex layout |
| Vertical layout | `flex-col` | Stacks items vertically |
| Center items | `items-center` | Centers items on the cross axis |
| Center content | `justify-center` | Centers content on the main axis |
| Space between items | `justify-between` | Pushes items to opposite ends |
| Hide element | `hidden` | Hides an element |
| Show as block | `block` | Displays an element as a block |
| Full width | `w-full` | Uses the available width |
| Half width on large screens | `lg:w-1/2` | Uses half the width at large screens |
| Full screen minimum height | `min-h-screen` | At least the height of the screen |
| Limit width | `max-w-lg` | Limits the element's width |
| Padding | `p-4`, `p-6`, `p-10` | Adds space inside an element |
| Top margin | `mt-3`, `mt-4`, `mt-6`, `mt-8` | Adds space above an element |
| Gap between items | `gap-2`, `gap-4` | Adds space between flex/grid items |
| Text size | `text-base`, `text-lg`, `text-4xl` | Changes text size |
| Font weight | `font-medium`, `font-semibold` | Changes text thickness |
| Text color | `text-white`, `text-gray-500` | Changes text color |
| Background | `bg-white`, `bg-violet-500` | Sets background color |
| Gradient | `bg-linear-to-tr from-green-900 to-green-400` | Creates a diagonal gradient in Tailwind v4 |
| Border | `border`, `border-2`, `border-green-200` | Adds a border |
| Rounded corners | `rounded-xl`, `rounded-3xl` | Rounds corners |
| Image crop | `object-cover` | Fills the image area and crops if needed |
| Responsive prefix | `sm:`, `md:`, `lg:` | Applies a class at that screen size and above |
| Hover style | `hover:text-violet-400` | Changes text color on hover |
| Transition | `transition` | Smooths supported visual changes |
| Hover scale | `hover:scale-105` | Enlarges slightly on hover |
| Focus border | `focus:border-violet-500` | Changes border color when focused |
| Remove outline | `focus:outline-none` | Removes default outline; use an accessible focus style |

**Quick spacing reminder:** in the default spacing scale, `4` is usually `1rem` or `16px`. For example, `p-4` adds 16px padding.

## 2. Reusable Login/Signup Card

```jsx
<div className="w-full max-w-lg rounded-3xl border border-green-200 bg-white p-6 sm:p-10">
  {/* Put your form content here */}
</div>
```

## 3. Heading and Supporting Text

```jsx
<div>
  <h1 className="text-4xl font-semibold">Welcome Back</h1>
  <p className="mt-3 text-lg font-medium text-gray-500">
    Welcome back! Please enter your details.
  </p>
</div>
```

## 4. Reusable Input Field

Change the label, `id`, `type`, and placeholder for each field.

```jsx
<div className="mt-4">
  <label htmlFor="email" className="text-lg font-medium">
    Email
  </label>
  <input
    id="email"
    name="email"
    type="email"
    placeholder="Email Address"
    className="mt-1 w-full rounded-xl border-2 border-gray-100 bg-transparent p-2 focus:border-violet-500 focus:outline-none"
  />
</div>
```

For a password field, change `type="email"` to `type="password"` and update the label and placeholder.

## 5. Primary Button

```jsx
<button
  type="submit"
  className="w-full rounded-xl bg-violet-500 py-2 text-lg font-medium text-white transition hover:scale-105"
>
  Sign In
</button>
```

Use `type="button"` if the button should not submit the form.

## 6. Google Button

Install the icon package once:

```bash
npm install react-icons
```

Then use:

```jsx
import { FcGoogle } from "react-icons/fc";

<button
  type="button"
  className="flex w-full items-center justify-center gap-2 rounded-xl border-2 border-gray-100 py-2 transition hover:scale-105"
>
  <FcGoogle />
  Continue with Google
</button>
```

This is only the button UI. It does not implement Google authentication.

## 7. Login/Signup Switch

Use this inside a component that receives an `onSwitch` prop.

```jsx
<div className="mt-5 flex items-center justify-center">
  <p className="text-base font-medium">Don't have an account?</p>
  <button
    type="button"
    onClick={onSwitch}
    className="ml-2 text-base font-medium text-violet-500 hover:text-violet-400"
  >
    Sign Up
  </button>
</div>
```

## 8. Form Spacing

```jsx
<form className="mt-8">
  {/* Input fields, each using mt-4 */}

  <div className="mt-6 flex flex-col gap-y-4">
    {/* Submit and secondary buttons */}
  </div>
</form>
```

## 9. Page Layout with Gradient and Side Image

Use this in `App.jsx`. Put your image at `public/logo.jpg`.

```jsx
import Login from "./components/Login";

export default function App() {
  return (
    <div className="flex min-h-screen w-full bg-linear-to-tr from-green-900 to-green-400">
      <main className="flex w-full items-center justify-center p-4 lg:w-1/2">
        <Login />
      </main>

      <aside className="hidden h-screen w-1/2 p-4 lg:block">
        <img
          src="/logo.jpg"
          alt="Page illustration"
          className="h-full w-full rounded-3xl object-cover"
        />
      </aside>
    </div>
  );
}
```

To show signup instead, import `Signup` and replace `<Login />` with `<Signup />`.

## 10. Remember These Patterns

| **Goal** | **Classes** |
| --- | --- |
| Center content | `flex items-center justify-center` |
| Card | `w-full max-w-lg rounded-3xl bg-white p-6 sm:p-10` |
| Stack buttons vertically | `flex flex-col gap-y-4` |
| Put icon and text side by side | `flex items-center gap-2` |
| Hide image on mobile, show on large screens | `hidden lg:block` |
| Responsive padding | `p-6 sm:p-10` |
| Responsive width | `w-full lg:w-1/2` |
| Gradient background | `bg-linear-to-tr from-green-900 to-green-400` |
| Image fills its container | `h-full w-full object-cover` |

That's enough for your current login/signup UI. Add more classes only when a project needs them.
