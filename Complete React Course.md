# Getting Started

- JS library for creating UI
- https://discord.gg/gxvEWGU

## First single page App

```jsx
function Person(props) {
  return (
  <div className='person'>
    <h1>{props.name}</h1>
    <p>{props.age}</p>
  </div>
  );
}

var app = (
  <div>
    <Person name='Honza' age='27' />
    <Person name='Manu' age='29' />
  </div>
)

ReactDOM.render(app, document.getElementById('root'));
```

## Single vs Multi-page apps

### Single page apps

- only one `reactDOM.render()`
- only one HTML file

### Multi page apps

- multiple `reactDOM.render()`
- the individual components do not know about each other

# Next-gen JavaScript

## let & const

- `let` - for variable values
- `const` - create constant

## arrow functions

normal functions:

```javascript
function myFunc() {
    ...
}
```

arrow functions:

```javascript
const myFunc = () => {
    ...
}
```

one line arrow functions:

```javascript
const multiply = number => number * 2;
```



## Export and Import

### Export default

```javascript
const person = {
    name: 'Max'
}

export default person
```

and import:

```javascript
// Imports default and only export of the file, name is up to you
import person from './person.js'
import prs from './person.js' 
```

### Named export

```javascript
export const clean = () => { ... }
export const baseData = 10;
```

and import

```javascript
import { baseData } from './utility.js'
import { clean } from './utility.js'
// OR
import { clean as myAlias } from './utility.js'
// OR
import * as bundled from './utility,js' 
// Bundled is js object that exposes everyhing as properties of the object (so to access you type bundled.data or whatever)
```



## Classes

```javascript
// Example
class Person {
	name = 'Max'
	call = () => { ... }
}
    
// Usage
const myPerson = new Person();
myPerson.call();
console.log(myPerson.name);

// Inheritance
class Person extends Master

```

Complex usage:

```javascript
class Human {
    // This will trigger whenever you instantiate the class
    constructor() {
        this.gender = 'male';
    }
    
    printGender() {
        console.log(this.gender);
    }
}

class Person extends Human {
    constructor() {
        super(); // This triggers inheritance from the extended class
        this.name = 'Max';
        this.gender = 'female';
    }
    
    printMyName() {
        console.log(this.name);
    }
}

const person = new Person();
person.printMyName();
person.printGender();
```

## Classes, Properties & Methods

Properties

```javascript
// ES6
constructor () {
    this.myProperty = 'value'
}

// ES7
myProperty = 'value'
```

Methods

```javascript
// ES6
myMethod () { ... }

//ES7
myMethod = () => { ... } // Think of it as a variable that is assigned a function
```

ES7 Usage

```javascript
class Human {
    // This will trigger whenever you instantiate the class
    gender = 'male';
    
    printGender = () => {
        console.log(this.gender);
    }
}

class Person extends Human {
    name = 'Max';
	gender = 'female';
    
    printMyName = () => {
        console.log(this.name);
    }
}

const person = new Person();
person.printMyName();
person.printGender();
```

### Spread & Rest operators

```javascript
...
```

Spread usage

```javascript
// Used to split up array of elements or Object properties
const newArray = [...oldArray, 1, 2]
const newObject = {...oldObject, newProp: 5 }
```

Rest usage

```javascript
// Used to merge a list of function arguiments int oarray
function sortArgs(...args) {
    return args.sort();
}
```



## Destructuring

- easily extract array elements or object properties and store them in variables

Array destructuring

```javascript
const numbers = [1, 2, 3];
[num1, , num3] = numbers;
console.log(num1, num3); // 1, 3
```

Object destructuring

```javascript
{name} = {name: 'Max', age: 28 }
console.log(name) // Max
console.log(age) //undefined
```



## Reference and Primitive Types Refresher

- **numbers and booleans**, etc, are primitive types (when you assign it it copies the value)
- **object and arrays** are reference types 

```javascript
const person = {
    name: 'Max'
}

const secondPerson = person;

person.name = 'Manu';

console.log(secondPerson); // [object Object] { name: 'Manu' }

// This actually coppies the object, not points to it
const secondPerson = {
    ...person
};
```

Actually copying the object

# Understanding the base Features & Syntax

## Using react-create-app

1. Install npm
2. `npm install create-react-app -g` 
3. `create-react-app project-name`
4. `npm start` to run the server  in the folder
5. **localhost:3000** then runs the active server

## Understanding JSX

```jsx
return (<div>
    	...
    	</div>)
```

