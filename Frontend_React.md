# Frontend - React

> **Note:** Interview Tips are highlighted in <span style="color: #007acc;">blue</span> for easy identification.
> **Accordion Feature:** Each question can be made collapsible by wrapping in `<details><summary>Question Title</summary> content </details>`.

<details><summary>⚛️ React Interview Preparation Guide</summary>

<details><summary style="font-size: 1.3em; font-weight: bold;">Short Forms</summary>

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

<span style="color: #007acc;">**Interview Tip:**</span> Know these acronyms as they are fundamental to web development.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Hooks</summary>

Hooks allow functional components to use state and lifecycle features that were previously only available in class components. They were introduced in React 16.8 to make functional components more powerful.

### useState - State Management
Manages local component state. Returns a stateful value and a function to update it.

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // [currentState, updateFunction]

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

### Advanced useState Patterns:
```javascript
// Object state
const [user, setUser] = useState({ name: '', email: '' });
const updateName = (name) => setUser(prev => ({ ...prev, name }));

// Array state
const [todos, setTodos] = useState([]);
const addTodo = (text) => setTodos(prev => [...prev, { id: Date.now(), text }]);

// Lazy initial state (for expensive computations)
const [data, setData] = useState(() => expensiveInitialValue());
```

### useEffect - Side Effects
Handles side effects like API calls, subscriptions, DOM manipulation, and cleanup.

```javascript
useEffect(() => {
  // Effect logic runs after every render
  console.log('Component rendered');

  // Cleanup function (optional)
  return () => {
    console.log('Cleanup before next effect or unmount');
  };
}); // No dependency array = runs after every render

useEffect(() => {
  console.log('Only on mount');
}, []); // Empty array = runs only on mount

useEffect(() => {
  console.log('Runs when count changes:', count);
}, [count]); // Runs when count changes
```

### Common useEffect Patterns:
```javascript
// Data fetching
useEffect(() => {
  let isMounted = true;
  fetch('/api/users')
    .then(res => res.json())
    .then(data => {
      if (isMounted) setUsers(data);
    });
  return () => { isMounted = false; }; // Cleanup
}, []);

// Event listeners
useEffect(() => {
  const handleResize = () => setWindowWidth(window.innerWidth);
  window.addEventListener('resize', handleResize);
  return () => window.removeEventListener('resize', handleResize);
}, []);

// Timer
useEffect(() => {
  const timer = setInterval(() => setTime(new Date()), 1000);
  return () => clearInterval(timer);
}, []);
```

### useContext - Global State
Accesses React Context without prop drilling. Context provides a way to share values between components without explicitly passing props.

```javascript
// Create context
const ThemeContext = React.createContext('light');

// Provider component
function App() {
  const [theme, setTheme] = useState('light');
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

// Consumer using useContext
function Toolbar() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
      Toggle Theme: {theme}
    </button>
  );
}
```

### useRef - Direct DOM Access
Creates a mutable ref object that persists across renders. Used for accessing DOM elements directly or storing mutable values.

```javascript
function TextInput() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus(); // Direct DOM access
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

### useMemo - Memoization
Memoizes expensive computations to avoid unnecessary recalculations.

```javascript
function ExpensiveComponent({ numbers }) {
  // Without memoization - recalculates on every render
  const sum = numbers.reduce((acc, num) => acc + num, 0);

  // With memoization - only recalculates when numbers change
  const memoizedSum = useMemo(() => {
    console.log('Calculating sum...');
    return numbers.reduce((acc, num) => acc + num, 0);
  }, [numbers]);

  return <div>Sum: {memoizedSum}</div>;
}
```

### useCallback - Memoized Functions
Returns a memoized callback function that only changes when dependencies change. Prevents unnecessary re-renders of child components.

```javascript
function ParentComponent() {
  const [count, setCount] = useState(0);

  // Without useCallback - new function on every render
  const increment = () => setCount(count + 1);

  // With useCallback - stable function reference
  const memoizedIncrement = useCallback(() => {
    setCount(prev => prev + 1);
  }, []); // No dependencies needed

  return <ChildComponent onIncrement={memoizedIncrement} />;
}

