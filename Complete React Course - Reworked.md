# I. Getting Started

## 2. What is react

- JS library to build user interfaces
- runs the logic in the browser
- manipulates the DOM

## 3. Why React instead of JS?

- in JS you need to code every single step (imperative approach)
- every code snippet has a single task it takes care of
- React is in written in **declarative** way

## 5. Exploring React Alternatives (Vue, Angular)

- **React** just focuses on the components, extra functionality requires packages
- **Angular** ships in more built-in features, can be overkill for smaller projects but you dont need to rely on the community for the larger projects
- **Vue** is something in between. It is a bit less popular. You have to rely less on community and dont have as much overload as with Angular.

## 6. Join the Online Learning Community

- https://academind.com/community/

## 7. About this course

- Basics of React
  - Components and building UIs
  - Working with Events, Props, State
  - Styling your react App & Components
  - React Hooks
- Advanced concepts
  - Side Effects, Refs, More Hooks
  - Context API, Redux
  - Forms, Http Requests, Custom Hooks
  - Routing Deployment, NextJS
- Summaries and refreshers
  - Javascript Refresher
  - ReactJS Summary

## 10. Setting up the environment

- **Visual Studio Code**
  - install **prettier** plugin

# 2. Understanding Javascript

## 11. let & const

- `let` - for variable values
- `const` - create constant

## 12. Arrow functions

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



## 13. Export and Import

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



## 14. Classes

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

## 15. Classes, Properties & Methods

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



## 16. Destructuring

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



## 17. Reference and Primitive Types Refresher

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

# 3. React Basics & Working With Components

## 25. What are components and why is react all about them

- react is library for simplifying building UIs.
- It makes more sense to use it for more complex UIs.
- Its less error prone.
- React is all about Components
  - all UIs are made of components
  - Components are reusable building blocks in your UIs
- Components are great due to **reusability** and **separation of concerns**

## 26. React is written in declarative way

- how is A component built?
  - HTML + CSS + JS ==> All combined in React
    - CSS is the least important part
    - mostly React is combining HTML + JS
  - React uses **declarative approach**
    - You will not tell steps to react.
    - You just define desired target state and its the reacts job to figure out what to add / remove / update. We do not write these steps.

## 27. Creating a new React Project

- **Create React App**
  - First install NodeJS
  - install **create-react-app**
  - `npx create-react-app name-of-the-folder`
    - check for vpn, antivirus, etc errors when installing
  - now you can **cd** into the folder and run `npm start` to start the development web server **:3000**
  - install **visual studio code**

## 29. Analyzing a standard React project

- React is just **JavaScript**
- **index.js** is the first file that is executed
- **public folder** holds **index.html**, which is the only html that we deliver to the browser
- **App.js** holds the **JS** logic

## 30. Introducing JSX

- stands for **JS xtml**. Its a xtml code inside JavaScript

## 31. How React Works

- we define target state and React is responsible for the rest

## 39. The concept of Composition

```jsx
import './Card.css';

function Card(props) {
  const classes = 'card ' + props.className;
  return (
    <div className={classes}>
      {props.children}
    </div>
  )
}

export default Card;
```

## 41. Closer Look at JSX

- you no longer need to import React in CRA apps
- **jsx** is basically just **React.createElement()** function called

## 42. Organizing component files

- usually components go to subfolders
- UI to separate folders, etc.

## 43. Alternative function syntax

- standard function syntax

```jsx
function App() {
    ...
}
```

- arrow function syntax

```jsx
const App = () => {
    ...
}
```



# 4. React State & Working with Events

## 46. Listening to events and working with event handlers

```jsx
import ExpenseDate from './ExpenseDate';
import './ExpenseItem.css';
import Card from '../UI/Card';

const ExpenseItem = (props) => {
  const clickHandler = () => {
    console.log('clicked!');
  }

  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date}/>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">${props.amount}
        </div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  )
}

export default ExpenseItem;
```

## 48. Working with state

- all the React hooks start with **use...**
- hooks should not be called in the nested functions