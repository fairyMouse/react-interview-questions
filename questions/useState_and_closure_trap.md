# useState Closure Trap

## Core Mechanism

🔒 State persistence through component re-renders using closure scope

### Stale Closure Example

```jsx
function Counter() {
  const [count, setCount] = useState(0)

  const handleClick = () => {
    setCount(count + 1) // Closure captures initial value
  }

  // Multiple clicks won't accumulate
  return <button onClick={handleClick}>{count}</button>
}
```

## Solutions

1. Functional updates

```jsx
setCount(prev => prev + 1)
```

2. useReducer for complex state
3. useRef for mutable values

## Common Scenarios

- Event listeners/timeouts
- Async operation queues
- Callback prop passing

## Best Practices

- Prefer functional updates
- Use reducer for state transitions
- Track mutable values with refs
