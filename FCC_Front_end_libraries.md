# FRONT END LIBRARIES

## REACT

### 1. Create a simple JSX Element

- Created by FB

- Uses JSX

- To write JS within JSX you use curly braces ` { 'this is treated as JavaScript code' } `

- Babel is popular transpiler

- ` ReactDOM.render(JSX, document.getElementById('root')) ` places JSX in the DOM

- React uses virtual DOM to render only specific parts of the actual DOM

  ```jsx
  const JSX = <h1>Hello JSX!</h1>;
  ```

### 2. Create a complex JSX Element

- JSX must return a single element

- parent has to wrap all of the other levels

  ```jsx
  const JSX = 
  <div>
      <h1>Hello there</h1>
      <p>whatever</p>
      <ul>
          <li>1st</li>
          <li>2nd</li>
          <li>3rd</li>
      </ul>
  </div>
  ```

### 3. Add comments in JSX

- Use ` {/* */} ` to wrap around the comment text

```jsx
const JSX = (
  <div>
    <h1>This is a block of JSX</h1>
    <p>Here's a subtitle</p>
    {/* Random comment */}
  </div>
);
```

### 4. Render HTML Elements to the DOM

- ReactDOM is rendering API of react
- ReactDOM offers a simple method to render React elements to the DOM which looks like this: `ReactDOM.render(componentToRender, targetNode)` 
- Must be called after the JSX declarations

```jsx
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);

ReactDOM.render(JSX, document.getElementById('challenge-node'));
```

### 5. Define  a HTML Class in JSX

- Have to use `className` instead of `class` as `class` is a reserved keyword in JS
- `camelCase` is the naming convention for all HTML attributes in JSX

```jsx
const JSX = (
  <div className='myDiv'>
    <h1>Add a class to this div</h1>
  </div>
);
```

### 6. Self-closing JSX Tags

```jsx
const JSX = (
  <div>
    <h2>Welcome to React!</h2> <br />
    <p>Be sure to close all tags!</p>
    <hr />
  </div>
);
```

### 7. Creating a Stateless Functional Component

- JavaScript function => stateless functional component (receives data and renders it but does not track changes to the data)
- The function has to begin with a capital letter

```jsx
const MyComponent = function() {
  return (
    <div>text</div>
  )
}
```

### 8. Create a React  Component

- access to many useful React features such as `local state` and `lifecycle hooks`
- best practice to call constructor with props and inside super with props

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      <h1>Hello React!</h1>
    </div>
    )
  }
};
```

### 9. Create a Component with Composition

```jsx
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        { /* change code below this line */ }
          <ChildComponent />
        { /* change code above this line */ }
      </div>
    );
  }
};
```

### 10. Use React to Render Nested Components

```jsx
const TypesOfFruit = () => {
  return (
    <div>
      <h2>Fruits:</h2>
      <ul>
        <li>Apples</li>
        <li>Blueberries</li>
        <li>Strawberries</li>
        <li>Bananas</li>
      </ul>
    </div>
  );
};

const Fruits = () => {
  return (
    <div>
      <TypesOfFruit />
    </div>
  );
};

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
          <Fruits />
      </div>
    );
  }
};
```

### 11. Compose React Components

```jsx
class Fruits extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h2>Fruits:</h2>
        <NonCitrus />
        <Citrus />
      </div>
    );
  }
};

class TypesOfFood extends React.Component {
  constructor(props) {
     super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        { /* change code below this line */ }
        <Fruits />
        { /* change code above this line */ }
        <Vegetables />
      </div>
    );
  }
};
```

### 12. Render a Class Component to the DOM

- React components are passed into `ReactDOM.render()` a bit differenly than JSX elements
- You need to use the same syntax as if you were rendering a nested component

```jsx
class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits />
        <Vegetables />
      </div>
    );
  }
};

// change code below this line
ReactDOM.render(<TypesOfFood />, document.getElementById("challenge-node"));
```

### 13. Write a React Component from Scratch

```jsx
// change code below this line
class MyComponent extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return (
            <div>
                <h1>My First React Component!</h1>
            </div>
        )
    }
}

ReactDOM.render(<MyComponent />, document.getElementById("challenge-node"));
```

### 14. Pass props to functional stateless Component

```jsx
const CurrentDate = (props) => {
  return (
    <div>
      { /* change code below this line */ }
      <p>The current date is: {props.date}</p>
      { /* change code above this line */ }
    </div>
  );
};

class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>
        { /* change code below this line */ }
        <CurrentDate date={Date()}/>
        { /* change code above this line */ }
      </div>
    );
  }
};
```

### 14. Passing array as props

```jsx
const List = (props) => {
  { /* change code below this line */ }
  return <p>{props.tasks.join(", ")}</p>
  { /* change code above this line */ }
};

class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        { /* change code below this line */ }
        <List tasks={["walk dog", "workout"]}/>
        <h2>Tomorrow</h2>
        <List tasks={["walk dog", "workout", "clean"]}/>
        { /* change code above this line */ }
      </div>
    );
  }
};
```

### 15. Use default props

```jsx
const ShoppingCart = (props) => {
  return (
    <div>
      <h1>Shopping Cart Component</h1>
    </div>
  )
};
ShoppingCart.defaultProps = { items: 0 };
```

### 16. Override default props

```jsx
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    { /* change code below this line */ }
    return <Items quantity={10} />
    { /* change code above this line */ }
  }
};
```

