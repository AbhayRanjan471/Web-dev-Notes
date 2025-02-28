# React Hooks
# 1. Use Context hook
# useContext Hook in React (Beginner-Friendly Explanation)

## 🏡 Imagine you have a big house

Imagine you have a **big house** with many rooms, and each room needs access to **WiFi**. Instead of giving each room its own **WiFi router**, you set up **one central router** in the house, and all rooms can use it without extra setup.

In React, `useContext` works like the **central WiFi router**—it provides data to many components **without passing it manually** through each level.

---

## 📌 Problem Without `useContext` (Prop Drilling)

Let’s say we have a **grandparent component**, a **parent component**, and a **child component**. The child component needs to access **user data** from the grandparent.

### ❌ Without `useContext` (Using Props)

We have to **pass data through every component manually**:

```jsx
import React from "react";

const Grandparent = () => {
  const user = "John Doe"; // User data

  return <Parent user={user} />;
};

const Parent = ({ user }) => {
  return <Child user={user} />;
};

const Child = ({ user }) => {
  return <h1>Hello, {user}!</h1>;
};

export default Grandparent;
```

### ⛔ Why is this a problem?

✅ If the app grows and has **many nested components**, passing props becomes **messy**.
✅ If we need to change the **user data structure**, we must **update all components** that pass the data.

---

## ✔ Solution: `useContext` (Avoid Prop Drilling)

We can use **React Context API** to **provide** the user data globally so any component can access it **directly**.

---

### 🔹 Step 1: Create a Context

Think of this as setting up the **WiFi router** (a global data source).

```jsx
import React, { createContext } from "react";

// Create a Context
const UserContext = createContext();
```

---

### 🔹 Step 2: Provide the Data at a Higher Level

The **Grandparent** component will **provide** the data so that any component inside can access it.

```jsx
import React from "react";
import { UserContext } from "./UserContext";
import Parent from "./Parent";

const Grandparent = () => {
  const user = "John Doe"; // Global data

  return (
    <UserContext.Provider value={user}>
      <Parent />
    </UserContext.Provider>
  );
};

export default Grandparent;
```

👆 **Here’s what happens:**
✅ `UserContext.Provider` wraps the components and **shares the user data** with all children inside it.
✅ Now, **any child component** inside `<UserContext.Provider>` can access `user` **without prop drilling**.

---

### 🔹 Step 3: Use `useContext` to Access the Data

Now, the **child component** can **directly access** the user data without needing to receive it as a prop!

```jsx
import React, { useContext } from "react";
import { UserContext } from "./UserContext";

const Child = () => {
  const user = useContext(UserContext); // Access data

  return <h1>Hello, {user}!</h1>;
};

export default Child;
```

---

### 🔹 Step 4: Parent Component (Does Nothing Now!)

Since **we don’t need to pass the user data manually**, the **parent component remains simple**:

```jsx
import React from "react";
import Child from "./Child";

const Parent = () => {
  return <Child />;
};

export default Parent;
```

---

## 🎯 Final Code: Using `useContext` (Complete Solution)

```jsx
// UserContext.js (Create Context)
import { createContext } from "react";
export const UserContext = createContext();

// Grandparent.js (Provide Data)
import React from "react";
import { UserContext } from "./UserContext";
import Parent from "./Parent";

const Grandparent = () => {
  const user = "John Doe"; // Data

  return (
    <UserContext.Provider value={user}>
      <Parent />
    </UserContext.Provider>
  );
};

export default Grandparent;

// Parent.js (No Need to Pass Props)
import React from "react";
import Child from "./Child";

const Parent = () => {
  return <Child />;
};

export default Parent;

// Child.js (Use Data with useContext)
import React, { useContext } from "react";
import { UserContext } from "./UserContext";

const Child = () => {
  const user = useContext(UserContext); // Get data from context

  return <h1>Hello, {user}!</h1>;
};

export default Child;
```

---

## 📌 Summary

✅ **Without `useContext`** → We pass data **manually** through each component (**prop drilling**)
✅ **With `useContext`** → Any component can access the data **directly** (**no prop drilling**)
✅ `useContext` is like **WiFi**—once connected, all components **can use it** without extra setup

---

## 🎯 When to Use `useContext`?

✔ **Global data** (e.g., user authentication, theme, language settings)
✔ **Avoid passing props manually** through multiple components
✔ **Easier state management** for small/medium apps

