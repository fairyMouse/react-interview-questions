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

## 2. Batching Updates

```jsx
// React 18 auto-batching
const handleClick = () => {
  setCount(c => c + 1)
  setName("new")
  // Only one re-render
}

// Force synchronous update
flushSync(() => {
  setCount(42)
})
```

**Batching Explained**:  
React groups state updates occurring in:

- Event handlers
- Lifecycle methods
- useEffect callbacks

**Exception**: Async operations (setTimeout/fetch) need manual batching

## 3. Complex State

```jsx
// Object update (immutable pattern)
setUser(prev => ({ ...prev, age: 25 }))

// Array update
setList(prev => [...prev, newItem])
```

**Rule**: Always return new references for state objects/arrays

## 4. Initial State Computation

```jsx
// ❌ Avoid expensive init
const [data] = useState(computeExpensiveValue())

// ✅ Lazy initialization
const [data] = useState(() => computeExpensiveValue())
```

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
