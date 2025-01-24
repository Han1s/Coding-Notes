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
- empty conditional array if run for the first time

## Cleaning up with lifecycle hooks

- ending lifeconnections etc
- in a class-based component you can use **componentWillUnmount()**
- with hooks you can use **useEffect** hook you can return a function, this function will run when the useEffect runs for  the last time
  - but it has to have empty conditional array, if it does not it triggers every time
- example with a hook:

```jsx
    useEffect(() => {
        console.log('[Cockpit.js] useEffect');
        const timer = setTimeout(() => {
             alert('Saved data to cloud!');
        }, 1000);
        return () => {
            clearTimeout(timer);
            console.log('[Cockpit.js] cleanup work in useEffect');
        }
    }, [])
```

## Using should component update for Optimization

```jsx
  shouldComponentUpdate(nextProps, nextState) {
    console.log('[Persons.js] shouldComponentUpdate')
    return nextProps.persons !== this.props.persons;
  }
```

- **Note!** - this works only because when mutating state we are creating a copy of the state. If we adjusted the state directly this would still be the same pointer

## Optimizing Functional Components with React.memo()

- **React.memo**

```jsx
export default React.memo(cockpit);
```

- need to study this more.

## When should you optimize?

- only when the check is necessary.
- If the component really should rerender almost allways these checks slow down performance

## PureComponents instead of shouldComponentUpdate

- if you impletemt **shouldComponentUpdate** when you are comparing all the props you can use **PureComponent**
  - it already implements **shouldComponentUpdate** with all props check

```jsx
class Persons extends PureComponent {
    ...
}
```

## How React Updates The Dom

- **render()**  does not immediately rerender, it is bascially a suggestion. Even if we do not catch the unnecessary update calls, it does not mean it hits the real DOM. It compares **Virtual DOMs**. It has a virtual DOM and a real DOM. React takes the Virtual one because it is faster. (It is a pure JavaScript basically). So React keeps the old one and the new one. Rerendering does not immediately update the DOM. It compares them and checks for differences. If it detects differences it updates the real dom, but only the places that are different. So if a text changes, it only updates the text. If no differences were found the real dom is not touched. Accessing the DOM is slow so you wanna do it as little as possible. This is what react does.

## Rendering Adjacent JSX Elements

- you can only return one root JSX element
- this can also be an array as long as its elements have a key
- bypass this like this:

```jsx
class Person extends Component {
    render() {
        console.log('[Person.js] rendering...');
        return [
            <p key={'i1'} onClick={this.props.click}>I'm {this.props.name}</p>,
            <p key={'i2'}>{this.props.children}</p>,
            <input key={'i3'} type='text' onChange={this.props.changed} value={this.props.name}/>
        ]
    }
}
```

- another method
- you can create a **hoc** folder with **Aux.js** (Auxilliary.js for windows) which looks like this

```jsx
const aux = props => props.children;

export default aux;
```

- this then becomes a wrapping element that solves this exact problem

## Using React Fragment

```jsx
import React, { Component } from 'react';

class Person extends Component {
    render() {
        console.log('[Person.js] rendering...');
        return (
            <React.Fragment>
                <p key={'i1'} onClick={this.props.click}>I'm {this.props.name}</p>,
                <p key={'i2'}>{this.props.children}</p>,
                <input key={'i3'} type='text' onChange={this.props.changed} value={this.props.name}/>
            </React.Fragment>
        )
    }
}

export default Person;
```

- same as Auxilliary component

## Higher Order Components

- component wrapping other components and adding something to it. Might be styling, other HTML or some logic.

```jsx
import React from 'react';

const withClass = props => (
    <duv className={props.classes}>
        {props.children}
    </duv>
);

export default withClass;
```

## Another Form of HOCs

- usually if you wanna handle behind the scene logic like errors etc, these might go with the another form
- others adding style / html etc probably the first form

