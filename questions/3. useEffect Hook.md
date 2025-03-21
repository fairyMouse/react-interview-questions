# useEffect Essential Guide

## Core Principles

🎯 Manage side effects (data fetching, subscriptions, DOM mutations) in function components

### Basic Pattern

```jsx
useEffect(() => {
  // Setup logic
  return () => {
    // Cleanup logic
  }
}, [dependencies])
```

## Lifecycle Mapping

| Class Component      | useEffect Equivalent   | Typical Use Case      |
| -------------------- | ---------------------- | --------------------- |
| componentDidMount    | `useEffect(fn, [])`    | Initial data fetch    |
| componentDidUpdate   | `useEffect(fn, [dep])` | Update on prop change |
| componentWillUnmount | Cleanup function       | Cancel subscriptions  |

## Common Patterns

### Data Fetching

```jsx
useEffect(() => {
  let isMounted = true
  const controller = new AbortController()

  fetchData(id, { signal: controller.signal }).then(data => {
    if (isMounted) setData(data)
  })

  return () => {
    isMounted = false
    controller.abort()
  }
}, [id])
```

### Event Listeners

```jsx
useEffect(() => {
  const handleResize = () => setWidth(window.innerWidth)
  window.addEventListener("resize", handleResize)
  return () => window.removeEventListener("resize", handleResize)
}, [])
```

## Critical Rules

1. **Dependency Array**

   - Empty `[]`: Run once on mount
   - Omitted: Run after every render
   - Specific values: Run when values change

2. **Cleanup Essentials**

   ```jsx
   useEffect(() => {
     const timer = setInterval(() => {}, 1000)
     return () => clearInterval(timer)
   }, [])
   ```

3. **Async Handling**

   ```jsx
   // ✅ Correct async pattern
   useEffect(() => {
     let isActive = true

     const fetchData = async () => {
       const result = await apiCall()
       if (isActive) setData(result)
     }

     fetchData()
     return () => {
       isActive = false
     }
   }, [query])
   ```

## Performance Optimization

| Technique             | Implementation           | When to Use                  |
| --------------------- | ------------------------ | ---------------------------- |
| Conditional Execution | `if (shouldRun) { ... }` | Skip unnecessary effects     |
| Memoized Dependencies | `useMemo`/`useCallback`  | Prevent unnecessary triggers |
| Effect Splitting      | Multiple useEffect calls | Separate concerns            |

## Common Pitfalls

```jsx
// ❌ Infinite loop (missing dependency)
useEffect(() => {
  setCount(count + 1)
}, [])

// ❌ Stale closure (outdated state)
useEffect(() => {
  const id = setInterval(() => {
    console.log(count) // Always initial value
  }, 1000)
  return () => clearInterval(id)
}, [])

// ❌ Missing cleanup
useEffect(() => {
  socket.connect()
}, [])
```

## React 18+ Considerations

- **Strict Mode** double effects (development only)
- **Concurrent Mode** effects might run multiple times
- **Suspense** integration with data fetching

## Best Practices

1. Always specify dependencies explicitly
2. Clean up every effect that needs it
3. Use custom hooks for complex logic
4. Prefer smaller focused effects
5. Use eslint-plugin-react-hooks
