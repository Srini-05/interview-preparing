# Frontend - React

## Short Forms
- DOM: Document Object Model
- BOM: Browser Object Model
- HTML: HyperText Markup Language
- CSS: Cascading Style Sheets
- JS: JavaScript
- JSON: JavaScript Object Notation
- AJAX: Asynchronous JavaScript And XML
- SPA: Single Page Application
- UI: User Interface
- UX: User Experience

**Interview Tip:** Know these acronyms as they are fundamental to web development.

## Hooks

Hooks allow functional components to use state and lifecycle features.

### useState
Used to manage component state.

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

Additional Example: Managing form input
```javascript
const [name, setName] = useState("");
return <input value={name} onChange={(e) => setName(e.target.value)} />;
```

### useEffect
Handles side effects like API calls.

```javascript
useEffect(() => {
  console.log("Component mounted");
}, []);
```

Runs when: component mounts, dependencies change.

Additional Example: Fetching data
```javascript
useEffect(() => {
  fetch('/api/data').then(res => res.json()).then(setData);
}, []);
```

### useContext
Access global data without prop drilling.

```javascript
const value = useContext(MyContext);
```

Example:
```javascript
const ThemeContext = React.createContext();
function Component() {
  const theme = useContext(ThemeContext);
  return <div style={{ color: theme.color }}>Hello</div>;
}
```

### useRef
Access DOM elements directly.

```javascript
const inputRef = useRef();
```

Example:
```javascript
<input ref={inputRef} />
useEffect(() => inputRef.current.focus(), []);
```

### useMemo / useCallback
Performance optimization.

Example useMemo:
```javascript
const expensiveValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

Example useCallback:
```javascript
const handleClick = useCallback(() => { console.log('Clicked'); }, []);
```

**Interview Tip:** useState for state, useEffect for side effects, useContext for global state, useRef for DOM access, useMemo/useCallback for optimization.

## State Management

State management controls how data flows through an application.

### Local State
Managed inside a component using useState.

```javascript
const [name, setName] = useState("");
```

### Global State
Used when many components share data.
Popular tools: Redux, Zustand, Recoil, React Context API

Example (Context):
```javascript
const ThemeContext = React.createContext();
```

Additional Example with useReducer:
```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

**Interview Tip:** Local state for component-specific data, global for app-wide. Context for simple cases, Redux for complex.

## API Integration

Frontend applications often fetch data from servers.

### Fetch API
```javascript
fetch("https://api.example.com/users")
  .then(res => res.json())
  .then(data => console.log(data));
```

### Axios
Popular HTTP client.

```javascript
import axios from "axios";

axios.get("/api/users")
  .then(response => console.log(response.data));
```

### API Call with useEffect
```javascript
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("/api/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return <div>{users.length} users</div>;
}
```

Additional Example: Error handling
```javascript
const [error, setError] = useState(null);
useEffect(() => {
  fetch("/api/users")
    .then(res => {
      if (!res.ok) throw new Error('Failed to fetch');
      return res.json();
    })
    .then(setUsers)
    .catch(setError);
}, []);
```

**Interview Tip:** Handle loading states, errors, and cleanup in useEffect.

## Quick Summary
- Concept: React Lifecycle - Component creation, update, removal
- Concept: Hooks - Use state & lifecycle in functional components
- Concept: State Management - Manage application data
- Concept: API Integration - Fetch data from backend

**Interview Tip:** React is component-based. Hooks replaced class lifecycle methods.

## Axios vs Fetch

Axios is a third-party HTTP client library while Fetch is a built-in browser API. Axios provides automatic JSON parsing, better error handling, interceptors, and simpler syntax, while Fetch requires more manual configuration but does not require installing any library.

Example Axios:
```javascript
axios.get('/api/users').then(res => console.log(res.data));
```

Example Fetch:
```javascript
fetch('/api/users').then(res => res.json()).then(console.log);
```

**Interview Tip:** Axios for simplicity, Fetch for no dependencies.

## State vs Props

State is mutable data managed inside a component, while props are read-only data passed from a parent component to a child component.

### State
- Definition: State is an internal data structure that a component manages. It holds information that can change over time, often due to user interactions.
- Usage: State is used for data that needs to be tracked within a component and can change over time.
- Mutability: State can be updated using setState() method, causing the component to re-render.