```jsx
import React from 'react';

const withClass = (WrappedComponent, className) => {
    return props => (
        <div className={className}>
            <WrappedComponent />
        </div>
    );
};

export default withClass;
```

```jsx
export default withClass(App, classes.App);
```

## Passing Unknown Props

```jsx
import React from 'react';

const withClass = (WrappedComponent, className) => {
    return props => (
        <div className={className}>
            <WrappedComponent {...props} />
        </div>
    );
};

export default withClass;
```

## Setting State Correctly

- when referencing the state the update does not happen synchronously, so the state might be unexpected.
- when you depend on the old state you should use optional syntax where first argument is prevState and the second argument are current props

```jsx
this.setState( {
    persons: persons, 
    nameChangedCounter: this.state.nameChangedCounter + 1 }  // This is INCORRECT!
);
```

```jsx
// CORRECT SOLUTION

this.setState((prevState, props) => {
    return {
        persons: persons, 
        nameChangedCounter: prevState.nameChangedCounter + 1 };
	}
)
```

## Using PropTypes

- `npm install --save prop-types`

```jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';
import withClass from '../../../hoc/WithClass';
import classes from './Person.css';

class Person extends Component {
    render() {
        console.log('[Person.js] rendering...');
        return (
            <React.Fragment>
                <p onClick={this.props.click}>I'm {this.props.name} and I am {this.props.age} years old!</p>
                <p>{this.props.children}</p>
                <input type='text' onChange={this.props.changed} value={this.props.name}/>
            </React.Fragment>
        )
    }
}

Person.propTypes = {
    click: PropTypes.func,
    name: PropTypes.string,
    age: PropTypes.number,
    changed: PropTypes.func,
}

export default withClass(Person, classes.Person);
```

- feel free to use them on any components where other people might be using your components

## Using Refs

- on any element you can pass **ref** keyword. You can pass a function there and the argument you are getting is the reference to the element you place it on. In the body you can then use it

```jsx
    componentDidMount() {
        this.inputElement.focus();
    }

    render() {
        console.log('[Person.js] rendering...');
        return (
            <React.Fragment>
                <p onClick={this.props.click}>I'm {this.props.name} and I am {this.props.age} years old!</p>
                <p>{this.props.children}</p>
                <input 
                    ref={(inputEl) => {this.inputElement = inputEl}}
                    type='text' 
                    onChange={this.props.changed} 
                    value={this.props.name}/>
            </React.Fragment>
        )
    }
}
```

- other way of using

```jsx
class Person extends Component {
    constructor(props) {
        super(props);
        this.inputElementRef = React.createRef();
    }

    componentDidMount() {
        // this.inputElement.focus();
        this.inputElementRef.current.focus();
    }

    render() {
        console.log('[Person.js] rendering...');
        return (
            <React.Fragment>
                <p onClick={this.props.click}>I'm {this.props.name} and I am {this.props.age} years old!</p>
                <p>{this.props.children}</p>
                <input 
                    // ref={(inputEl) => {this.inputElement = inputEl}}
                    ref={this.inputElementRef}
                    type='text' 
                    onChange={this.props.changed} 
                    value={this.props.name}/>
            </React.Fragment>
        )
    }
}
...
```

## Refs in functional components

- not usable in functional components, but we can use react hooks

```jsx
import React, { useEffect, useRef } from 'react';
import classes from './Cockpit.css';

const cockpit = (props) => {
    const toggleBtnRef = useRef(null);  // SEUP REF HERE

    useEffect(() => {
        console.log('[Cockpit.js] useEffect');
        // setTimeout(() => {
        //      alert('Saved data to cloud!');
        // }, 1000);
        toggleBtnRef.current.click();  // CLICK HERE
        return () => {
            console.log('[Cockpit.js] cleanup work in useEffect');
        }
    }, [])

    useEffect(() => {
        console.log('[Cockpit.js] 2nd useEffect');
        return () => {
            console.log('[Cockpit.js] cleanup work in 2nd useEffect')
        }
    })

    const assignedClasses = [];
    let btnClass = '';

    if (props.showPersons) {
        btnClass = classes.Red;
    }

    if (props.personsLength <= 2) {
      assignedClasses.push(classes.red);
    }

    if (props.personsLength <= 1) {
      assignedClasses.push(classes.bold);
    }

    return (
        <div className={classes.Cockpit}>
            <h1>{props.title}</h1>
            <p className={assignedClasses.join(' ')}>This is really working!</p>
            <button
                ref={toggleBtnRef}  // REF HERE
                className={btnClass} 
                onClick={props.clicked}>
            Toggle Persons
            </button>
        </div>
    );
}

export default React.memo(cockpit);
```

