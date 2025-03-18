## Concise Introduction

`useState` is React's fundamental state management hook that gives function components memory.It is one of the most commonly used hooks.

```jsx
// Basic usage pattern
const [value, setValue] = useState(initialValue)
```

### Common use cases

- UI state (modals, dropdowns)
- Component-specific temporary data
- Form inputs (text fields, checkboxes)

## Key Characteristics

### 1. State Isolation

Each component instance maintains its own state

### 2. Update Triggers

Calling the setter function (e.g., setValue) queues a re-render

**Batching Updates**

Batching updates is a crucial performance optimization mechanism in React that combines multiple state updates into a single re-render.

```jsx
// Multiple state updates trigger only one re-render
function handleClick() {
  setCount(c => c + 1) // Update 1
  setName("John") // Update 2
  setAge(30) // Update 3
  // React will perform just one render after all updates, not three
}
```

After React 18, introduced "automatic batching" for almost all updates, including:

- Event handlers
- Lifecycle methods
- useEffect callbacks
- Custom hooks

### 3. Initialization

Accepts initial value or initialization function for expensive computations

**Initial State Computation**

```jsx
// ❌ Avoid expensive init
const [data] = useState(computeExpensiveValue())

// ✅ Lazy initialization
const [data] = useState(() => computeExpensiveValue())
```

### 4. Update Patterns

```jsx
// Direct value
setValue(5)

// Functional update (safe for sequential updates)
setValue(prev => prev + 1)
// Object update (immutable pattern)
setUser(prev => ({ ...prev, age: 25 }))
// Array update
setList(prev => [...prev, newItem])
```

# useState Essential Usage Guide

## 1. Closure Trap

```jsx
// ❌ Wrong approach
const [count, setCount] = useState(0)
const increment = () => setCount(count + 1)

// ✅ Correct solution
const increment = () => setCount(prev => prev + 1)
```

**Why**: Functional updates ensure accessing latest state

**Rule**: Always return new references for state objects/arrays

## 5. Dependency Management

```jsx
useEffect(() => {
  // ❌ Stale state dependency
  console.log(count)
}, [])

// ✅ Proper dependency array
useEffect(() => {
  console.log(count)
}, [count])
```

## Best Practices

- Use `useState` for simple state, `useReducer` for complex logic
- Merge related states into objects
- Never mutate state directly
- Use controlled components for forms

## Common Pitfalls

```jsx
// ❌ Direct mutation
const [list] = useState([1, 2, 3])
list.push(4) // No re-render

// ❌ Accessing state after async update
setCount(42)
console.log(count) // Old value
```
