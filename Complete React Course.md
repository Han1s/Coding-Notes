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
3. `create react app project-name`
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

## useState() Hook sfor State Maniupulation

- **hooks** are the way to use state in functional components

- **useState** returns array with two elemtns

  - the first element is the current state
  - the second element is always a function that allows us to update the state

- **useState** does not actually merge the info as **setState** which means you have oto use several **useState** properties for the app

  ## TEST

