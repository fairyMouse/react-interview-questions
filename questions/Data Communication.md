React applications utilize several patterns for data communication, each suited for different scenarios

## 1、Props (Parent-Child Communication)

The most fundamental method for data flow, following React's unidirectional data pattern.

```jsx
// Parent component
function Parent() {
  const [data, setData] = useState("Hello")
  return <Child message={data} onUpdate={setData} />
}

// Child component
function Child({ message, onUpdate }) {
  return (
    <div>
      <p>{message}</p>
      <button onClick={() => onUpdate("Updated")}>Update</button>
    </div>
  )
}
```

## 2. Context API (Cross-Component Communication)

Ideal when data needs to be shared across multiple levels of the component tree.

```jsx
// Create context
const ThemeContext = React.createContext("light")

// Provider in parent
function App() {
  const [theme, setTheme] = useState("light")

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <MainContent />
    </ThemeContext.Provider>
  )
}

// Consumer in deeply nested component
function Button() {
  const { theme, setTheme } = useContext(ThemeContext)

  return (
    <button
      style={{ background: theme === "dark" ? "#333" : "#fff" }}
      onClick={() => setTheme(theme === "light" ? "dark" : "light")}
    >
      Toggle Theme
    </button>
  )
}
```

## 3. State Management Libraries

### 1. Zustand

Lightweight state management with a simple API.

```jsx
// Create store
const useStore = create(set => ({
  count: 0,
  increment: () => set(state => ({ count: state.count + 1 })),
  decrement: () => set(state => ({ count: state.count - 1 })),
}))

// Using in component
function Counter() {
  const { count, increment } = useStore()
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  )
}
```

### 2. Redux

Suitable for large applications, providing predictable state management.

```jsx
// Store setup
const store = configureStore({
  reducer: {
    todos: todosReducer,
    filter: filterReducer,
  },
})

// Using in component with hooks
function TodoList() {
  const todos = useSelector(state => state.todos)
  const dispatch = useDispatch()

  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id} onClick={() => dispatch(toggleTodo(todo.id))}>
          {todo.text}
        </li>
      ))}
    </ul>
  )
}
```

## Recommendations

Choose the appropriate communication method based on application size and complexity, avoiding over-engineering

- Small applications: Props + Context API
- Medium-sized applications: Zustand or Context+useReducer
- Large applications: Redux Toolkit