## Understanding Prop Chain Problems

- what if you have props that is passing through several components but is only relevant for the last one ?
- **context** is the answer

## Context API

- context is globally available variable (or whatever scope you wanna use it in)
- context should be used as a component
- context should wrap all the parts of the application that need access to the context
- we create a context component:

```jsx
import React from 'react';

const authContext = React.createContext({
    authenticated: false, 
    login: () => {}
});

export default authContext;
```

- then we wrap what we need with this

```jsx
import React, { Component } from 'react';
import classes from './App.css';
import Persons from '../components/Persons/Persons';
import Cockpit from '../components/Cockpit/Cockpit';
import withClass from '../hoc/WithClass';
import AuthContext from '../context/auth-context'; // IMPORTING CONTEXT

class App extends Component {
  constructor(props) {
    super(props);
    console.log('[App,js] constructor');
  }

  state = {
    persons: [
      { id: 1, name: 'random 1', age: 10 },
      { id: 2, name: 'random 2', age: 20 },
      { id: 3, name: 'random 3', age: 30 }
    ],
    showCockpit: true,
    nameChangedCounter: 0,
    authenticated: false,
  }

  static getDerivedStateFromProps(props, state) {
    console.log('[App.js] getDerviedStateFromProps', props);
    return state;
  }

  conponentWillMount() {
    console.log('[App.js] componentWillMount');
  }

  componentDidMount() {
    console.log('[App.js] componentDidMount');
  }

  deletePersonHandler = (index) => {
    // const persons = this.state.persons.slice(); OPTION 1
    const persons = [...this.state.persons]; // OPTION 2
    persons.splice(index, 1);
    this.setState({persons: persons});
  }

  nameChangedHandler = (event, id) => {
    const personIndex = this.state.persons.findIndex((p) => {
      return p.id === id;
    })
    
    const person = {
      ...this.state.persons[personIndex]
    }

    person.name = event.target.value;

    const persons = [...this.state.persons];

    persons[personIndex] = person;

    this.setState((prevState, props) => {
      return {
        persons: persons, 
        nameChangedCounter: prevState.nameChangedCounter + 1 };
      }
    )
  }

  togglePersonsHandler = () => {
    this.setState({
      showPersons: !this.state.showPersons,
    })
  }

  loginHandler = () => {
    this.setState({authenticated: true});
  }

  render() {
    console.log('[App.js] render');
    let persons = null;
    
    if (this.state.showPersons) {
      persons = (
        <Persons 
        persons={this.state.persons}
        clicked={this.deletePersonHandler}
        changed={this.nameChangedHandler}
        isAuthenticated={this.state.authenticated} />
      );
    }
  
    return (
      <React.Fragment>
        <button 
          onClick={() => {
            this.setState({showCockpit: false}
          )}}>Remove Cockpit
        </button>
        <AuthContext.Provider value={{  // CONTEXT HERE
          authenticated: this.state.authenticated,
          login: this.loginHandler,
        }}>
        { this.state.showCockpit ?  <Cockpit
          title={this.props.appTitle}
          showPersons={this.state.showPersons} 
          personsLength={this.state.persons.length}
          clicked={this.togglePersonsHandler}
          login={this.loginHandler} /> : null }
        {persons}
        </AuthContext.Provider>
      </React.Fragment>
    );
  }
}

export default withClass(App, classes.App);

```