### Props
- Definition: Props (short for "properties") are read-only attributes passed from a parent component to a child component.
- Usage: Props are used to pass data and event handlers down to child components from parent components.
- Mutability: Props are immutable within the child component; the child cannot modify the props it receives.

Example:
```javascript
function Parent() {
  const [message, setMessage] = useState("Hello");
  return <Child text={message} onUpdate={setMessage} />;
}

function Child({ text, onUpdate }) {
  return <button onClick={() => onUpdate("Updated")}>{text}</button>;
}
```

**Interview Tip:** Props flow down, state flows up. Use props for parent-child communication.

## Component Architecture

Learn how to structure large React apps.

Topics:
- Reusable components
- Container vs presentational components
- Folder structure
- Props drilling vs composition

Example structure:
```
src
 ├ components
 ├ pages
 ├ hooks
 ├ services
 ├ utils
```

Example Reusable Component:
```javascript
function Button({ children, onClick, variant = 'primary' }) {
  return <button className={`btn-${variant}`} onClick={onClick}>{children}</button>;
}
```

**Interview Tip:** Break UI into small, reusable components. Use composition over inheritance.

## Routing

Frontend apps need navigation between pages.

Learn React Router.

Example:
```javascript
import { BrowserRouter, Routes, Route } from "react-router-dom";

<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/users" element={<Users />} />
  </Routes>
</BrowserRouter>
```

Additional Example: Protected Route
```javascript
<Route path="/admin" element={<ProtectedRoute><Admin /></ProtectedRoute>} />
```

**Interview Tip:** Use Link for navigation, useParams for dynamic routes.

## Form Handling

Forms are everywhere in applications.

Learn: controlled components, validation, form libraries.

Popular library: React Hook Form.

Example Controlled Component:
```javascript
const [email, setEmail] = useState("");
return <input value={email} onChange={(e) => setEmail(e.target.value)} />;
```

Example React Hook Form:
```javascript
import { useForm } from 'react-hook-form';

function Form() {
  const { register, handleSubmit } = useForm();
  const onSubmit = data => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('email')} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

**Interview Tip:** Controlled components for full control, libraries for complex forms.

## Authentication

Login and secure pages.

Concepts: JWT tokens, login/logout, protected routes, storing tokens (localStorage / cookies).

Example Protected Route:
```javascript
function ProtectedRoute({ children }) {
  const token = localStorage.getItem('token');
  return token ? children : <Navigate to="/login" />;
}
```

**Interview Tip:** Store tokens securely, handle token expiry.

## Performance Optimization

Important for real-world apps.

Learn: useMemo, useCallback, React.memo, lazy loading, code splitting.

Example React.memo:
```javascript
const MemoizedComponent = React.memo(function Component({ prop }) {
  return <div>{prop}</div>;
});
```

Example Lazy Loading:
```javascript
const LazyComponent = lazy(() => import('./Component'));
<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>
```

**Interview Tip:** Memoize expensive computations, lazy load routes.

## Advanced State Management

Beyond basic state.

Libraries: Redux Toolkit, Zustand, React Context API.

Example Redux:
```javascript
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: 0,
  reducers: {
    increment: state => state + 1,
  },
});
```

**Interview Tip:** Redux for predictable state, Context for simple global state.

## API Architecture

Instead of calling APIs everywhere.

Create API service layers using: Axios, custom hooks, caching libraries.

Advanced tools: TanStack Query.

Example Custom Hook:
```javascript
function useUsers() {
  const [users, setUsers] = useState([]);
  useEffect(() => {
    axios.get('/api/users').then(res => setUsers(res.data));
  }, []);
  return users;
}
```

**Interview Tip:** Abstract API calls into services or hooks.

## Testing

Companies expect frontend testing.

Learn: Jest, React Testing Library.

Example Test:
```javascript
import { render, screen } from '@testing-library/react';
import Button from './Button';

test('renders button', () => {
  render(<Button>Click me</Button>);
  expect(screen.getByText('Click me')).toBeInTheDocument();
});
```

**Interview Tip:** Test user interactions, not implementation details.