- this is just a substitute of `React.createElement()`

## JSX Restrictions

- `className` instad of `class`
- JSX has to have only one root element (this is loosened with React 16)

## Creating a functional component

```jsx
import React from 'react';

const person = () => {
    return <p>I'm a Person!</p>
}

export default person;
```

When creating components, you have the choice between **two different ways:**

1. **Functional components** (also referred to as "presentational", "dumb" or "stateless" components - more about this later in the course) => `const cmp = () => { return <div>some JSX</div> }` (using ES6 arrow functions as shown here is recommended but optional)
2. **class-based components** (also referred to as "containers", "smart" or "stateful" components) => `class Cmp extends Component { render () { return <div>some JSX</div> } }` 

## Outputting dynamic content

```jsx
import React from 'react';

const person = () => {
    return <p>I'm a Person and I am { Math.floor(Math.random() * 30) } years old!</p>
}

export default person;
```

## Working with props

```jsx
import React from 'react';

const person = (props) => {
    return <p>I'm { props.name } and I am { props.age } years old!</p>
}

export default person;
```

## Children props

- `children` is a reserved props that takes whatever is between opening and closing brackets including complex html and js code

```jsx
import React from 'react';

const person = (props) => {
    return (
        <div>
            <p>I'm { props.name } and I am { props.age } years old!</p>
            <p>{ props.children }</p>
        </div>
    )
}

export default person;
```

## Props and State

- Only changes in **props** and **state** trigger rerender of the DOM

**Props**

`props` allow you to pass data from a parent (wrapping) component to a child (embedded) component.

**Example:**

**AllPosts Component:**

```jsx
const posts = () => {
    return (
        <div>
            <Post title="My first Post" />
        </div>    
    );
}
```

Here, `title` is the custom property (`prop` ) set up on the custom `Post` component. We basically replicate the default HTML attribute behavior we already know (e.g. `<input type="text">` informs the browser about how to handle that input).

**Post Component:**

```jsx
const post = (props) => {
    return (
        <div>
            <h1>{props.title}</h1>
        </div>
    );
}
```

The `Post` component receives the `props` argument. You can of course name this argument whatever you want - it's your function definition, React doesn't care! But React will pass one argument to your component function => An object, which contains all properties you set up on `<Post ... />` .

`{props.title}` then dynamically outputs the `title` property of the `props` object - which is available since we set the `title` property inside `AllPosts` component (see above).



**State**

Whilst props allow you to pass data down the component tree (and hence trigger an UI update), state is used to change the component, well, state from within. Changes to state also trigger an UI update.

**Example:**

**NewPost Component:**

```jsx
class NewPost extends Component { // state can only be accessed in class-based components!    
    state = {
        counter: 1
    };       

	render () { // Needs to be implemented in class-based components! Needs to return some JSX!        
        return (
            <div>{this.state.counter}</div>
        );    
    }
}
```

Here, the `NewPost` component contains `state` . Only class-based components can define and use `state` . You can of course pass the `state` down to functional components, but these then can't directly edit it.

`state` simply is a property of the component class, you have to call it `state` though - the name is not optional. You can then access it via `this.state` in your class JSX code (which you return in the required `render()` method).

Whenever `state` changes (taught over the next lectures), the component will re-render and reflect the new state. The difference to `props` is, that this happens within one and the same component - you don't receive new data (`props` ) from outside!

## Manipulating the state

- **changing state** & **changing props** rerenders the dom
- **state** is only usable in class components

```jsx
switchNameHandler = () => {
    // console.log('Was clicked!');
    this.setState({
        persons: [
            { name: 'Maximilian', age: 20 },
            { name: 'Manu', age: 27 },
            { name: 'Stephanie', age: 26 }
        ]
    })
}
```

## useState() Hooks for State Maniupulation

- **hooks** are the way to use state in functional components

- **useState** returns array with two elements
- the first element is the current state
  - the second element is always a function that allows us to update the state
  
- **useState** does not actually merge the info as **setState** which means you have to use several **useState** properties for the app


## Stateful vs Stateless Components

- Good practice to use as many **stateless** components as you can
- Only a couple **statefull** components
  - This makes app easier to manage and maintain
- Have as many **pure** components as possible

## Passing method references between components

- You can pass a method to the child through props (no method call, only a method refernece)
- Two methods how to pass a argument with it as well
  - `click={this.switchNameHandler.bind(this, 'Max!')}` 
    - preferred way. More efficient.
  - `onClick={() => this.switchNameHandler('Maximilan!!')}`
    - less efficient, preferably dont use

