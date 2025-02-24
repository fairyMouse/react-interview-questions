# What is React?

## Core Concept

⚛️ A JavaScript library for building user interfaces using reusable components. Maintained by Facebook (Meta) and community.

## Key Features

### 1. Component-Based

React build encapsulated UI elements with own logic.

In order to build a user interface, we need to create components and then put them together like building blocks, each component is reusable, and handles its own state and logic

```JSX
// Parent component
function ShoppingApp() {
  return (
    <div>
      <Header title="My Shop" />
      <ProductCatalog products={['Laptop', 'Phone', 'Headphones']} />
    </div>
  )
}

// Reusable Header component
function Header({ title }) {
  return (
    <header>
      <h1>{title}</h1>
      <nav>
        <a href="#home">Home</a>
        <a href="#products">Products</a>
      </nav>
    </header>
  )
}

// Product list component
function ProductCatalog({ products }) {
  return (
    <div>
      {products.map((product, index) => (
        <Product key={index} name={product} />
      ))}
    </div>
  )
}

// Individual product component
function Product({ name }) {
  return <div className="product">{name}</div>
}
```

### 2. Declarative

In traditional imperative DOM manipulation, developers directly control every step of UI updates (like using document.getElementById() and modifying styles).

```js
// Imperative: Focus on HOW
const list = document.createElement("ul")
const item1 = document.createElement("li")
item1.textContent = "Apple"
const item2 = document.createElement("li")
item2.textContent = "Banana"
list.append(item1, item2)

// Update operation
const newItem = document.createElement("li")
newItem.textContent = "Orange"
list.appendChild(newItem)
```

However, React simplifies this process. You just need to tell React "what the UI should look like", and React handles the DOM updates automatically.

```jsx
// Declarative: Focus on WHAT
function FruitList({ items }) {
  return (
    <ul>
      {items.map((fruit, index) =>
        <li key={index}>{fruit}</li>
      )}
    </ul>
  )
}

// Usage
<FruitList items={['Apple', 'Banana']} />
// Update by changing props
<FruitList items={['Apple', 'Banana', 'Orange']} />
```

This makes our code more readable and easier to maintain.

### 3. Virtual DOM

### 4. Unidirectional Data Flow

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