- To consume:

  ```jsx
  import React, { Component } from 'react';
  import PropTypes from 'prop-types';
  import withClass from '../../../hoc/WithClass';
  import classes from './Person.css';
  import AuthContext from '../../../context/auth-context';
  
  class Person extends Component {
      constructor(props) {
          super(props);
          this.inputElementRef = React.createRef();
      }
  
      componentDidMount() {
          // this.inputElement.focus();
          this.inputElementRef.current.focus();
      }
  
      render() {
          console.log('[Person.js] rendering...');
          return (
              <React.Fragment>
                  <AuthContext.Consumer>
                      {(context) =>  context.authenticated ? <p>authenticated!</p> : <p>Please log In</p>}
                  </AuthContext.Consumer>
                  <p onClick={this.props.click}>I'm {this.props.name} and I am {this.props.age} years old!</p>
                  <p>{this.props.children}</p>
                  <input 
                      // ref={(inputEl) => {this.inputElement = inputEl}}
                      ref={this.inputElementRef}
                      type='text' 
                      onChange={this.props.changed} 
                      value={this.props.name}/>
              </React.Fragment>
          )
      }
  }
  
  Person.propTypes = {
      click: PropTypes.func,
      name: PropTypes.string,
      age: PropTypes.number,
      changed: PropTypes.func,
  }
  
  export default withClass(Person, classes.Person);
  ```

  ## contextType  &useContext

  - usage:

  ```jsx
  import React, { Component } from 'react';
  import PropTypes from 'prop-types';
  import withClass from '../../../hoc/WithClass';
  import classes from './Person.css';
  import AuthContext from '../../../context/auth-context';
  
  class Person extends Component {
      constructor(props) {
          super(props);
          this.inputElementRef = React.createRef();
      }
  
      static contextType = AuthContext;
  
      componentDidMount() {
          // this.inputElement.focus();
          this.inputElementRef.current.focus();
          console.log(this.context.authenticated);
      }
  
      render() {
          console.log('[Person.js] rendering...');
          return (
              <React.Fragment>
                  { this.context.authenticated ? <p>Authenticated!</p> : <p>Please log In</p> }
                  <p onClick={this.props.click}>I'm {this.props.name} and I am {this.props.age} years old!</p>
                  <p>{this.props.children}</p>
                  <input 
                      // ref={(inputEl) => {this.inputElement = inputEl}}
                      ref={this.inputElementRef}
                      type='text' 
                      onChange={this.props.changed} 
                      value={this.props.name}/>
              </React.Fragment>
          )
      }
  }
  
  Person.propTypes = {
      click: PropTypes.func,
      name: PropTypes.string,
      age: PropTypes.number,
      changed: PropTypes.func,
  }
  
  export default withClass(Person, classes.Person);
  ```

- in functional components not available, you have to use **useContext** hook

<<<<<<< Updated upstream
```jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';
import withClass from '../../../hoc/WithClass';
import classes from './Person.css';
import AuthContext from '../../../context/auth-context';

class Person extends Component {
    constructor(props) {
        super(props);
        this.inputElementRef = React.createRef();
    }

    static contextType = AuthContext;

    componentDidMount() {
        // this.inputElement.focus();
        this.inputElementRef.current.focus();
        console.log(this.context.authenticated);
    }

    render() {
        console.log('[Person.js] rendering...');
        return (
            <React.Fragment>
                { this.context.authenticated ? <p>Authenticated!</p> : <p>Please log In</p> }
                <p onClick={this.props.click}>I'm {this.props.name} and I am {this.props.age} years old!</p>
                <p>{this.props.children}</p>
                <input 
                    // ref={(inputEl) => {this.inputElement = inputEl}}
                    ref={this.inputElementRef}
                    type='text' 
                    onChange={this.props.changed} 
                    value={this.props.name}/>
            </React.Fragment>
        )
    }
}

Person.propTypes = {
    click: PropTypes.func,
    name: PropTypes.string,
    age: PropTypes.number,
    changed: PropTypes.func,
}

export default withClass(Person, classes.Person);
```

