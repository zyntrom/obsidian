### **Example (Functional Component):**

```js
function Greeting({ name }) {   
	return <h1>Hello, {name}!</h1>; 
}
```

- `props` are used to pass data from parent to child.
- Components can be **nested** inside each other.

### **1.2 JSX**

- JSX looks like HTML but **is JavaScript**.
- You can embed JS expressions with `{}`.

```js
const name = "Alen"; 
const element = <h1>Hello, {name}</h1>;
```

### **1.3 State**

- State holds **data that can change over time** inside a component.
- Use `useState` hook for functional components.

```js
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

```

---

### **1.4 Props**

- Props are **read-only data** passed from parent to child component.

```js
function Welcome({ user }) {
  return <h2>Welcome, {user}</h2>;
}

<Welcome user="Alen" />

```

---

### **1.5 Event Handling**

- Events are handled using **camelCase** syntax.

```js
<button onClick={() => alert("Clicked!")}>Click me</button>
```
---

### **1.6 Conditional Rendering**

```js
function Status({ isLoggedIn }) {
  return <div>{isLoggedIn ? "Welcome!" : "Please login"}</div>;
}
```

---

### **1.7 Lists & Keys**

```js
const items = ["React", "Vue", "Angular"];
<ul>
  {items.map((item, index) => (
    <li key={index}>{item}</li>
  ))}
</ul>

```

- **Keys** help React track items in lists efficiently.

---

### **1.8 Hooks (most important)**

- `useState` → state
- `useEffect` → side effects (like API calls)
- `useContext` → global data
- `useRef` → DOM references

---

## **2. Usual React Folder Structure**

Here’s a standard React project structure (using `create-react-app` or Vite):

```js
my-app/
│
├── public/
│   ├── index.html      # Main HTML template
│   └── favicon.ico     # App icon
│
├── src/
│   ├── assets/         # Images, fonts, icons, etc.
│   ├── components/     # Reusable components (buttons, cards)
│   ├── pages/          # Page components (Home, About, Dashboard)
│   ├── hooks/          # Custom React hooks
│   ├── context/        # Context API for global state
│   ├── services/       # API calls, axios instances
│   ├── utils/          # Helper functions (formatting, validation)
│   ├── App.jsx         # Main component
│   ├── index.js        # React DOM render
│   └── styles/         # CSS or SCSS files
│
├── package.json         # Project dependencies and scripts
└── README.md            # Project description

```

---

### **3. Why each folder/file exists**

1. **`public/`**
    - Contains **static files** that aren’t processed by React.
    - `index.html` is your **single-page template**. React injects your app here.
2. **`src/`**
    - All your **React code lives here**.
    - Organized into subfolders for maintainability.
3. **`components/`**
    - Small, reusable UI pieces like buttons, headers, forms.
4. **`pages/`**
    - Components representing **full pages**, usually tied to routes.
5. **`hooks/`**
    - Custom hooks to **reuse logic** across components.
6. **`context/`**
    - For React Context API to **share state globally**.
7. **`services/`**
    - For making API calls or interacting with backend.
8. **`utils/`**
    - For utility functions like **date formatting, validation, etc.**
9. **`styles/`**
    - Central place for CSS/SCSS.
10. **`App.jsx`**
    - Root component that contains **routes and main layout**.
11. **`index.js`**
    - Entry point of your app, renders `App.jsx` to the DOM.