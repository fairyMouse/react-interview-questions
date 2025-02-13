# What is React?

## Core Concept

⚛️ A JavaScript library for building user interfaces using reusable components. Maintained by Facebook (Meta) and community.

## Key Features

- **Component-Based**: Build encapsulated UI elements with own logic
- **Declarative**: Describe UI for different states
- **Virtual DOM**: Efficient updates with diffing algorithm
- **Unidirectional Data Flow**: Props down, events up

```jsx
// React component example
function Greeting({ name }) {
  return <h1>Hello, {name}</h1>
}
```

## React vs Others

|              | React       | Angular    | Vue         |
| ------------ | ----------- | ---------- | ----------- |
| **Type**     | Library     | Framework  | Framework   |
| **DOM**      | Virtual DOM | Real DOM   | Virtual DOM |
| **Learning** | JS-focused  | TypeScript | Template    |

## React 18 Updates

- Concurrent Mode
- Automatic Batching
- New Hooks (useId, useSyncExternalStore)
