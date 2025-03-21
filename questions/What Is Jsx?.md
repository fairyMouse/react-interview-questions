# What is JSX?

## Core Concept

🔧 JavaScript syntax extension that allows writing HTML-like markup in JavaScript files. Used with React to describe UI components.

## Key Features

- **JavaScript + HTML**: Mix logic and markup in same file
- **Expression Embedding**: {variables} in markup
- **Conditional Rendering**: Ternary/logical operators
- **List Rendering**: map() with key prop
- **CSS Handling**: className/style props
- **Component Composition**: Nest components like HTML tags

```jsx
// JSX example with conditional rendering
function UserGreeting({ user }) {
  return (
    <div className="card">
      {user ? (
        <h1 style={{ color: "green" }}>Welcome {user.name}!</h1>
      ) : (
        <button onClick={() => login()}>Sign In</button>
      )}
      <ul>
        {user?.skills?.map(skill => (
          <li key={skill.id}>{skill.name}</li>
        ))}
      </ul>
    </div>
  )
}
```

## JSX vs Alternatives

|                  | JSX            | HTML Strings    | Template Literals |
| ---------------- | -------------- | --------------- | ----------------- |
| **Type**         | Syntax ext     | String          | ES6 Feature       |
| **Syntax**       | XML-like       | Manual Escaping | Backticks         |
| **Data Binding** | {} Expressions | Concatenation   | ${} Interpolation |
| **Tooling**      | Babel Required | None            | Native Support    |

## Common Questions

❓ **Why not just use HTML?**  
JSX provides JavaScript's full power in markup and compile-time checks

❓ **Is JSX required for React?**  
No, but recommended for better readability

❓ **How to handle loops?**  
Use JavaScript's map()/filter() inside JSX

❓ **Adding CSS classes?**  
Use className prop instead of class

❓ **Can I use JSX without React?**  
Yes with other compilers like SolidJS/Preact