// Child component with React.memo
const ChildComponent = React.memo(({ onIncrement }) => {
  console.log('Child re-rendered');
  return <button onClick={onIncrement}>Increment</button>;
});
```

### Interview Explanation:
"React Hooks revolutionized functional components by enabling state and lifecycle features. useState manages local state with array destructuring returning [value, setter]. useEffect handles side effects with dependency arrays controlling when it runs. useContext eliminates prop drilling for global state. useRef gives direct DOM access or persistent mutable values. useMemo prevents expensive recalculations, useCallback prevents unnecessary child re-renders. I use them to write cleaner, more maintainable functional components."

**Interview Tip:** useState for state, useEffect for side effects, useContext for global state, useRef for DOM access, useMemo/useCallback for optimization. Rules: only call at top level, only in React functions.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">State Management</summary>

State management controls how data flows through a React application. Choosing the right approach depends on application complexity and data sharing needs.

### Local State (useState)
Best for component-specific data that doesn't need to be shared.

```javascript
function TodoItem({ todo }) {
  const [isEditing, setIsEditing] = useState(false);
  const [editText, setEditText] = useState(todo.text);

  const handleEdit = () => {
    setIsEditing(true);
  };

  const handleSave = () => {
    // Update todo logic
    setIsEditing(false);
  };

  return (
    <div>
      {isEditing ? (
        <input
          value={editText}
          onChange={(e) => setEditText(e.target.value)}
          onBlur={handleSave}
        />
      ) : (
        <span onClick={handleEdit}>{todo.text}</span>
      )}
    </div>
  );
}
```

### Lifting State Up
When multiple components need the same state, move it to their common parent.

```javascript
function TodoApp() {
  const [todos, setTodos] = useState([]);

  const addTodo = (text) => {
    setTodos(prev => [...prev, { id: Date.now(), text, completed: false }]);
  };

  const toggleTodo = (id) => {
    setTodos(prev =>
      prev.map(todo =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  return (
    <div>
      <AddTodo onAdd={addTodo} />
      <TodoList todos={todos} onToggle={toggleTodo} />
    </div>
  );
}
```

### React Context API
For global state that needs to be accessed by many components without prop drilling.

```javascript
// Create context
const UserContext = React.createContext();

// Provider component
function UserProvider({ children }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Fetch user data
    fetch('/api/user')
      .then(res => res.json())
      .then(data => {
        setUser(data);
        setLoading(false);
      });
  }, []);

  const login = (credentials) => {
    // Login logic
    return fetch('/api/login', {
      method: 'POST',
      body: JSON.stringify(credentials)
    }).then(res => res.json());
  };

  const logout = () => {
    setUser(null);
    // Clear tokens, etc.
  };

  return (
    <UserContext.Provider value={{ user, loading, login, logout }}>
      {children}
    </UserContext.Provider>
  );
}

// Usage
function Navbar() {
  const { user, logout } = useContext(UserContext);

  return (
    <nav>
      {user ? (
        <div>
          <span>Welcome, {user.name}</span>
          <button onClick={logout}>Logout</button>
        </div>
      ) : (
        <LoginForm />
      )}
    </nav>
  );
}
```

### useReducer for Complex State
When state logic involves multiple sub-values or complex transitions.

```javascript
const initialState = {
  todos: [],
  filter: 'all', // 'all', 'active', 'completed'
  loading: false
};

function todoReducer(state, action) {
  switch (action.type) {
    case 'ADD_TODO':
      return {
        ...state,
        todos: [...state.todos, action.payload]
      };
    case 'TOGGLE_TODO':
      return {
        ...state,
        todos: state.todos.map(todo =>
          todo.id === action.payload
            ? { ...todo, completed: !todo.completed }
            : todo
        )
      };
    case 'SET_FILTER':
      return { ...state, filter: action.payload };
    case 'SET_LOADING':
      return { ...state, loading: action.payload };
    default:
      return state;
  }
}

function TodoApp() {
  const [state, dispatch] = useReducer(todoReducer, initialState);

  const addTodo = (text) => {
    dispatch({ type: 'ADD_TODO', payload: { id: Date.now(), text, completed: false } });
  };

  const filteredTodos = state.todos.filter(todo => {
    if (state.filter === 'active') return !todo.completed;
    if (state.filter === 'completed') return todo.completed;
    return true;
  });

  return (
    <div>
      {state.loading && <div>Loading...</div>}
      <AddTodo onAdd={addTodo} />
      <FilterButtons
        currentFilter={state.filter}
        onFilterChange={(filter) => dispatch({ type: 'SET_FILTER', payload: filter })}
      />
      <TodoList todos={filteredTodos} onToggle={(id) => dispatch({ type: 'TOGGLE_TODO', payload: id })} />
    </div>
  );
}
```

### Interview Explanation:
"State management in React ranges from local useState for component-specific data to global solutions for app-wide state. I start with local state, lift state up when multiple components need it, use Context for theme/user data, and consider Redux/Zustand for complex apps. The key is choosing the right tool: useState for simple cases, useReducer for complex state logic, Context for global data without prop drilling. I always consider performance implications and avoid unnecessary re-renders."

**Interview Tip:** Local state for component-specific data, global for app-wide. Context for simple cases, Redux for complex. Lifting state up when multiple components need same data.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">API Integration</summary>

Frontend applications frequently communicate with backend APIs. Proper API integration involves handling loading states, errors, caching, and user feedback.

### Fetch API (Built-in)
Modern browser API for making HTTP requests. Returns Promises.

```javascript
// Basic GET request
async function fetchUsers() {
  try {
    const response = await fetch('/api/users');
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const users = await response.json();
    return users;
  } catch (error) {
    console.error('Error fetching users:', error);
    throw error;
  }
}

// POST request with JSON body
async function createUser(userData) {
  const response = await fetch('/api/users', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${token}`
    },
    body: JSON.stringify(userData)
  });

  if (!response.ok) {
    throw new Error('Failed to create user');
  }

  return response.json();
}

// File upload
async function uploadFile(file) {
  const formData = new FormData();
  formData.append('file', file);

  const response = await fetch('/api/upload', {
    method: 'POST',
    body: formData
  });

  return response.json();
}
```

### Axios (Third-party Library)
Feature-rich HTTP client with automatic JSON parsing, interceptors, and better error handling.

```javascript
import axios from 'axios';

// Create configured instance
const apiClient = axios.create({
  baseURL: '/api',
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json'
  }
});

// Request interceptor for auth
apiClient.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// Response interceptor for error handling
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // Handle unauthorized
      localStorage.removeItem('token');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

// Usage
const fetchUsers = () => apiClient.get('/users');
const createUser = (userData) => apiClient.post('/users', userData);
const updateUser = (id, userData) => apiClient.put(`/users/${id}`, userData);
const deleteUser = (id) => apiClient.delete(`/users/${id}`);
```

### Custom Hook for API Calls
Encapsulates API logic and state management for reusable components.

```javascript
import { useState, useEffect, useCallback } from 'react';

function useApi(endpoint, options = {}) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const execute = useCallback(async (overrideOptions = {}) => {
    setLoading(true);
    setError(null);

    try {
      const response = await fetch(endpoint, { ...options, ...overrideOptions });
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      const result = await response.json();
      setData(result);
      return result;
    } catch (err) {
      setError(err.message);
      throw err;
    } finally {
      setLoading(false);
    }
  }, [endpoint, options]);

  useEffect(() => {
    if (options.immediate) {
      execute();
    }
  }, [execute, options.immediate]);

  return { data, loading, error, execute, refetch: execute };
}

// Usage
function UsersList() {
  const { data: users, loading, error, refetch } = useApi('/api/users', {
    immediate: true
  });

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;

  return (
    <div>
      <button onClick={refetch}>Refresh</button>
      {users?.map(user => <div key={user.id}>{user.name}</div>)}
    </div>
  );
}
```

### Advanced Patterns
```javascript
// Optimistic updates
function useOptimisticUpdate() {
  const [items, setItems] = useState([]);

  const addItem = async (newItem) => {
    // Optimistically add to UI
    const tempId = Date.now();
    setItems(prev => [...prev, { ...newItem, id: tempId, pending: true }]);

    try {
      const savedItem = await apiClient.post('/items', newItem);
      // Replace with real data
      setItems(prev => prev.map(item =>
        item.id === tempId ? savedItem : item
      ));
    } catch (error) {
      // Revert on error
      setItems(prev => prev.filter(item => item.id !== tempId));
      throw error;
    }
  };

  return { items, addItem };
}

// Infinite scroll with pagination
function useInfiniteScroll(endpoint) {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);
  const [loading, setLoading] = useState(false);

  const loadMore = async () => {
    if (loading || !hasMore) return;

    setLoading(true);
    try {
      const response = await fetch(`${endpoint}?page=${page}&size=20`);
      const newItems = await response.json();

      if (newItems.length === 0) {
        setHasMore(false);
      } else {
        setItems(prev => [...prev, ...newItems]);
        setPage(prev => prev + 1);
      }
    } finally {
      setLoading(false);
    }
  };

  return { items, loadMore, hasMore, loading };
}
```

### Interview Explanation:
"API integration in React involves fetching data, handling loading/error states, and managing side effects. I use custom hooks to encapsulate API logic, ensuring reusability and clean components. For error handling, I implement global error boundaries and user-friendly messages. I prefer Axios for its interceptors and automatic JSON parsing, but Fetch works for simple cases. I always handle loading states to prevent poor UX and implement proper error boundaries for graceful failures."

**Interview Tip:** Handle loading states, errors, and cleanup in useEffect. Use custom hooks for reusable API logic. Consider optimistic updates for better UX.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Quick Summary</summary>

- Concept: React Lifecycle - Component creation, update, removal
- Concept: Hooks - Use state & lifecycle in functional components
- Concept: State Management - Manage application data
- Concept: API Integration - Fetch data from backend

**Interview Tip:** React is component-based. Hooks replaced class lifecycle methods.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Axios vs Fetch</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">State vs Props</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Component Architecture</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Routing</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Form Handling</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Authentication</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Performance Optimization</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Advanced State Management</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">API Architecture</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Testing</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Basic React + Async Interview Questions</summary>

🚀 BASIC REACT + ASYNC INTERVIEW QUESTIONS
1️⃣ What is a Promise?

👉 A Promise is an object that represents the result of an asynchronous operation.
👉 It can be in three states: pending, resolved, or rejected, and helps handle async code cleanly.

2️⃣ What is async/await?

👉 async/await is a modern way to handle asynchronous operations in JavaScript.
👉 It makes code look synchronous and improves readability compared to .then() chaining.

3️⃣ Difference between Promise and async/await?

👉 Both handle asynchronous operations, but async/await provides cleaner and more readable syntax.
👉 Promises use .then() and .catch(), while async/await uses try-catch blocks.

4️⃣ What is React?

👉 React is a JavaScript library used to build user interfaces, especially single-page applications.
👉 It uses a component-based architecture and virtual DOM for efficient updates.

5️⃣ What is a Component?

👉 A component is a reusable piece of UI in React.
👉 It can be a function that returns JSX and helps in building modular applications.

6️⃣ What is useState?

👉 useState is a React hook used to manage state in functional components.
👉 It allows components to store and update dynamic data, triggering re-renders.

7️⃣ What is useEffect?

👉 useEffect is a hook used to perform side effects like API calls or subscriptions.
👉 It runs after render and depends on the dependency array.

8️⃣ What is dependency array?

👉 The dependency array controls when useEffect runs.
👉 If empty, it runs once; if values change, it re-runs based on those dependencies.

9️⃣ What are props?

👉 Props are inputs passed from parent to child components.
👉 They are read-only and help in making components reusable.

🔟 What is state?

👉 State is a built-in object used to store dynamic data in a component.
👉 When state changes, the component re-renders automatically.

1️⃣1️⃣ Props vs State

👉 Props are read-only and passed from parent to child, while state is managed within the component.
👉 State can change over time, but props cannot be modified by the child.

1️⃣2️⃣ What is lifting state up?

👉 Lifting state up means moving state to a common parent component.
👉 This allows multiple child components to share and sync the same data.

1️⃣3️⃣ What is event handling in React?

👉 Event handling is used to respond to user actions like clicks or input.
👉 React uses camelCase syntax like onClick and passes functions as handlers.

1️⃣4️⃣ What is conditional rendering?

👉 Conditional rendering means displaying UI based on certain conditions.
👉 It can be done using ternary operators or logical operators.

1️⃣5️⃣ What is key in React?

👉 Keys are used to uniquely identify elements in a list.
👉 They help React optimize rendering and avoid unnecessary updates.

1️⃣6️⃣ What is Axios?

👉 Axios is a library used to make HTTP requests like GET and POST.
👉 It returns promises and simplifies API handling compared to fetch.

1️⃣7️⃣ What happens when state updates?

👉 When state updates, React re-renders the component.
👉 It compares the virtual DOM and updates only changed parts in the real DOM.

1️⃣8️⃣ What is Virtual DOM?

👉 Virtual DOM is a lightweight copy of the real DOM.
👉 React uses it to improve performance by updating only necessary elements.

1️⃣9️⃣ What is controlled component?

👉 A controlled component is a form element controlled by React state.
👉 The input value is managed using state and updated via onChange.

2️⃣0️⃣ What is useCallback?

👉 useCallback is a hook used to memoize functions.
👉 It prevents unnecessary re-creation of functions and improves performance.

🔥 FINAL INTERVIEW TIP

👉 Speak like this:

"React is component-based and state-driven"

"Async operations handled using Promises or async/await"

"Hooks simplify functional component logic"

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Interview Questions</summary>

<details><summary style="font-size: 1.3em; font-weight: bold;">What is React and why use it?</summary>

**Explanation:** React is a JavaScript library for building user interfaces, focusing on component-based architecture for reusable and maintainable code.

**Example:** A simple React component.
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

**Real-time Example:** Building a dashboard where each widget (like charts, user info) is a reusable React component, making it easy to update and maintain.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Explain the difference between state and props.</summary>

**Explanation:** Props are read-only data passed from parent to child components, while state is mutable data managed within a component that can change over time.

**Example:** Props for static data, state for dynamic.
```javascript
function Counter({ initialCount }) { // initialCount is prop
  const [count, setCount] = useState(initialCount); // count is state
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

**Real-time Example:** In an e-commerce app, product name (prop) is fixed, but quantity in cart (state) changes as user adds/removes items.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">What are React Hooks and give an example of useEffect.</summary>

**Explanation:** Hooks are functions that let you use state and lifecycle features in functional components. useEffect runs side effects after render.

**Example:** Fetching data on component mount.
```javascript
useEffect(() => {
  fetch('/api/users').then(res => res.json()).then(setUsers);
}, []);
```

**Real-time Example:** In a news app, useEffect fetches latest articles when the page loads, updating the UI automatically.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">How does React handle rendering and what is Virtual DOM?</summary>

**Explanation:** React uses a Virtual DOM to optimize rendering by comparing changes and updating only what's necessary in the real DOM.

**Example:** When state changes, React re-renders the component in Virtual DOM, diffs with previous, and patches real DOM.

**Real-time Example:** In a chat app, when a new message arrives, only the message list updates, not the entire page, for smooth performance.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Explain controlled vs uncontrolled components.</summary>

**Explanation:** Controlled components have their value controlled by React state, while uncontrolled use DOM directly.

**Example:** Controlled input.
```javascript
const [value, setValue] = useState('');
return <input value={value} onChange={(e) => setValue(e.target.value)} />;
```

**Real-time Example:** A search bar where input value is tracked in state for filtering results as you type.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">What is the Context API and when to use it?</summary>

**Explanation:** Context API provides a way to share state between components without prop drilling.

**Example:** ThemeContext allows child components to access theme without passing through all parents.

**Real-time Example:** In a multi-language app, LanguageContext provides current language to all components.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Explain React Router and its usage.</summary>

**Explanation:** React Router enables navigation between different components/views in a single-page application.

**Example:** BrowserRouter with Routes and Route components to define navigation paths.

**Real-time Example:** In a dashboard app, navigating between /dashboard, /users, /settings without page reloads.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">What are React performance optimization techniques?</summary>

**Explanation:** Use React.memo, useMemo, useCallback to prevent unnecessary re-renders, lazy loading for code splitting.

**Example:** React.memo(Component) prevents re-render if props unchanged, useMemo(() => expensiveCalc()) caches results.

**Real-time Example:** In a data-heavy table, memoize row components to prevent re-rendering on unrelated state changes.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">How do you handle forms in React?</summary>

**Explanation:** Use controlled components with state, or libraries like React Hook Form for complex forms.

**Example:** Track form values in state, validate on submit, show errors.

**Real-time Example:** In a registration form, validate email format, password strength, and show field-specific error messages.

</details>

</details>

</details>