```jsx
  render() {
    return (
      <div className='App'>
        <h1>Hi, I'm a React App</h1>
        <p>This is really working!</p>
        <button onClick={() => this.switchNameHandler('Maximilan!!')}>Switch Name</button>
        <Person 
        name={this.state.persons[0].name} 
        age={this.state.persons[0].age}></Person>
        <Person 
        name={this.state.persons[1].name} 
        age={this.state.persons[1].age}
        click={this.switchNameHandler.bind(this, 'Max!')}></Person>
        <Person 
        name={this.state.persons[2].name} 
        age={this.state.persons[2].age}></Person>
      </div>
    );
  }
```

## Adding a two way binding

- for example for an input field you can create

```jsx
  nameChangedHandler = (event) => {
    this.setState( {
      persons: [
        { name: 'Max', age: 28 },
        { name: event.target.value, age: 29 },
        { name: 'Stephanie', age: 26 },
      ]
    })
  }
```

- evand set value for the person 

```jsx
const Person = ( props ) => {
    return (
        <div>
            <p onClick={props.click}>I'm {props.name}</p>
            <p>{props.children}</p>
            <input type='text' onChange={props.changed} value={props.name}/>
        </div>
    )
}
```

- and pass it as

```jsx
<Person 
    name={this.state.persons[1].name} 
    age={this.state.persons[1].age}
    click={this.switchNameHandler.bind(this, 'Max!')}
    changed={this.nameChangedHandler}>
</Person>
```

## Adding Extra Styling

Two ways:

- Create a css file with the same name in the component folder and import it to the component.

## Working with inline styles

```jsx
  render() {
    const style = {
      backgroundColor: 'white',
      font: 'inherit',
      border: '1px solid blue',
      padding: '8px',
      cursor: 'pointer',
    };
    // ...
  }

// ...
<button 
    style={style}
    onClick={() => this.switchNameHandler('Maximilan!!')}>Switch Name
</button>
// ...
```

- Problems
  - if you use css file, the css will get applied globally,
  - if you use inline styles, there are certain limitations
  - golden way later in the course.

# Working with Lists and Conditionals

## Rendering Content conditionally

- One way is to use ternary in jsx with null in the other condition

- Other cleaner way:

  ```jsx
  render() {
      const style = {
          backgroundColor: 'white',
          font: 'inherit',
          border: '1px solid blue',
          padding: '8px',
          cursor: 'pointer',
      };
  
      let persons = null;
  
      if (this.state.showPersons) {
          persons = (
              <div>
                  <Person 
                      name={this.state.persons[0].name} 
                      age={this.state.persons[0].age}></Person> 
                  <Person 
                      name={this.state.persons[1].name} 
                      age={this.state.persons[1].age}
                      click={this.switchNameHandler.bind(this, 'Max!')}
                      changed={this.nameChangedHandler}></Person>
                  <Person 
                      name={this.state.persons[2].name} 
                      age={this.state.persons[2].age}></Person>
              </div>
          )
      }
  
      return (
          <div className='App'>
              <h1>Hi, I'm a React App</h1>
              <p>This is really working!</p>
              <button 
                  style={style}
                  onClick={this.togglePersonsHandler}>Toggle Persons</button>
              {persons}
          </div>
      );
  }
  ```

## Outputting lists

- **map()** method

  ```jsx
  <div>
      {   this.state.persons.map((person) => {
          return <Person 
                     name={person.name} 
                     age={person.age} />
      })}
  </div>
  ```

## Lists and state

- **When mutating arrays you should create a copy first, otherwise this will lead to a buggy behavior**

```jsx
  deletePersonHandler = (index) => {
    // const persons = this.state.persons.slice(); OPTION 1
    const persons = [...this.state.persons]; // OPTION 2
    persons.splice(index, 1);
    this.setState({persons: persons});
  }
```

- **List key has to be an unique value, say DB Id, NOT index of the array, because that mutates as array changes and does not help react**

# Styling React Components

## Outlining the problem set

- If you use inline styles, you cannot use pseudo-selectors (such as ::hover)
- but if we create css file it will apply globally
- how about changing styling dynamically?

## Setting Styles Dynamically