# A Real App: The Burger Builder (Basic Version)

## Planning an App in React - Core Steps

- **Component Tree / Component Structure**
  - split app into react components
  - this naturally changes throughout the development
  - very important to have an idea about what should be a component and what not
- **Application State (Data)**
  - data youre planning to manipulate
- **Components vs Containers**
  - which components dumb / stateless & which components stateful

## Planning an App - Layout and Component Tree

- use firgma or something
- **App**
  - **Layout** - could be a part of the root component
    - **Toolbar**
      - Drawer Toggle
      - Logo
      - Navigation Items
    - **SideDrawer**
      - Logo
      - Navigation Items
    - **BackDrop**
    - **props.children** - other pages
      - **BurgerBuilder** will be our starting page
        - build controls
          - **list** of individual build control components
          - Order Button
        - burger
          - **list** of ingredients dynamically managed
        - Modal giving checkout preview
          - takes props children to display all sorts of stuff

## Planning the State

- **Ingredients**
  - { meat: n, cheese: x, ... }
- **purchased**: true / false
- **total price**: int
- state will be managed in the burger - builder component. New pages will manage the components as well and will not be interested in this.
- so burger builder will be stateful. Other components might be stateless.
=======
# React Router

## TODO

# REDUX

## Understanding State

**State** 

- ingredients added to Burger
- is User authenticated?
- is a Modal open?
- list of Blog Posts
- ...

## Understanding the Redux Flow

- **Central Store** stores entire application state
- **Action** is predefined information package holding a payload we are sending to redux.
  - the action does not hold any logic, its just a messanger
- **Reducers** change the central store
  - action reaches the reducer
  - the reducer then checks the type of action
  - the reducer finds the reaction and spits out the updated state
  - the reducer has to reduce synchronous code only - I/O
  - the updated store is then replacing Central Store stat
- **Subscription (module)**
  - is triggered whenever state changes

## Setting Up Reducer and Store

- `npm install --save redux` 

## Basic Redux Schema

```javascript
const redux = require('redux');
const createStore = redux.createStore;

const initialState = {
  counter: 0,
}

// Reducer
const rootReducer = (state = initialState, action) => {
  if (action.type === 'INC_COUNTER') {
    return {
      ...state,
      counter: state.counter + 1,
    }
  }
  
  if (action.type === 'ADD_COUNTER') {
    return {
      ...state,
      counter: state.counter + action.value,
    }
  }

  return state;
};

// Store
const store = createStore(rootReducer);
console.log(store.getState());

// Subscription
store.subscribe(() => {
  console.log('[Subscription]', store.getState());
});

// Dispatching Action
store.dispatch({type: 'INC_COUNTER'});
store.dispatch({type: 'ADD_COUNTER', value: 10});
console.log(store.getState());
```

## Connecting Redux to React

- `npm install --save react-redux` 
- create **store** folder in root folder next to **components** and **containers** folder
- **index.js** holds the **store** since its the place where our application roots

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import reducer from './store/reducer';
import { createStore } from 'redux';
import { Provider } from 'react-redux';

const store = createStore(reducer);

ReactDOM.render(<Provider store={store}><App /></Provider>, document.getElementById('root'));
registerServiceWorker();

```

- **store** contains **reducer.js**

```javascript
const initialState = {
  counter: 0
}

const reducer = (state = initialState, action) => {
  return state;
}

export default reducer;
```

Example:

```jsx
import React, { Component } from 'react';
import {connect} from 'react-redux';

import CounterControl from '../../components/CounterControl/CounterControl';
import CounterOutput from '../../components/CounterOutput/CounterOutput';

class Counter extends Component {
 ...
}

const mapStateToProps = state => {
    return {
        ctr: state.counter
    }
}

export default connect(mapStateToProps)(Counter);
```

>>>>>>> Stashed changes
