# useEffect Lifecycle Management

## Lifecycle Mapping

| Class Component      | useEffect Equivalent       |
| -------------------- | -------------------------- |
| componentDidMount    | `useEffect(fn, [])`        |
| componentDidUpdate   | `useEffect(fn, [deps])`    |
| componentWillUnmount | `useEffect(() => cleanup)` |

## Data Fetching Pattern

```jsx
function DataFetcher({ id }) {
  const [data, setData] = useState(null)

  useEffect(() => {
    const controller = new AbortController()

    const fetchData = async () => {
      const res = await fetch(`/api/${id}`, {
        signal: controller.signal,
      })
      setData(await res.json())
    }

    fetchData()
    return () => controller.abort()
  }, [id]) // Re-fetch when ID changes

  return <div>{data ? renderData(data) : "Loading..."}</div>
}
```

## Common Pitfalls

- Missing dependencies causing stale closures
- Infinite loops from incorrect deps
- Memory leaks from uncleaned effects

## Optimization Tips

- Split unrelated logic into multiple effects
- Memoize functions with useCallback
- Use empty deps for mount-only effects