```jsx
  render() {
    const style = {
      backgroundColor: 'green',
      color: 'white',
      font: 'inherit',
      border: '1px solid blue',
      padding: '8px',
      cursor: 'pointer',
    };

    let persons = null;
    
    if (this.state.showPersons) {
      persons = (
        <div>
          {this.state.persons.map((person, index) => {
            return (
            <Person 
              key={person.id}
              click={() => this.deletePersonHandler(index)}
              name={person.name} 
              age={person.age}
              changed={(event) => this.nameChangedHandler(event, person.id)} />)
          })}
        </div>
      )

      // Here the style is changed if the condition is met
      style.backgroundColor = 'red';
    }
  
    return (
      <div className='App'>
        <h1>Hi, I'm a React App</h1>
        <p>This is really working!</p>
        <button 
          style={style}
          onClick={this.togglePersonsHandler}>Toggle Persons</button>
          {persons}
      </div>
    );
```

## Setting Class Names Dynamically

```jsx
    const classes = [];
    if (this.state.persons.length <= 2) {
      classes.push('red');
    }

    if (this.state.persons.length <= 1) {
      classes.push('bold');
    }
  
    return (
      <div className='App'>
        <h1>Hi, I'm a React App</h1>
        <p className={classes.join(' ')}>This is really working!</p>
        <button 
          style={style}
          onClick={this.togglePersonsHandler}>Toggle Persons</button>
          {persons}
      </div>
    );
```

## Adding and Using Radium

- `npm install --save radium` 

- using radium:

  ```jsx
  import Radium from 'radium';
  // ... now wrap the app or a component exported with the higher order function
  export default Radium(App);
  ```

- using radium features:

  ```jsx
    render() {
      const style = {
        backgroundColor: 'green',
        color: 'white',
        font: 'inherit',
        border: '1px solid blue',
        padding: '8px',
        cursor: 'pointer',
        ':hover': {  // RADIUM FEATURE
          backgroundColor: 'lightgreen',
          color: 'black',
        }
      };
  
      let persons = null;
      
      if (this.state.showPersons) {
        persons = (
          <div>
            {this.state.persons.map((person, index) => {
              return (
              <Person 
                key={person.id}
                click={() => this.deletePersonHandler(index)}
                name={person.name} 
                age={person.age}
                changed={(event) => this.nameChangedHandler(event, person.id)} />)
            })}
          </div>
        )
  
        style.backgroundColor = 'red';
        style[':hover'] = {  // RADIUM FEATURE
          backgroundColor: 'lightred',
          color: 'black',
        }
      }
  ```

  ## Using Radium for Media Queries

  ```jsx
  import React from 'react';
  import './Person.css';
  import Radium from 'radium';
  
  const Person = ( props ) => {
      const style = {
          '@media (min-width: 500px)': {  // RADIUM
              width: '450px',
          }
      }
  
      return (
          <div className="Person" style={style}>
              <p onClick={props.click}>I'm {props.name}</p>
              <p>{props.children}</p>
              <input type='text' onChange={props.changed} value={props.name}/>
          </div>
      )
  }
  
  export default Radium(Person);  // RADIUM
  ```

  - then import styleroot

  ```jsx
  import Radium, { StyleRoot } from 'radium';
  ...
  return (
      <StyleRoot>
          <div className='App'>
              <h1>Hi, I'm a React App</h1>
              <p className={classes.join(' ')}>This is really working!</p>
              <button 
                  style={style}
                  onClick={this.togglePersonsHandler}>Toggle Persons</button>
              {persons}
          </div>
      </StyleRoot>
  );
  ```

  ## Introducing Styled Components

  - `npm install --save styled-components`

  ```jsx
  import React from 'react';
  import './Person.css';
  import styled from 'styled-components';
  
  const StyledDiv = styled.div`  // Styled components
      width: 60%;
      margin: 16px auto;
      border: 1px sold #eee;
      box-shadow: 0 2px 3px #ccc;
      padding: 16px;
      text-align: center;
  
      @media (min-width: 500px) {
          width: 450px;
      }
  `;
  
  const Person = ( props ) => {
      return (
          <StyledDiv>  // Styled components
              <p onClick={props.click}>I'm {props.name}</p>
              <p>{props.children}</p>
              <input type='text' onChange={props.changed} value={props.name}/>
          </StyledDiv>
      )
  }
  
  export default Person;
  ```

  ## More on Styled Components

  - it creates classes automatically so it is not global
  - adding hover and stuff

  ```jsx
  const StyledButton = styled.button`
    background-color: green,
    color: white,
    font: inherit, 
    border: 1px solid blue,
    padding: 8px,
    cursor: pointer,
    
    &:hover {
      background-color: lightgreen,
      color: black,
    }
  `;
  ```

  ## Styled Components & Dynamic Styles

  ```jsx
  const StyledButton = styled.button`
    background-color: ${props => props.alt ? 'red' : 'green'},
    color: white,
    font: inherit, 
    border: 1px solid blue,
    padding: 8px,
    cursor: pointer,
    
    &:hover {
      background-color: ${props => props.alt ? 'salmon' : 'lightgreen'},
      color: black,
    }
  `;
  
  ...
   <StyledButton alt={this.state.showPersons} onClick={this.togglePersonsHandler}>
      Toggle Persons
  </StyledButton>
  ...
  ```

  ## Working with CSS Modules

  - first eject `npm run eject`

  - this will display the config folder in which you will find **webfack.config.dev.js** and **webpack.config.prod.js** files.   

  - Do this in both of the files

    ![image-20201018181814217](C:\Users\honza\AppData\Roaming\Typora\typora-user-images\image-20201018181814217.png)

  - now we can:

  ```jsx
  import classes from './App.css';
  ```

  - This will import all the classes as properties of classes object
  - then we can do:

  ```jsx
  <button className={classes.button} onClick={this.togglePersonsHandler}>
  ```
  - In  React-scripts 2.0 + you can use modules automatically with a little tweak - watch the video 74.

  ## More on CSS Modules

  - Projects

    - https://medium.com/nulogy/how-to-use-css-modules-with-create-react-app-9e44bec2b5c2

  - More information about modules

    - https://github.com/css-modules/css-modules

    

# Debugging React Apps

## Finding Logical Errors by using Dev Tools & Sourcemaps

- In **developer tools** > **sources** tab you can access your original code and place a breakpoint. Afterwards you just trigger the function

## Using Error Boundaries

- ```jsx
  import React, { Component } from 'react';
  
  class ErrorBoundary extends Component {
      state = {
          hasError: false,
          errorMessage: '',
      }
  
      componentDidCatch = (error, info) => {
          this.setState({
              hasError: true,
              errorMessage: error,
          })
      }
  
      render() {
          if (this.state.hasError) {
              return <h1>{this.state.errorMessage}</h1>;
          } else {
              return this.props.children;
          }
      }
  }
  
  export default ErrorBoundary;
  ```

- should go to ErrorBoundary folder for its own component

- wrap only the code that can fail

## Useful resources and Links

- Error boundaries: https://reactjs.org/docs/error-boundaries.html
- Chrome Dev Tool Debugging https://developers.google.com/web/tools/chrome-devtools/javascript/

# Diving Deeper into Components & React Internals

## A Better Project Structure

- No need to setup smaller components unless there is a reason for it
- The statefull components should actually have as little jsx as possible in its render method
- **The root**
  - **assets**
    - imges, etc
  - **components**
    - Cockpit
      - Cockpit.js
    - Persons
      - Person
        - Person.js
        - Person.css
  - **containers**
    - App.css
    - App.js
    - App.test.js
    - ...

## Class-based vs Functional Components

- **class-based**
  - class
  - can access state
  - lifecycle hooks
  - needs `this` keyword
- **functional**
  - const
  - access to state
  - lifecycle hooks still not supported
  - props are argument and therefore normal variable

## Component Lifecycle

- only available in class-based components
- **constructor(props)**
  - when a component is created, default ES6 feature.
  - This constructor receives props and you have to call `super(props)` if you wanna own constructor
  - you should not do side-effects in constructor (sending request, doing something, etc)
- **getDerivedStateFromProps(props, state)** 
  - sync state, if props can change and then you wanna update something then this is the hook
  - dont cause side effects
- **render**()
  - prepares structure
  - do your jsx here
- **render child components**
- **componentDidMount()**
  - can cause side effects
  - you should not update state here, triggers rerender cycle

## Component Update Lifecycle

- **getDerivedStateFromProps(props, state)**
- **shouldComponentUpdate(nextProps, nextState)**
  - decide whether or not react should rerender component
  - this is mostly for performance reasons
- **render()**
  - prepare and structure jsx code here
- react then goes ahead and **updates child component props**
- **getSnapshotBeforeUpdate(prevProps, prevState)**
  - for last minute DOM operations, (getting current scrolling position of the user etc)
- **componentDidUpdate()**
  - can cause side-effects here, but
  - you should not update state here
- **componentDIdMount, componentDidUpdate, shouldComponentUpdate** are the most important by far

## Using useEffect() in Functional Components

- conditional array usage