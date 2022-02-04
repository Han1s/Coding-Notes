Notes for work:

- debouncing into return
- refactor using context
- utilize React.memo()

TODO:

- check https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
- module 13.

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
- you can just use a single state, depends on you

## 55. Updating a state depending on the previous state

- whenever you update a state and you depend on the previous state, you should pass an anonymous arrow function to that receives **prevState** snapshot and now you can return new state snapshot
- this is because React schedules state updates so you could be depending on incorrect state snapshots in some cases

```javascript
const titleChangeHandler = (event) => {
    setUserInput((prevState) => {
        return { 
	        ...prevState,
            enteredTitle: event.target.value
        }
    })
}
```

## 56. Form Submission

- whenever form is submitted the browser reloads, that we dont want so we have to use **event.preventDefault()**

```jsx
const submitHandler = (event) => {
    event.preventDefault(); // prevent page reload

    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date (enteredDate)
    }

    console.log(expenseData);
  }

  return (
    <form onSubmit={submitHandler}>
          ...
```

## 58. Controlled Components & Stateless vs Stateful components

- controlled are components with two-way binding
  - the component is controlled by its parent
  - most components in the app should be stateless

## 62. Rendering lists of data

- use **map()**
  - React can render list of elements

## 63. Understanding Keys

- without keys the react updates all the items
- not recommended to use index
- always add Keys

## 66. Outputting a conditional content

```jsx
import { Fragment, useState } from 'react';
import './Expenses.css';
import ExpenseItem from './ExpenseItem';
import Card from '../UI/Card';
import ExpensesFilter from './ExpensesFilter';

const Expenses = (props) => {
  const [year, setYear] = useState(2020);

  const filteredExpenses = props.expenses.filter((expense) => {
    return expense.date.getFullYear().toString() === year;
  });

  let expensesContent = <p>No Expenses found.</p>;
  if (filteredExpenses.length) {
    expensesContent = (
      filteredExpenses.map((expense) => {
        return (
          <ExpenseItem
            key={expense.id}
            title={expense.title}
            amount={expense.amount}
            date={expense.date}/>
          )
        }
      )
    )
  }

  const yearChangeHandler = (event) => {
    setYear(event.target.value);
  }

  return (
    <Fragment>
      <Card className='expenses'>
        <ExpensesFilter 
          yearChangeHandler={yearChangeHandler}
          year={year}
        />
        {expensesContent}
      </Card>
    </Fragment>
  )
}

export default Expenses;
```

# 6. Styling React Components

- two approaches
  - **Styled Components** library
  - **CSS Modules** approach

## 74. Setting dynamic inline styles

- they have the highest priority
- not ideal solution

```jsx
const CourseInput = props => {
  # ...

  return (
    <form onSubmit={formSubmitHandler}>
      <div className="form-control">
        <label style={{color: !isValid ? 'red' : 'black'}}>Course Goal</label>
        <input style={{borderColor: !isValid ? 'red' : 'black', background: !isValid ? 'salmon': 'transparent'}} type="text" onChange={goalInputChangeHandler} />
      </div>
      <Button type="submit">Add Goal</Button>
    </form>
  );
};
```

## 75. Using styled components

`npm install --save styled-components`

- you can also install **vscode-styled-components** extension for the markup

```jsx
import styled from 'styled-components';

const Button = styled.button`
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;
  width: 100%;

  @media (min-width: 700px) {
    width: auto;
  }

  &:focus {
    outline: none;
  }

  &:hover,
  &:active {
    background: #ac0e77;
    border-color: #ac0e77;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
  }
`;

export default Button;

```

## 77. Styled components and dynamic mapping

```jsx
import React, { useState } from 'react';
import styled from 'styled-components';

import Button from '../../UI/Button/Button';
import './CourseInput.css';

const FormControl = styled.div`
  margin: 0.5rem 0;

  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
    color: ${props => (props.invalid ? 'red' : 'black')};
  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid ${props => (props.invalid ? 'red' : '#ccc')};
    background: ${props => (props.invalid? '#ffd7d7' : 'transparent')};
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
  }

  & input:focus {
    outline: none;
    background: #fad0ec;
    border-color: #8b005d;
  }
`;

const CourseInput = props => {
  const [enteredValue, setEnteredValue] = useState('');
  const [isValid, setIsValid] = useState(true);

  const goalInputChangeHandler = event => {
    if (event.target.value) setIsValid(true);
    setEnteredValue(event.target.value);
  };

  const formSubmitHandler = event => {
    event.preventDefault();
    if (!enteredValue.trim().length) {
      setIsValid(false);
      return;
    }
    props.onAddGoal(enteredValue);
  };

  return (
    <form onSubmit={formSubmitHandler}>
      <FormControl invalid={!isValid}>
        <label>Course Goal</label>
        <input type="text" onChange={goalInputChangeHandler} />
      </FormControl>
      <Button type="submit">Add Goal</Button>
    </form>
  );
};

export default CourseInput;

```

## 79. CSS Modules

- need a specific configuration (**CRA** for example)

```jsx
import styled from 'styled-components';

import styles from './Button.module.css'; 
# rename the css file and the import syntax\
# call classes with styles.*

const Button = (props) => {
  return (
    <button type={props.type} className={styles.button} onClick={props.onClick}>
      {props.children}
    </button>
  )
}

export default Button;

```

# 8. Time to practice

- to pass normal class as well as a props classes:

  ```jsx
  const Card = (props) => {
      return (
          <div className={`${classes.card} ${props.className}`}>
              {props.children}
          </div>
      )
  }
  ```

- to create a button with style and onClick

  ```jsx
  const Button = (props) => {
      return (
          <button 
              className={classes.button} 
              type={props.type || 'button'}
              onClick={props.onClick}>
              {props.children}
          </button>
      )
  }
  ```


# 9. Diving Deeper: Fragments, Portals, Refs

## 103. React Portals

- for example relevant with **modals**
- Render componetn somewhere else
- e.g. to move modals or backdrop directly below the body

## 104. Working with Portals

```html
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="backdrop-root"></div>
    <div id="overlay-root"></div>
    <div id="root"></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  </body>
```

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

import Card from './Card';
import Button from './Button';
import classes from './ErrorModal.module.css';

const Backdrop = (props) => (
	# ...
)

const ModalOverlay = (props) => (
	# ...
)

const ErrorModal = (props) => {
  return (
    <React.Fragment>
      {ReactDOM.createPortal(<Backdrop onConfirm={props.onConfirm}/>, document.getElementById('backdrop-root'))}
      {ReactDOM.createPortal(<ModalOverlay title={props.title} message={props.message} onConfirm={props.onConfirm} />, document.getElementById('overlay-root'))}
    </React.Fragment>
  );
};

export default ErrorModal;

```

## 105. Working with Refs

- allow us to access and work with other dom elements
- **Usage**: If you only want to read a value, and not change anything. To use state as a keylogger is not really nice.

```jsx
import React, { useState, useRef } from 'react';

import Card from '../UI/Card';
import Button from '../UI/Button';
import ErrorModal from '../UI/ErrorModal';
import classes from './AddUser.module.css';

const AddUser = (props) => {
  const nameInputRef = useRef();
  const ageInputRef = useRef();

  const [error, setError] = useState();

  const addUserHandler = (event) => {
    event.preventDefault();
    const enteredName = nameInputRef.current.value;
    const enteredUserAge = ageInputRef.current.value;
    if (enteredName.trim().length === 0 || enteredUserAge.trim().length === 0) {
      setError({
        title: 'Invalid input',
        message: 'Please enter a valid name and age (non-empty values).',
      });
      return;
    }
    if (+enteredUserAge < 1) {
      setError({
        title: 'Invalid age',
        message: 'Please enter a valid age (> 0).',
      });
      return;
    }
    props.onAddUser(enteredName, enteredUserAge);
    nameInputRef.current.value = '';
    ageInputRef.current.value = '';
  };

  const errorHandler = () => {
    setError(null);
  };

  return (
    <div>
      {error && (
        <ErrorModal
          title={error.title}
          message={error.message}
          onConfirm={errorHandler}
        />
      )}
      <Card className={classes.input}>
        <form onSubmit={addUserHandler}>
          <label htmlFor="username">Username</label>
          <input
            id="username"
            type="text"
            ref={nameInputRef}
          />
          <label htmlFor="age">Age (Years)</label>
          <input
            id="age"
            type="number"
            ref={ageInputRef}
          />
          <Button type="submit">Add User</Button>
        </form>
      </Card>
    </div>
  );
};

export default AddUser;

```

## 106. Controlled vs Uncontrolled Components

- **Uncontrolled Components** - values accessed with a ref. Their internal value is not controlled by React. We rely on the input and we just fetch it. We dont feed data back to the input. The native state is utilized by the input element.
- **Controlled component** - has its own internal state controlled by react

# 10. Advanced: Handling Side Effects, Reducers, Context API

## 109. Side Effects, useEffect

- main job of react is to render UI and react to user input
- **side effects** are everything else (e.g. http requests or storing things inside browser storage, utilizing timers, etc.). These happen outside component evaluation and render cycle, especially since they may block or delay rendering
- **useEffect()** hook is a special hook to handle side effects


## 110. UseEffect() hook

```jsx
function App() {
  const [isLoggedIn, setIsLoggedIn] = 
     ...
  useEffect(() => {
    const storedUserLoggedIn = localStorage.getItem('isLoggedIn');
    if (storedUserLoggedIn === '1') {
      setIsLoggedIn(true);
    }
  }, []);
    ...
}
```

## 111. UseEffect() and dependencies

```jsx
	# trigger every time the enteredEmail or enteredPassword change
  useEffect(() => {
    setFormIsValid(
      enteredEmail.includes('@') && enteredPassword.trim().length > 6
    )
  }, [enteredEmail, enteredPassword])
```

- you can use as dependencies:
  - **state**
  - **variables**
  - **props**
  - **functions** 
  - all has to be defined inside the components

## 113. UseEffect Cleanup Function

- **Debouncing**
- cleanup runs when the function is run again or component is removed from the dom
- with empty dependency array the cleanup runs only when the component is removed

```jsx
  useEffect(() => {
    const identifier = setTimeout(() => {
      setFormIsValid(
        enteredEmail.includes('@') && enteredPassword.trim().length > 6
      )
    }, 500)

    return () => {
      console.log('CLEANUP');
      clearTimeout(identifier);
    }
  }, [enteredEmail, enteredPassword])
```

## 115. UseReducer() Hook

- useful for more complex state
- its a replacement if you need more powerful state management
- for majority of cases you will use useState
- its good to use if you have two states that are related or if you update state that depend on other state

```jsx
import React, { useState, useEffect, useReducer } from 'react';

import Card from '../UI/Card/Card';
import classes from './Login.module.css';
import Button from '../UI/Button/Button';

const emailReducer = (state, action) => {
  if (action.type === 'USER_INPUT') {
    return {
      value: action.val,
      isValid: action.val.includes('@')
    }
  }

  if (action.type === 'INPUT_BLUR') {
    return {
      value: state.value,
      isValid: state.value.includes('@')
    }
  }

  return {
    value: '',
    isValid: ''
  }
}

const passwordReducer = (state, action) => {
  if (action.type === 'USER_INPUT') {
    return {
      value: action.value,
      isValid: action.value.trim().length > 6
    }
  }

  if (action.type === 'INPUT_BLUR') {
    return {
      value: state.value,
      isValid: state.value.trim().length > 6
    }
  }

  return {
    value: '',
    isValid: ''
  }
}

const Login = (props) => {
  const [formIsValid, setFormIsValid] = useState(false);
  const [emailState, dispatchEmail] = useReducer(
    emailReducer,
    {value: '', isValid: null}
  );
  const [passwordState, dispatchPassword] = useReducer(
    passwordReducer,
    {value: '', isValid: null}
  )

  const { isValid: emailIsValid } = emailState;  # Using destructuring for more concrete useEffect
  const { isValid: passwordIsValid } = passwordState;  # Using destructuring for more concrete useEffect

  useEffect(() => {
    const identifier = setTimeout(() => {
      console.log('CHecking form validity!');
      setFormIsValid(emailIsValid && passwordIsValid);
    }, 500)

    return () => {
      console.log('CLEANUP');
      clearTimeout(identifier);
    }
  }, [emailIsValid, passwordIsValid])

  const emailChangeHandler = (event) => {
    dispatchEmail({type: 'USER_INPUT', val: event.target.value})

    setFormIsValid(
      event.target.value.includes('@') && passwordState.isValid
    );
  };

  const passwordChangeHandler = (event) => {
    dispatchPassword({type: 'USER_INPUT', value: event.target.value});

    setFormIsValid(
      event.target.value.trim().length > 6 && emailState.isValid
    );
  };

  const validateEmailHandler = () => {
    dispatchEmail({type: 'INPUT_BLUR'});
  };

  const validatePasswordHandler = () => {
    dispatchPassword({type: 'INPUT_BLUR'});
  };

  const submitHandler = (event) => {
    event.preventDefault();
    props.onLogin(emailState.value, passwordState.value);
  };

  return (
    <Card className={classes.login}>
      <form onSubmit={submitHandler}>
        <div
          className={`${classes.control} ${
            emailState.isValid === false ? classes.invalid : ''
          }`}
        >
          <label htmlFor="email">E-Mail</label>
          <input
            type="email"
            id="email"
            value={emailState.value}
            onChange={emailChangeHandler}
            onBlur={validateEmailHandler}
          />
        </div>
        <div
          className={`${classes.control} ${
            passwordState.isValid === false ? classes.invalid : ''
          }`}
        >
          <label htmlFor="password">Password</label>
          <input
            type="password"
            id="password"
            value={passwordState.value}
            onChange={passwordChangeHandler}
            onBlur={validatePasswordHandler}
          />
        </div>
        <div className={classes.actions}>
          <Button type="submit" className={classes.btn} disabled={!formIsValid}>
            Login
          </Button>
        </div>
      </form>
    </Card>
  );
};

export default Login;

```



## 120. React Context

- useful when you pass a lot of state through a lot of components
- we have the component-wide **State Storage**
- You need to

  - **Create it**

```jsx
# src/store/auth-context.js
import React from 'react';

const AuthContext = React.createContext({
  isLoggedIn: false,
});

export default AuthContext;
```

- **Provide it**

```jsx
function App() {
    ...

  return (
    <AuthContext.Provider 
    value={{isLoggedIn: isLoggedIn, onLogout: logoutHandler}} >
      <MainHeader />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </AuthContext.Provider>
  );
}

export default App;
```

- **Hook into it** (consume it)
  - the first way

```jsx
  import React from 'react';
  import AuthContext from '../../store/auth-context';
  
  import classes from './Navigation.module.css';
  
  const Navigation = (props) => {
    return (
      <AuthContext.Consumer>
        {(ctx) => {
          return (
          <nav className={classes.nav}>
            <ul>
              {ctx.isLoggedIn && (
                <li>
                  <a href="/">Users</a>
                </li>
              )}
              {ctx.isLoggedIn && (
                <li>
                  <a href="/">Admin</a>
                </li>
              )}
              {ctx.isLoggedIn && (
                <li>
                  <button onClick={props.onLogout}>Logout</button>
                </li>
              )}
            </ul>
          </nav>
          )
        }}
        
      </AuthContext.Consumer>
    );
  };
  
  export default Navigation;
  
  
```

  The second, preferred way:

  ```jsx
  import React, { useContext } from 'react';
  import AuthContext from '../../store/auth-context';
  
  import classes from './Navigation.module.css';
  
  const Navigation = (props) => {
    const ctx = useContext(AuthContext);
    
    return (
      <nav className={classes.nav}>
        <ul>
          {ctx.isLoggedIn && (
            <li>
              <a href="/">Users</a>
            </li>
          )}
          {ctx.isLoggedIn && (
            <li>
              <a href="/">Admin</a>
            </li>
          )}
          {ctx.isLoggedIn && (
            <li>
              <button onClick={props.onLogout}>Logout</button>
            </li>
          )}
        </ul>
      </nav>
    );
  };
  
  export default Navigation;
  
  ```

  ## 123. Making context dynamic

## 125. Context Limitations

- not optimized for high frequency changes
  - e.g. state changes every second
  - so good for themes / login
  - redux is the alternative for faster updates
- Context shouldnt be used to replace all component communications

## 126. Rules of Hooks

- Only call hooks (all use... functions) in component functions
- Only call hooks at the top level of the functions
  - dont call them in nested functions or block statements
- Always add everything you refer to inside the **useEffect** hook as a dependency unless there is a good reason for that

## 128. Diving into forwardRefs

- avoid at all costs, but useful with focusing and scrolling often

```jsx
import React, { useRef, useImperativeHandle } from 'react';

import classes from './Input.module.css';

const Input = React.forwardRef((props, ref) => {
  const inputRef = useRef();

  const activate = () => {
    inputRef.current.focus();
  }

  useImperativeHandle(ref, () => {
    return {
      focus: activate
    }
  }) 

  return (
    <div
      className={`${classes.control} ${
        props.isValid === false ? classes.invalid : ''
      }`}
    >
      <label htmlFor={props.id}>{props.label}</label>
      <input
        ref={inputRef}
        type={props.type}
        id={props.id}
        value={props.value}
        onChange={props.onChange}
        onBlur={props.onBlur}
      />
    </div>
  );
});

export default Input;
```

```jsx
import React, { useState, useEffect, useReducer, useContext, useRef } from 'react';

import Card from '../UI/Card/Card';
import classes from './Login.module.css';
import Button from '../UI/Button/Button';
import AuthContext from '../../store/auth-context';
import Input from '../UI/Input/Input';

const emailReducer = (state, action) => {
  if (action.type === 'USER_INPUT') {
    return {
      value: action.val,
      isValid: action.val.includes('@')
    }
  }

  if (action.type === 'INPUT_BLUR') {
    return {
      value: state.value,
      isValid: state.value.includes('@')
    }
  }

  return {
    value: '',
    isValid: ''
  }
}

const passwordReducer = (state, action) => {
  if (action.type === 'USER_INPUT') {
    return {
      value: action.value,
      isValid: action.value.trim().length > 6
    }
  }

  if (action.type === 'INPUT_BLUR') {
    return {
      value: state.value,
      isValid: state.value.trim().length > 6
    }
  }

  return {
    value: '',
    isValid: ''
  }
}

const Login = () => {
  const authCtx = useContext(AuthContext);

  const emailInputRef = useRef();
  const passwordInputRef = useRef();

  const [formIsValid, setFormIsValid] = useState(false);
  const [emailState, dispatchEmail] = useReducer(
    emailReducer,
    {value: '', isValid: null}
  );
  const [passwordState, dispatchPassword] = useReducer(
    passwordReducer,
    {value: '', isValid: null}
  )

  const { isValid: emailIsValid } = emailState;
  const { isValid: passwordIsValid } = passwordState;

  useEffect(() => {
    const identifier = setTimeout(() => {
      console.log('CHecking form validity!');
      setFormIsValid(emailIsValid && passwordIsValid);
    }, 500)

    return () => {
      console.log('CLEANUP');
      clearTimeout(identifier);
    }
  }, [emailIsValid, passwordIsValid])

  const emailChangeHandler = (event) => {
    dispatchEmail({type: 'USER_INPUT', val: event.target.value})

    setFormIsValid(
      event.target.value.includes('@') && passwordState.isValid
    );
  };

  const passwordChangeHandler = (event) => {
    dispatchPassword({type: 'USER_INPUT', value: event.target.value});

    setFormIsValid(
      event.target.value.trim().length > 6 && emailState.isValid
    );
  };

  const validateEmailHandler = () => {
    dispatchEmail({type: 'INPUT_BLUR'});
  };

  const validatePasswordHandler = () => {
    dispatchPassword({type: 'INPUT_BLUR'});
  };

  const submitHandler = (event) => {
    event.preventDefault();
    if (formIsValid) {
      authCtx.onLogin(emailState.value, passwordState.value);
    } else if (!emailIsValid) {
      emailInputRef.current.focus();
    } else {
      passwordInputRef.current.focus();
    }
  };

  return (
    <Card className={classes.login}>
      <form onSubmit={submitHandler}>
        <Input
          ref={emailInputRef}
          id='email' 
          label='E-Mail' 
          type='email' 
          isValid={emailIsValid} 
          value={emailState.value} 
          onChange={emailChangeHandler} 
          onBlur={validateEmailHandler} />
        <Input
          ref={passwordInputRef}
          id='password'
          label='password'
          type='password'
          isValid='passwordIsValid'
          value={passwordState.value}
          onChange={passwordChangeHandler}
          onBlur={validatePasswordHandler} />
        <div className={classes.actions}>
          <Button type="submit" className={classes.btn}>
            Login
          </Button>
        </div>
      </form>
    </Card>
  );
};

export default Login;

```

# 11. Practice Project - food order app

## 132.  Adding header

- to add Image

  ```jsx
  import React, { Fragment } from 'react';
  import mealsImage from '../../assets/meals.jpg';
  import classes from './Header.module.css';
  
  const Header = props => {
    return (
      <Fragment>
        <header className={classes.header}>
          <h1>ReactMeals</h1>
          <button>Cart</button>
        </header>
        <div className={classes['main-image']}>
          <img src={mealsImage} alt="A table full of delicious food!" />
        </div>
      </Fragment>
    );
  };
  
  export default Header;
  ```

  

# 12. A Look Behind The Scenes Of  Optimization Techniques

  ## 151. How does React work?

- JS library for building UI
- Component based
- **ReactDOM** is interface to the web. It is responsible for working with the real **DOM**
- React uses **Virtual DOM**. This determines how does the component tree looks like and what it should look like after the component update. ReactDOM then knows what to update.
- Whenever state, props, or a context of component changes that component is reevaluated. But that is not re-rendering. Real DOM is updated only where it changes. 
  - all its child components are also revaluated

## 154. Preventing Unnecessary Re-Evaluations with React.memo()

- this tells react to check the props, and only if props changed reevaluate component.
- If the parent changed but the prop did not change the execution will be skipped.
- this optimization comes at a cost. You're trading the performance cost of reevaluating a component for a performance cost of performing the comparison. Cost depends on the complexity of the component, number of props, number of children etc. It is a great tool if you wanna avoid the reevaluation of an entire tree at the top of the tree though.
- If the props usually change anyways then it does not make sense.
- For small component trees its probably not worth it.
- You wanna pick some key parts in the component tree that allows you to cut off the entire branch.
- keep in mind that passing a handler as props means the function will recreate when the parent changes. Which means the memo wont work.

```jsx
import React from "react";

import MyParagraph from "./MyParagraph";

const DemoOutput = (props) => {
  console.log('DemoOutput RUNNING');
  return (
    <MyParagraph>{props.show ? 'This is new!' : ''}</MyParagraph>
  );
};

export default React.memo(DemoOutput);
```

## 155. Preventing Function Re-Creation with useCallback()

- **useCallback** says we want to save a function and it should not recreate with each execution
- just wrap a function to save and add array of dependencies

```jsx
import React, { useState, useCallback } from 'react';
import Button from '../src/components/UI/Button/Button';

import './App.css';
import DemoOutput from './components/Demo/DemoOutput';

function App() {
  const [showParagraph, setShowParagraph] = useState(false);

  console.log('APP RUNNING');

  const toggleParagraphHandler = useCallback(() => {  # use callback
    setShowParagraph((prevShowParagraph) => !prevShowParagraph);
  }, []);

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={false} />
      <Button onClick={toggleParagraphHandler}>Show Paragraph!</Button>
    </div>
  );
}

export default App;
```

## 156. useCallback() and its dependencies

- the function is saved exactly as it is, so if something internal to that function changes we need to set up dependencies.

```jsx
import React, { useState, useCallback } from 'react';
import Button from '../src/components/UI/Button/Button';

import './App.css';
import DemoOutput from './components/Demo/DemoOutput';

function App() {
  const [showParagraph, setShowParagraph] = useState(false);
  const [allowToggle, setAllowToggle] = useState(false);

  console.log('APP RUNNING');

  const toggleParagraphHandler = useCallback(() => {
    if (allowToggle) {
      setShowParagraph((prevShowParagraph) => !prevShowParagraph);
    }
  }, [allowToggle]);

  const allowToggleHandler = () => {
    setAllowToggle(true);
  }

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={showParagraph} />
      <Button onClick={allowToggleHandler}>Allow Toggling</Button>
      <Button onClick={toggleParagraphHandler}>Show Paragraph!</Button>
    </div>
  );
}

export default App;
```

## 158. A Closer Look at State & Components

- the state is initiali zed only for the first run, for others run it does not unless the component was removed from DOM.

## 159. Understanding State Scheduling & Batching

- state changes are processed almost instantly but react reserves right to postpone the state changs. It guarantees the order tho.

## 160. Optimizing with useMemo

- to store objects and rerun them only if arguments changed
- good for for example sorting
- can be used for other objects such as arrays etc with empty dependency array

```jsx
# this function will only rerun if items props changes
const sortedList = useMemo(() => {
    return items.sort((a, b) => a - b);
}, [items]) 
```

# 13. Class-based components

TODO: optional

# 14. HTTP Requests

## 173. How to (Not) connect to the database

- React app does not talk to the database directly
- Separated back-end and front-end

## 175. Sending a GET request

- you can use **axios** or **fetch API** (native browser)

## 176. Using async / await

- a bit easier to read

```jsx
  async function fetchMoviesHandler() {
    const response = await fetch('https://swapi.dev/api/films');
    const data = await response.json();
    
    const transformedMovies = data.results.map(movie => {
      return {
        id: movie.episode_id,
        title: movie.title,
        openingText: movie.opening_crawl,
        releaseDate: movie.release_date
      }
    });
    setMovies(transformedMovies);
  }
```

## 178. Handlig HTTP Errors

```jsx
import React, { useState } from 'react';

import MoviesList from './components/MoviesList';
import './App.css';

function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  async function fetchMoviesHandler() {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch('https://swapi.dev/api/films/');

      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();
      
      const transformedMovies = data.results.map(movie => {
        return {
          id: movie.episode_id,
          title: movie.title,
          openingText: movie.opening_crawl,
          releaseDate: movie.release_date
        }
      });
      setMovies(transformedMovies);
      setIsLoading(false);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  }

  let content = <p>Found no movies.</p>;

  if (movies.length > 0) {
    content = <MoviesList movies={movies} />
  }

  if (error) {
    content = <p>{error}</p>;
  }
  if (isLoading) {
    content = <p>Lading...</p>;
  }

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchMoviesHandler}>Fetch Movies</button>
      </section>
      <section>
        {content}
      </section>
    </React.Fragment>
  );
}

export default App;

```

# 15. Building Custom React Hooks

- they can use react hooks and react state
- the custom hook function **has** to start with **use...**
- if you use **useEffect** or **useState** in the custom hook, it will get tied to the components its used in
- the custom hooks are generally a good idea for implementation in places where you need to abstract some reused logic that utilizes state/hooks

```jsx
# use-counter.js
import { useState, useEffect } from 'react';

const useCounter = () => {
  const [counter, setCounter] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCounter((prevCounter) => prevCounter + 1);
    }, 1000);

    return () => clearInterval(interval);
  }, []);

  return counter;
}

export default useCounter;
```

```jsx
# usage
import Card from './Card';
import useCounter from '../hooks/use-counter';

const ForwardCounter = () => {
  const counter = useCounter();

  return <Card>{counter}</Card>;
};

export default ForwardCounter;
```

example of a custom hook:

```jsx
# use-http.js
import React, { useState, useCallback } from 'react';

const useHttp = () => {
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const sendRequest = useCallback(async (requestConfig, applyData) => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch(requestConfig.url, {
        method: requestConfig.method ? requestConfig.method : 'GET',
        headers: requestConfig.headers ? requestConfig.headers : {},
        body: requestConfig.body ? JSON.stringify(requestConfig.body) : null,
      });

      if (!response.ok) {
        throw new Error('Request failed!');
      }

      const data = await response.json();
      applyData(data);
    } catch (err) {
      setError(err.message || 'Something went wrong!');
    }
    setIsLoading(false);
  }, []);

  return {
    isLoading,
    error,
    sendRequest
  };
};

export default useHttp;
```

example of a form input custom hook:

```jsx
# use-input.js
import { useState } from 'react';

const useInput = (validateValue) => {
  const [value, setValue] = useState('');
  const [isTouched, setIsTouched] = useState(false);

  const valueIsValid = validateValue(value);
  const hasError = !valueIsValid && isTouched;

  const valueChangeHandler = event => {
    setValue(event.target.value);
  };

  const inputBlurHandler = () => {
    setIsTouched(true);
  };

  const reset = () => {
    setValue('');
    setIsTouched(false);
  }


  return {
    value,
    isValid: valueIsValid,
    hasError,
    valueChangeHandler,
    inputBlurHandler,
    reset
  }
}

export default useInput;
```

```jsx
# form component
import { useEffect, useState } from 'react';

import useInput from '../hooks/use-input';

const SimpleInput = (props) => {
  const  { 
    value: name, 
    isValid: nameIsValid,
    hasError: nameInputHasError, 
    valueChangeHandler: nameChangedHandler, 
    inputBlurHandler: nameBlurHandler,
    reset: resetName
  } = useInput((value) => {
    return value.trim() !== '';
  });

  const {
    value: email,
    isValid: emailIsValid,
    hasError: emailHasError,
    valueChangeHandler: emailChangeHandler,
    inputBlurHandler: emailBlurHandler,
    reset: resetEmail
  } = useInput((value) => {
    return value.includes('@');
  })

  const formIsValid = nameIsValid && emailIsValid;

  const formSubmissionHandler = event => {
    event.preventDefault();

    if (!nameIsValid || !emailIsValid) {
      return;
    }

    console.log(name);
    console.log(email);

    resetName();
    resetEmail();
  }


  const nameInputClasses = nameInputHasError ? 'form-control invalid' : 'form-control';
  const emailInputClasses = emailHasError ? 'form-control invalid' : 'form-control';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input 
          type='text' 
          id='name' 
          onChange={nameChangedHandler} 
          value={name}
          onBlur={nameBlurHandler} />
        {nameInputHasError && <p className="error-text">Name must not be empty.</p>}
      </div>
      <div className={emailInputClasses}>
        <label htmlFor='name'>Your Email</label>
        <input 
          type='email' 
          id='email' 
          onChange={emailChangeHandler} 
          value={email}
          onBlur={emailBlurHandler} />
        {emailHasError && <p className="error-text">Email must be valid.</p>}
      </div>
      <div className="form-actions">
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;
```



# 16. Forms & User input

# 18. Redux

## 225.  Another look at state

- Redux is **state management system** for cross-component or app-wide state
- consider also using **redux toolkit**
- can be used for any JS project, not just react
- 3 types of state
  - **local** - belongs to a single component
  - **cross-component** - affects multiple components, requires prop chains (prop drilling)
  - **app-wide** - affects the entire app (e.g. user authentication), also requires prop chains. 
  - for cross components or app-wide state we can use react context.

## 226. Context vs Redux

- context requires a complex setup and becomes cumbersome for bigger apps and you might end up with a lot of nested code / providers. For small to medium apps it might be ok.
- react context is for low frequency updates. So performance might become an issue.

## 227. How Redux Works

- one central **data store** (state) - you **never** have more than one store. So all the state goes here.
- components setup **subscriptions** to the central store, and whenever the data changes, the store notifies the components and they get a slice of the central data store.
- components **never** directly manipulate store data. For that we have **reducer function**. This function is responsible for mutating Store Data.
- the reducer should be a pure function that always receives the **old state** and **dispatch action** and returns a **new state** object (usually)
- components dispatch (trigger) **actions**. Actions are JS object describing operations reducer should perform.

## 228. Exploring the Cure Redux Components

```jsx
# Basic instance of Redux
const redux = require('redux');

const counterReducer = (state = { counter: 0 }, action) => {
  if (action.type === 'increment') {
    return {
      counter: state.counter + 1
    };
  } else if (action.type === 'decrement') {
    return {
      counter: state.counter - 1
    }
  } else {
    return state;
  }
};

const store = redux.createStore(counterReducer);

console.log(store.getState());

const counterSubscriber = () => {
  const latestState = store.getState();
  console.log(latestState);
}

store.subscribe(counterSubscriber);

store.dispatch({
  type: 'increment'
});
store.dispatch({
  type: 'decrement'
})
```

## 230. Preparing new project

`npm install redux react-redux`

- react-redux makes connecting to react very simple

## 231. Create a Redux Store for React

```jsx
import { createStore } from 'redux';

const counterReducer = (state = { counter: 0}, action) => {
  if (action.type === 'increment') {
    return {
      counter: state.counter + 1
    }
  } else if (action.type === 'decrement') {
    return {
      counter: state.counter - 1
    }
  } else {
    return state
  }
};

const store = createStore(counterReducer);

export default store;
```

Redux store example:

```jsx
# store/index.js
import { createStore } from 'redux';

const initialState = { counter: 0, showCounter: true };

export const INCREMENT = 'increment';

const counterReducer = (state = initialState, action) => {
  if (action.type === INCREMENT) {
    // always copy and output news objects, never mutate the old ones
    return {
      counter: state.counter + 1,
      showCounter: state.showCounter
    }
  } else if (action.type === 'increase') {
    return {
      counter: state.counter + action.amount,
      showCounter: state.showCounter
    }
  } else if (action.type === 'decrement') {
    return {
      counter: state.counter - 1,
      showCounter: state.showCounter
    }
  } else if (action.type === 'toggle') {
    return {
      counter: state.counter,
      showCounter: !state.showCounter
    }
  } else {
    return state
  }
};

const store = createStore(counterReducer);

export default store;
```

```jsx
# src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';

import './index.css';
import App from './App';
import store from './store/index';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root'));
```

```jsx
# Component.js
import { Component } from 'react';
import { useSelector, useDispatch, connect } from 'react-redux';
import { INCREMENT } from '../store/index';

import classes from './Counter.module.css';

const Counter = () => {
  const dispatch = useDispatch();
  const counter = useSelector(state => state.counter);
  const show = useSelector(state => state.showCounter);

  const incrementHandler = () => {
    dispatch({
      type: INCREMENT,
    });
  }

  const increaseHandler = (amount) => {
    dispatch({
      type: 'increase',
      amount: amount
    })
  }

  const decrementHandler = () => {
    dispatch({
      type: 'decrement'
    })
  }

  const toggleCounterHandler = () => {
    dispatch({
      type: 'toggle'
    })
  };

  return (
    <main className={classes.counter}>
      <h1>Redux Counter</h1>
      {show && <div className={classes.value}>{counter}</div>}
      <div>
        <button onClick={incrementHandler}>Increment</button>
        <button onClick={() => increaseHandler(10)}>Increase by 10</button>
        <button onClick={decrementHandler}>Decrement</button>
      </div>
      <button onClick={toggleCounterHandler}>Toggle Counter</button>
    </main>
  );
};

# Class approach
// class Counter extends Component {
//   incrementHandler() {
//     this.props.increment();
//   }

//   decrementHandler() {
//     this.props.decrement();
//   }

//   render() {
//     return (
//       <main className={classes.counter}>
//         <h1>Redux Counter</h1>
//         <div className={classes.value}>{this.props.counter}</div>
//         <div>
//           <button onClick={this.incrementHandler.bind(this)}>Increment</button>
//           <button onClick={this.decrementHandler.bind(this)}>Decrement</button>
//         </div>
//         <button onClick={this.toggleCounterHandler}>Toggle Counter</button>
//       </main>
//     );
//   }
// };

// const mapStateToProps = state => {
//   return {
//     counter: state.counter,
//   };
// }

// const mapDispatchToProps = dispatch => {
//   return {
//     increment: () => dispatch({type: 'increment'}),
//     decrement: () => dispatch({type: 'decrement'})
//   }
// }

// export default connect(mapStateToProps, mapDispatchToProps)(Counter);

export default Counter;
```

## 240. Utilizing redux toolkit

- `npm install @reduxjs/toolkit` - installs the toolkit. You can uninstall redux itself when installing this.

- **the toolkit utilizes a tool that automatically clones and edits the state so you can mutate the state directly.*

```jsx
# store/index.js
import { createSlice, configureStore } from '@reduxjs/toolkit';

const initialState = { counter: 0, showCounter: true };

const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment(state) {
      state.counter++;
    },
    decrement(state) {
      state.counter--;
    },
    increase(state, action) {
      state.counter = state.counter + action.payload
    },
    toggleCounter(state) {
      state.showCounter = !state.showCounter;
    }
  }
});

// Configure store merges the reducers
const store = configureStore({
  reducer: counterSlice.reducer
});

export const counterActions = counterSlice.actions;
export default store;
```

```jsx
# index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';

import './index.css';
import App from './App';
import store from './store/index';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root'));
```

```jsx
# component.js
import { useSelector, useDispatch } from 'react-redux';

import { counterActions } from '../store/index';
import classes from './Counter.module.css';

const Counter = () => {
  const dispatch = useDispatch();
  const counter = useSelector(state => state.counter);
  const show = useSelector(state => state.showCounter);

  const incrementHandler = () => {
    dispatch(counterActions.increment());
  }

  const increaseHandler = (amount) => {
    dispatch(counterActions.increase(amount));  // { type: uniq_identifier, payload: 10 }
  }

  const decrementHandler = () => {
    dispatch(counterActions.decrement());
  }

  const toggleCounterHandler = () => {
    dispatch(counterActions.toggleCounter());
  };

  return (
    <main className={classes.counter}>
      <h1>Redux Counter</h1>
      {show && <div className={classes.value}>{counter}</div>}
      <div>
        <button onClick={incrementHandler}>Increment</button>
        <button onClick={() => increaseHandler(10)}>Increase by 10</button>
        <button onClick={decrementHandler}>Decrement</button>
      </div>
      <button onClick={toggleCounterHandler}>Toggle Counter</button>
    </main>
  );
};

export default Counter;
```

# 19. Advanced Redux

## 249. Reducer & Side Effects

- Reducers must be **pure, side effects-free, synchronous functions**
- utilize **redux dev tools** for awesome debugging
- The same is true for the **useReducer** hook
- Where should we put side effects?
  - either ot the component, with **useEffect** for example.
  - or we write our own **action creators**

## 256. Using useEffect with Redux

```jsx
function App() {
  const showCart = useSelector(state => state.ui.cartIsVisible);
  const cart = useSelector((state) => state.cart);

  useEffect(() => {
    fetch('https://react-http-6a7a1-default-rtdb.europe-west1.firebasedatabase.app/cart.json', {
      method: 'PUT',
      body: JSON.stringify(cart)
    });
  }, [cart]);

  return (
    <Layout>
      {showCart && <Cart />}
      <Products />
    </Layout>
  );
}
```

## 259. Using action creator Thunk

- **Thunk** a function that delays an action until later
  - does not return an action itself but rather a function that eventually returns an action

```jsx
#cart-slice.js
import { createSlice } from "@reduxjs/toolkit";

const cartSlice = createSlice({
  name: 'cart',
  initialState: {
    items: [],
    totalQuantity: 0,
    changed: false,
  },
  reducers: {
    replaceCart(state, action) {
      state.totalQuantity = action.payload.totalQuantity;
      state.items = action.payload.items;
    },
    addItemToCart(state, action) {
      const newItem = action.payload;
      const existingItem = state.items.find(item => item.id === newItem.id)
      state.totalQuantity++;
      state.changed = true;
      if (!existingItem) {
        state.items.push({
          id: newItem.id,
          name: newItem.title,
          price: newItem.price,
          quantity: 1,
          totalPrice: newItem.price
        })
      } else {
        existingItem.quantity++;
        existingItem.totalPrice += newItem.price;
      }
    },
    removeItemFromCart(state, action) {
      const id = action.payload;
      const existingItem = state.items.find(item => item.id === id);
      state.totalQuantity--;
      state.changed = true;
      if (existingItem.quantity === 1) {
        state.items = state.items.filter((item) => item.id !== id)
      } else {
        existingItem.quantity--;
        existingItem.totalPrice -= existingItem.price;
      }
    }
  }
});

export const cartActions = cartSlice.actions;

export default cartSlice;
```



```jsx
#cart-actions.js
import { uiActions } from "./ui-slice";
import { cartActions } from './cart-slice';

const URL = 'https://react-http-6a7a1-default-rtdb.europe-west1.firebasedatabase.app/cart.json';

export const fetchCartData = () => {
  return async (dispatch) => {
    const fetchData = async () => {
      const response = await fetch(URL);

      if (!response.ok) {
        throw new Error('Could not fetch cart data!');
      }
  
      const data = await response.json();
  
      return data;
    };

    try { 
      const cartData = await fetchData();
      dispatch(cartActions.replaceCart({
        items: cartData.items || [],
        totalQuantity: cartData.totalQuantity
      }));
    } catch(error) {
      dispatch(
        uiActions.showNotification({
          status: 'error',
          title: 'Error!',
          message: 'Fetching cart data failed!'
        })
      )
    }
  }
}

export const sendCartData = (cart) => {
  return async (dispatch) => {
    dispatch(uiActions.showNotification({
      status: 'pending',
      title: 'Sending',
      message: 'Sending cart data...'
    }));

    const sendRequest = async () => {
      const response = await fetch(URL, {
        method: 'PUT',
        body: JSON.stringify({items: cart.items, totalQuantity: cart.totalQuantity})
      });
  
      if (!response.ok) {
        throw new Error('Sending cart data failed.');
      }
    };

    try {
      await sendRequest();
      dispatch(uiActions.showNotification({
        status: 'success',
        title: 'Success',
        message: 'Sent cart data'
      }));
    } catch (error) {
      dispatch(uiActions.showNotification({
        status: 'error',
        title: 'Error!',
        message: 'Sending cart data failed!'
      }));
    }
  }
};
```



```jsx
# app.js
import { useEffect, Fragment } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import Cart from './components/Cart/Cart';
import Layout from './components/Layout/Layout';
import Products from './components/Shop/Products';
import Notification from './components/UI/Notification';
import { fetchCartData, sendCartData } from './store/cart-actions';

let isInitial = true;

function App() {
  const dispatch = useDispatch();
  const showCart = useSelector(state => state.ui.cartIsVisible);
  const cart = useSelector((state) => state.cart);
  const notification = useSelector(state => state.ui.notification);

  useEffect(() => {
    dispatch(fetchCartData());
  }, [dispatch])

  useEffect(() => {
    if (isInitial) {
      isInitial = false;
      return;
    }

    if (cart.changed) {
      dispatch(sendCartData(cart));
    }
  }, [cart, dispatch]);

  return (
    <Fragment>
      {notification && <Notification
        status={notification.status}
        title={notification.title}
        message={notification.message} />}
      <Layout>
        {showCart && <Cart />}
        <Products />
      </Layout>
    </Fragment>
  );
}

export default App;
```

# 20. SPA with React Router

## 256. What is routing and Why?

- `npm install react-router-dom`

## 269 Defining and using routes

```jsx
# App.js
import {Route}  from 'react-router-dom';
import Welcome from './pages/Welcome';
import Products from './pages/Products';

function App() {
  return (
    <div>
      <Route path="/welcome">
        <Welcome />
      </Route>
      <Route path="/products">
        <Products />
      </Route>
    </div>
  );
}

export default App;

```

```jsx
# index.js
import ReactDOM from 'react-dom';
import {BrowserRouter} from 'react-router-dom';

import './index.css';
import App from './App';

ReactDOM.render(
<BrowserRouter>
  <App />
</BrowserRouter>
, document.getElementById('root'));
```

## 270. Working with Links

```jsx
import React from 'react';
import { Link } from 'react-router-dom';

const MainHeader = () => {
  return (
    <header>
      <ul>
        <li>
          <Link to="/welcome">Welcome</Link>
        </li>
        <li>
          <Link to="/products">Products</Link>
        </li>
      </ul>
    </header>
  );
};

export default MainHeader;
```

## 271. Using NavLinks

```jsx
import React from 'react';
import { NavLink } from 'react-router-dom';

import classes from './MainHeader.module.css';

const MainHeader = () => {
  return (
    <header className={classes.header}>
      <ul>
        <li>
          <NavLink activeClassName={classes.active} to="/welcome">Welcome</NavLink>
        </li>
        <li>
          <NavLink activeClassName={classes.active} to="/products">Products</NavLink>
        </li>
      </ul>
    </header>
  );
};

export default MainHeader;
```

## 272. Dynamic routing

```jsx
# App.js
import {Route}  from 'react-router-dom';
import Welcome from './pages/Welcome';
import Products from './pages/Products';
import MainHeader from './components/MainHeader';
import ProductDetail from './pages/ProductDetail';

function App() {
  return (
    <div>
      <MainHeader />
      <main>
        <Route path="/welcome">
          <Welcome />
        </Route>
        <Route path="/products">
          <Products />
        </Route>
        <Route path="/product-detail/:productId">
          <ProductDetail />
        </Route>
      </main>
    </div>
  );
}

export default App;
```

```jsx
# ProductDetails.js
import { useParams } from 'react-router';

import React from 'react';

const ProductDetail = () => {
  const params = useParams();

  return (
    <section>
      <h1>Product Detail</h1>
      <p>{params.productId}</p>
    </section>
  );
};

export default ProductDetail;
```

## 274. Using Switch + Exact

```jsx
# App.js
import {Route, Switch}  from 'react-router-dom';
import Welcome from './pages/Welcome';
import Products from './pages/Products';
import MainHeader from './components/MainHeader';
import ProductDetail from './pages/ProductDetail';
import { Fragment } from 'react';

function App() {
  return (
    <Fragment>
      <MainHeader />
      <main>
        <Switch>
          <Route path="/welcome">
            <Welcome />
          </Route>
          <Route path="/products" exact>
            <Products />
          </Route>
          <Route path="/products/:productId">
            <ProductDetail />
          </Route>
        </Switch>
      </main>
    </Fragment>
  );
}

export default App;

```

## 275. Nested Routes

- we can use routes in any component

```jsx
import React from 'react';
import { Route } from 'react-router-dom'

function Welcome(props) {
  return (
    <section>
      <h1>The Welcome Page</h1>
      <Route path='/welcome/new-user'>
        <p>Welcome, new user!</p>
      </Route>
    </section>
  );
}

export default Welcome;
```

## 276. Redirecting the user

```jsx
import {Route, Switch, Redirect}  from 'react-router-dom';
import Welcome from './pages/Welcome';
import Products from './pages/Products';
import MainHeader from './components/MainHeader';
import ProductDetail from './pages/ProductDetail';
import { Fragment } from 'react';

function App() {
  return (
    <Fragment>
      <MainHeader />
      <main>
        <Switch>
          <Route path='/' exact>
            <Redirect to='/welcome' />
          </Route>
          <Route path="/welcome">
            <Welcome />
          </Route>
          <Route path="/products" exact>
            <Products />
          </Route>
          <Route path="/products/:productId">
            <ProductDetail />
          </Route>
        </Switch>
      </main>
    </Fragment>
  );
}

export default App;
```

## 277. Nested routes

```jsx
import React, { Fragment } from 'react';
import { useParams, Route } from 'react-router';
import Comments from '../components/comments/Comments';



const QuoteDetails = () => {
  const params = useParams();

  console.log(params.quoteId);

  return (
    <Fragment>
      <h1>Quote Detail Page</h1>
      <Route path={`/quotes/${params.quoteId}/comments`}>
        <Comments />
      </Route>
    </Fragment>
  );
};

export default QuoteDetails;
```

## 282. Adding not found page

```jsx
import { Route, Switch, Redirect } from 'react-router-dom';
import Layout from './components/layout/Layout';
import AllQuotes from './pages/AllQuotes';
import NewQuote from './pages/NewQuote';
import NotFound from './pages/NotFound';
import QuoteDetails from './pages/QuoteDetails';

function App() {
  return (
    <Layout>
      <Switch>
        <Route path='/' exact>
          <Redirect to='/quotes' />
        </Route>
        <Route path='/quotes' exact>
          <AllQuotes />
        </Route>
        <Route path='/quotes/:quoteId'>
          <QuoteDetails />
        </Route>
        <Route path='/new-quote'>
          <NewQuote />
        </Route>
        <Route path='*'>
          <NotFound />
        </Route>
      </Switch>
    </Layout>
  );
}

export default App;
```

## 283. Implementic programmatic navigation

- **history.push()** pushes the link on the stack so user can use go back feature
- **history.repalce()** replaces the current url so user cannot go back

```jsx
import { useHistory } from 'react-router-dom';
import React from 'react';
import QuoteForm from '../components/quotes/QuoteForm';

const NewQuote = () => {
  const history = useHistory();

  const addQuoteHandler = (quoteData) => {
    console.log(quoteData);

    history.push('/quotes')
  }

  return (
    <QuoteForm onAddQuote={addQuoteHandler} />
  );
};

export default NewQuote;
```

## 284. Prevent unwanted redirects with prompt

```jsx
import { Fragment, useRef, useState } from 'react';
import { Prompt } from 'react-router';

import Card from '../UI/Card';
import LoadingSpinner from '../UI/LoadingSpinner';
import classes from './QuoteForm.module.css';

const QuoteForm = (props) => {
  const [isEntering, setIsEntering] = useState(false);

  const authorInputRef = useRef();
  const textInputRef = useRef();

  function submitFormHandler(event) {
    event.preventDefault();

    const enteredAuthor = authorInputRef.current.value;
    const enteredText = textInputRef.current.value;

    // optional: Could validate here

    props.onAddQuote({ author: enteredAuthor, text: enteredText });
  }

  const formFocusHandler = () => {
    setIsEntering(true);
  };

  const finishEnteringHandler = () => {
    setIsEntering(false);
  }

  return (
    <Fragment>
      <Prompt when={isEntering} message={(location) => 'Are you sure you want to leave? All your entered data will be lost'} />
      <Card>
        <form onFocus={formFocusHandler} className={classes.form} onSubmit={submitFormHandler}>
          {props.isLoading && (
            <div className={classes.loading}>
              <LoadingSpinner />
            </div>
          )}

          <div className={classes.control}>
            <label htmlFor='author'>Author</label>
            <input type='text' id='author' ref={authorInputRef} />
          </div>
          <div className={classes.control}>
            <label htmlFor='text'>Text</label>
            <textarea id='text' rows='5' ref={textInputRef}></textarea>
          </div>
          <div className={classes.actions}>
            <button onClick={finishEnteringHandler} className='btn'>Add Quote</button>
          </div>
        </form>
      </Card>
    </Fragment>
  );
};

export default QuoteForm;
```

## 285. Query Parameters

```jsx
import { Fragment } from 'react';
import { useHistory, useLocation } from 'react-router';

import QuoteItem from './QuoteItem';
import classes from './QuoteList.module.css';

const sortQuotes = (quotes, ascending) => {
  return quotes.sort((quoteA, quoteB) => {
    if (ascending) {
      return quoteA.id > quoteB.id ? 1 : -1;
    } else {
      return quoteA.id < quoteB.id ? 1 : -1;
    }
  });
};

const QuoteList = (props) => {
  const history = useHistory();
  const location = useLocation();

  const queryParams = new URLSearchParams(location.search);

  const isSortingAscending = queryParams.get('sort') === 'asc';

  const sortedQuotes = sortQuotes(props.quotes, isSortingAscending);
  
  const changeSortingHandler = () => {
    history.push('/quotes?sort=' + (isSortingAscending ? 'desc' : 'asc'))
  };

  return (
    <Fragment>
      <div className={classes.sorting}>
        <button onClick={changeSortingHandler}>Sort {isSortingAscending ? 'Descending' : 'Ascending'}</button>
      </div>
      <ul className={classes.list}>
        {sortedQuotes.map((quote) => (
          <QuoteItem
            key={quote.id}
            id={quote.id}
            author={quote.author}
            text={quote.text}
          />
        ))}
      </ul>
    </Fragment>
  );
};

export default QuoteList;
```

## 286. Writing more flexible react router code

```jsx
import { Fragment } from 'react';
import { useHistory, useLocation } from 'react-router';

import QuoteItem from './QuoteItem';
import classes from './QuoteList.module.css';

const sortQuotes = (quotes, ascending) => {
  return quotes.sort((quoteA, quoteB) => {
    if (ascending) {
      return quoteA.id > quoteB.id ? 1 : -1;
    } else {
      return quoteA.id < quoteB.id ? 1 : -1;
    }
  });
};

const QuoteList = (props) => {
  const history = useHistory();
  const location = useLocation();

  const queryParams = new URLSearchParams(location.search);

  const isSortingAscending = queryParams.get('sort') === 'asc';

  const sortedQuotes = sortQuotes(props.quotes, isSortingAscending);
  
  # Here
  const changeSortingHandler = () => {
    history.push({
      pathname: location.pathname,
      search: `?sort=${(isSortingAscending ? 'desc': 'asc')}`
    })
  };

  return (
    <Fragment>
      <div className={classes.sorting}>
        <button onClick={changeSortingHandler}>Sort {isSortingAscending ? 'Descending' : 'Ascending'}</button>
      </div>
      <ul className={classes.list}>
        {sortedQuotes.map((quote) => (
          <QuoteItem
            key={quote.id}
            id={quote.id}
            author={quote.author}
            text={quote.text}
          />
        ))}
      </ul>
    </Fragment>
  );
};

export default QuoteList;

```

```jsx
import React, { Fragment } from 'react';
import { useParams, Route, Link, useRouteMatch } from 'react-router-dom';
import Comments from '../components/comments/Comments';
import HighlightedQuote from '../components/quotes/HighlightedQuote';

const DUMMY_DATA = [
  { id: 'q1', author: 'Max', text: 'Learning React is fun!'},
  { id: 'q2', author: 'Maxmilian', text: 'Learning React is great!'},
];

const QuoteDetails = () => {
  const params = useParams();
  const match = useRouteMatch();

  const quote = DUMMY_DATA.find((quote) => {
    return quote.id === params.quoteId;
  })

  if (!quote) {
    return <p>No quote found!</p>;
  }

  console.log(params.quoteId);

  return (
    <Fragment>
      <HighlightedQuote text={quote.text} author={quote.author} />
      <Route path={match.path} exact>
        <div className='centered'>
          <Link className='btn--flat' to={`${match.url}/comments`}>
            Load Comments
          </Link>
        </div>
      </Route>
      <Route path={`${match.path}/comments`}>
        <Comments />
      </Route>
    </Fragment>
  );
};

export default QuoteDetails;
```

# 21. Deploying React App

## 293. Deployment steps

- Test code
- Optimize code (lazy loading)
- Build App for Production
- Upload Production code to server
- Configure server

## 294. Adding lazy loading

- certain chunks of our code are loaded only when needed

```jsx
import React, { Suspense } from 'react';  # Suspense is important

import { Route, Switch, Redirect } from 'react-router-dom';
import Layout from './components/layout/Layout';
import LoadingSpinner from './components/UI/LoadingSpinner';

const NewQuote = React.lazy(() => import('./pages/NewQuote'));
const QuoteDetails = React.lazy(() => import('./pages/QuoteDetails'));
const NotFound = React.lazy(() => import('./pages/NotFound'));
const AllQuotes = React.lazy(() => import('./pages/AllQuotes'));

function App() {
  return (
    <Layout>
      <Suspense fallback={(
        <div className='centered'>
          <LoadingSpinner />
        </div>
      )}>
        <Switch>
          <Route path='/' exact>
            <Redirect to='/quotes' />
          </Route>
          <Route path='/quotes' exact>
            <AllQuotes />
          </Route>
          <Route path='/quotes/:quoteId'>
            <QuoteDetails />
          </Route>
          <Route path='/new-quote'>
            <NewQuote />
          </Route>
          <Route path='*'>
            <NotFound />
          </Route>
        </Switch>
      </Suspense>
    </Layout>
  );
}

export default App;
```

## 295. Building for production

- `npm run build`
  - creates a **build folder** that is all the code that you need to upload to your sever

## 296. Getting Started with deployment

- A react SPA is a **Static Website**
  - its only HTML, CSS and JS
  - there is no backend
- We need a **Static Site Host**, we don't need a provider that offers a backend services
- We will use **Firebase**
- `npm install -g firebase-tools`
- `firebase login`
- `firebase init` in the root folder of the project
  - go to hosting and click `space`to select
  - hit `enter` and chose whether to use existing project or create new one
  - it asks as what folder we want to use, we want to use the **build** folder
  - configure your server as url is always ignored and you always return SPA code, so yes on SPA build
  - do not overwrite index.html
- `firebase deploy`
- in the console you can configure to application
- `firebase hosting:disable`pulls the page down

# 23. Next.js

## 316. What it is and why use it

- Full-stack Framework for Production
- It adds a lot of missing features that solve common problems

## 317. Added features and benefits

- **Server-side rendering** (built-in)
  - preparing the content on the page on the server instead of the client
  - better SEO
  - search engines see what users see
  - fetches data on the server and renders finished pages
- **File-based routing**
  - Define pages and routes with file structure instead of code
- **Allows building full-stack apps**
  - you can add backend code
  - storing data, getting data, authentication etc can be added to your projects

## 320. Creating New Next.js Project and App

- need to have **node.js** installed
- `npx create-next-app`

## 325. Dynamic pages - extracting value

structure:

PAGES/

- index.js
- NEWS/
  - index.js
  - [newsId].js

```jsx
import { useRouter } from 'next/router';

const Detail = () => {
  const router = useRouter();

  const newsId = router.query.newsId;

  return (
    <h1>
      The Detail Page
    </h1>
  );
};

export default Detail;
```

## 336. Data fetching for static pages

- if you `npm run build`you can identify SSG page by **full dot**

```jsx
import React from 'react';
import MeetupList from '../components/meetups/MeetupList';

const DUMMY_MEETUPS = [
  {
    id: 'm1',
    title: "A first meetup",
    image: "https://upload.wikimedia.org/wikipedia/commons/d/d3/Stadtbild_M%C3%BCnchen.jpg",
    address: "Some address 5, 12345 Some City",
    description: "This is a first meetup!"
  },
  {
    id: 'm2',
    title: "A second meetup",
    image: "https://upload.wikimedia.org/wikipedia/commons/d/d3/Stadtbild_M%C3%BCnchen.jpg",
    address: "Some address 4, 12345 Some City",
    description: "This is a second meetup!"
  }
];

const HomePage = (props) => {
  return (
    <MeetupList meetups={props.meetups} />
  );
};

export async function getStaticProps() {
  // The code written here will be server side, it will never executed on the client side.
  // fetch data from an API or something
  // always need to return object here
  return {
    props: {
      meetups: DUMMY_MEETUPS
    }
  };
};

export default HomePage;
```

## 337. Incremental static generation

```jsx
export async function getStaticProps() {
  // The code written here will be server side, it will never executed on the client side.
  // fetch data from an API or something
  // always need to return object here
  return {
    props: {
      meetups: DUMMY_MEETUPS
    },
    // incremental static generation
    revalidate: 10
  };
};
```

## 338. Server-side rendering

- runs after deployment

```jsx
export async function getServerSideProps(context) {
  const req = context.req;
  const res = context.res;
  // fetch data from an API
  // this is slower because its not cached and reused
  // useful if you need req, res, or if you have data changing every second or so.
  // Rerenders the page for every request
  // runs on the server, not on the client
  return {
    props: {
      meetups: DUMMY_MEETUPS
    }
  }
}
```

## 340. getStaticPaths

- needed if you have **dynamic** page with **getStaticProps**

```jsx
import React, { Fragment, useContext } from 'react';
import MeetupDetail from '../../components/meetups/MeetupDetail';

const MeetupDetails = () => {

  return (
    <MeetupDetail
      image="https://upload.wikimedia.org/wikipedia/commons/d/d3/Stadtbild_M%C3%BCnchen.jpg"
      title="A first Meetup"
      address="Some address 5, 12345 Some City"
      description="This is a first meetup!"
    />
  );
};

export async function getStaticPaths() {
  return {
    fallback: false,  // means we defined all paths, in true case we can only define some paths
    paths: [
      {
        params: {
          meetupId: 'm1',
        }
      },
      {
        params: {
          meetupId: 'm2',
        }
      }
    ]
  }
}

export async function getStaticProps(context) {
  // fetch data for a single meetup

  const meetupId = context.params.meetupId;

  console.log(meetupId);

  return {
    props: {
      meetupData: {
        image: "https://upload.wikimedia.org/wikipedia/commons/d/d3/Stadtbild_M%C3%BCnchen.jpg",
        id: meetupId,
        title: 'First Meetup', 
        address: "Some address 5, 12345 Some City",
        description: "This is a first meetup!"
      }
    }
  }
}

export default MeetupDetails;
```

## ## 341. API Routes

- enable you to build your own endpoints
- run only on the server
- create folder **api** in **pages** folder

## 342. Working with mongoDB

- we need to create cluster first
- potentially rewatch the lecture

```jsx
import { MongoClient } from 'mongodb'

// /api/new-meetup

async function handler(req, res) {
  if (req.method === "POST") {
    const data = req.body;

    const client = await MongoClient.connect('mongodb+srv://honza:ngage@cluster0.iewhe.mongodb.net/meetups?retryWrites=true&w=majority');
    const db = client.db();

    const meetupsCollection = db.collection('meetups');

    const result = await meetupsCollection.insertOne(data);

    console.log(result);

    client.close();

    res.status(201).json({ message: 'Meetup inserted!' });
  }
};

export default handler;
```

# 24. Animating React Apps

## 353. CSS transitions

```css
.Modal {
    position: fixed;
    z-index: 200;
    border: 1px solid #eee;
    box-shadow: 0 2px 2px #ccc;
    background-color: white;
    padding: 10px;
    text-align: center;
    box-sizing: border-box;
    top: 30%;
    left: 25%;
    width: 50%;
    transition: all 0.3s ease-out;
}

.ModalOpen {
    opacity: 1;
    transform: translateY(0);
}

.ModalClosed {
    opacity: 0;
    transform: translateY(-100%);
}
```

## 354. Using CSS Animations

```css
.Modal {
    position: fixed;
    z-index: 200;
    border: 1px solid #eee;
    box-shadow: 0 2px 2px #ccc;
    background-color: white;
    padding: 10px;
    text-align: center;
    box-sizing: border-box;
    top: 30%;
    left: 25%;
    width: 50%;
    transition: all 0.3s ease-out;
}

.ModalOpen {
    animation: openModal 0.4s ease-out forwards;
}

.ModalClosed {
    animation: closeModal 0.4s ease-out forwards;
}

@keyframes openModal {
    0% {
        opacity: 0;
        transform: translateY(-100%);
    }

    50% {
        opacity: 1;
        transform: translateY(20%);
    }

    100% {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes closeModal {
    0% {
        opacity: 1;
        transform: translateY(0);
    }

    50% {
        opacity: 0.8;
        transform: translateY(60%);
    }

    100% {
        opacity: 0;
        transform: translateY(-100%);
    }
}
```

## 355. CSS Limitations

- the elements stay present
- removing the elements happens instantly and does not trigger animation

## 356. React Transition Group

```jsx
import React, { Component } from "react";
import Transition from "react-transition-group/Transition";

import "./App.css";
import Modal from "./components/Modal/Modal";
import Backdrop from "./components/Backdrop/Backdrop";
import List from "./components/List/List";

class App extends Component {
  state = {
    modalIsOpen: false,
    showBlock: false
  }

  showModal = () => {
    this.setState({
      modalIsOpen: true
    })
  }

  closeModal = () => {
    this.setState({
      modalIsOpen: false
    })
  }

  render() {
    return (
      <div className="App">
        <h1>React Animations</h1>
        <button onClick={() => this.setState(prevState => ({showBlock: !prevState.showBlock}))}>Toggle
        </button>
        <br />
          <Transition 
            in={this.state.showBlock}
            timeout={300}
            mountOnEnter
            unmountOnExit>
            {state => (
              <div 
                style={{
                  backgroundColor: 'red', 
                  width: 100, 
                  height: 100,
                  margin: 'auto',
                  transition: 'opacity 1s ease-out',
                  opacity: state === 'exiting' ? 0 : 1
                }}>
              </div> 
            )}
          </Transition>
        <Modal show={this.state.modalIsOpen} closed={this.closeModal} />
        <Backdrop show={this.state.modalIsOpen}/>
        <button className="Button" onClick={this.showModal}>Open Modal</button>
        <h3>Animating Lists</h3>
        <List />
      </div>
    );
  }
}

export default App;
```

## 361. Using CSSTransition

```jsx
import React from 'react';
import CSSTransition from 'react-transition-group/CSSTransition';

import './Modal.css';

const animationTiming = {
    enter: 400,
    exit: 1000
}

const modal = (props) => {
    return (
      <CSSTransition 
        in={props.show} 
        timeout={animationTiming}
        mountOnEnter
        unmountOnExit
        onEnter={() => console.log('onEnter')}
        onEntering={() => console.log('onEntering')}
        onEntered={() => console.log('onEntered')}
        onExit={() => console.log('onExit')}
        onExiting={() => console.log('onExiting')}
        onExited={() => console.log('onExited')}
        classNames="fade-slide">
        <div className="Modal">
            <h1>A Modal</h1>
            <button className="Button" onClick={props.closed}>Dismiss</button>
        </div>
      </CSSTransition>
    )
};

export default modal;
```

```css
.fade-slide-enter {

}

.fade-slide-enter-active {
    animation: openModal 0.4s ease-out forwards;
}

.fade-slide-exit {

}

.fade-slide-exit-active {
    animation: closeModal 1s ease-out forwards;
}

@keyframes openModal {
    0% {
        opacity: 0;
        transform: translateY(-100%);
    }

    50% {
        opacity: 1;
        transform: translateY(20%);
    }

    100% {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes closeModal {
    0% {
        opacity: 1;
        transform: translateY(0);
    }

    50% {
        opacity: 0.8;
        transform: translateY(60%);
    }

    100% {
        opacity: 0;
        transform: translateY(-100%);
    }
}
```

## 362. Customizing CSS Classnames

```jsx
import React from 'react';
import CSSTransition from 'react-transition-group/CSSTransition';

import './Modal.css';

const animationTiming = {
    enter: 400,
    exit: 1000
}

const modal = (props) => {
    return (
      <CSSTransition 
        in={props.show} 
        timeout={animationTiming}
        mountOnEnter
        unmountOnExit
        onEnter={() => console.log('onEnter')}
        onEntering={() => console.log('onEntering')}
        onEntered={() => console.log('onEntered')}
        onExit={() => console.log('onExit')}
        onExiting={() => console.log('onExiting')}
        onExited={() => console.log('onExited')}
        classNames={{
            enter: '',
            enterActive: 'ModalOpen',
            exit: '',
            exitActive: 'ModalClosed'
        }}>
        <div className="Modal">
            <h1>A Modal</h1>
            <button className="Button" onClick={props.closed}>Dismiss</button>
        </div>
      </CSSTransition>
    )
};

export default modal;
```

## 363. Animating Lists

```jsx
import React, { Component } from 'react';
import TransitionGroup from 'react-transition-group/TransitionGroup';
import CSSTransition from 'react-transition-group/CSSTransition';

import './List.css';

class List extends Component {
    state = {
        items: [1, 2, 3]
    }

    addItemHandler = () => {
        this.setState((prevState) => {
            return {
                items: prevState.items.concat(prevState.items.length + 1)
            };
        });
    }

    removeItemHandler = (selIndex) => {
        this.setState((prevState) => {
            return {
                items: prevState.items.filter((item, index) => index !== selIndex)
            };
        });
    }

    render () {
        const listItems = this.state.items.map( (item, index) => (
            <CSSTransition key={index} classNames="fade" timeout={300}>
                <li 
                    className="ListItem" 
                    onClick={() => this.removeItemHandler(index)}>
                    {item}
                </li>
            </CSSTransition>
        ) );

        return (
            <div>
                <button className="Button" onClick={this.addItemHandler}>Add Item</button>
                <p>Click Item to Remove.</p>
                <TransitionGroup 
                    component="ul"
                    className="List"
                >
                    {listItems}
                </TransitionGroup>
            </div>
        );
    }
}

export default List;
```

```css
.List {
    list-style: none;
    margin: 0 auto;
    padding: 0;
    width: 280px;
}

.ListItem {
    margin: 0;
    padding: 10px;
    box-sizing: border-box;
    width: 100%;
    border: 1px solid #521751;
    background-color: white;
    text-align: center;
    cursor: pointer;
}

.ListItem:hover,
.ListItem:active {
    background-color: #ccc;
}

.fade-enter {
    opacity: 0;
}

.fade-enter-active {
    opacity: 1;
    transition: opacity 0.3s ease-out;
}

.fade-exit {
    opacity: 1;
}

.fade-exit-active {
    opacity: 0;
    transition: opacity 0.3s ease-out;

```

## 364.

- Alternatives:
  - **React Motion**
  - **React Move**
  - **React router transition** - for animating routing

# 26. Testing  Apps

- **manual testing**
- **automated testing**
  - **unit tests**
    - writing tests for smallest possible units (functions or components)
    - projects typically contain a lot of them
    - the most common / important test
  - **integration tests**
    - test the combination of multiple building blocks working together
    - projects typically contain a couple of integration tests but not as many
  - **end to end tests**
    - testing entire workflows or scenarios
    - reproduce a real human behavior
    - projects typically contain only a few e2e tests

## 384. What to test and how

- Test different building blocks
- Test smallest building blocks that make up your app
- Test success and error cases, also rare (but possible) results

## 385. Technical Setup and Tools

- We need a tool for running a test and asserting results
  - We typically use **jest**
- We need a tool for simulating a react app / components
  - We typically use **React Testing Library**
- Both tools are set up when you work with **CRA**
- best practice is to create files **Component.test.js** within **CRA**
- run tests  by `npm test`

## 387. Writing our first test

- Three **A's**
  - **Arrange** - setup the test data, conditions, and environment
  - **Act** - run logic that should be tested (execute function)
  - **Assert** - check that results match

```jsx
import { render, screen } from '@testing-library/react';
import Greeting from './Greeting';

test('renders Hello World as a text', () => {
  // Arrange
  render(<Greeting />);

  // Act
  // ... nothing

  // Assert
  const helloWorldElement = screen.getByText('Hello World', { exact: false });
  expect(helloWorldElement).toBeInTheDocument();
});
```

## 388. Tests suits vs Tests

- to organize different tests you can organize them into different testing suits

- to pass test into a suit:

  ```jsx
  describe('Greeting component', () => {
    test('renders Hello World as a text', () => {
      // Arrange
      render(<Greeting />);
    
      // Act
      // ... nothing
    
      // Assert
      const helloWorldElement = screen.getByText('Hello World', { exact: false });
      expect(helloWorldElement).toBeInTheDocument();
    });
  })
  ```

## 389. Testing suite with a state

```jsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import Greeting from './Greeting';

describe('Greeting component', () => {
  test('renders Hello World as a text', () => {
    // Arrange
    render(<Greeting />);
  
    // Act
    // ... nothing
  
    // Assert
    const helloWorldElement = screen.getByText('Hello World', { exact: false });
    expect(helloWorldElement).toBeInTheDocument();
  });

  test('renders good to see you if the button was NOT clicked', () => {
    render(<Greeting />);
    const outputElement = screen.getByText('good to see you', { exact: false });
    expect(outputElement).toBeInTheDocument();
  });

  test('renders "Changed!" if the button was clicked', () => {
    // Arrange
    render(<Greeting />);

    // Act
    const buttonElement = screen.getByRole('button');
    userEvent.click(buttonElement);

    // Assert
    const outputElement = screen.getByText('Changed!');
    expect(outputElement).toBeInTheDocument();
  });

  test('does not render "good to see you" if the button was clicked', () => {
      // Arrange
      render(<Greeting />);

      // Act
      const buttonElement = screen.getByRole('button');
      userEvent.click(buttonElement);
  
      // Assert
      const outputElement = screen.queryByText('good to see you', { exact: false });
      expect(outputElement).toBeNull();
  });
})
```

## 390. Testing connected components

- happens automatically

## 391. Testing asynchronous code

```jsx
import { render, screen } from "@testing-library/react";

import Async from "./Async";

describe('Async component', () => {
  test('renders posts if request succeeds', async () => {
    render(<Async />);

    const listItemElements = await screen.findAllByRole('listitem');
    expect(listItemElements).not.toHaveLength(0);
  });
})
```

## 392. Working with mocks

- generally dont want to stress the server

```jsx
import { render, screen } from "@testing-library/react";

import Async from "./Async";

describe('Async component', () => {
  test('renders posts if request succeeds', async () => {
    window.fetch = jest.fn();
    window.fetch.mockResolvedValueOnce({
      json: async () => [{id: 'p1', title: 'First post'}],
    });
    render(<Async />);

    const listItemElements = await screen.findAllByRole('listitem');
    expect(listItemElements).not.toHaveLength(0);
  });
});
```

## 393. Summary and further resources

- **Jest official** docs
- **React testing library** docs
- **react-hooks-testing-library** extension also worth mentioning

# 27. React + TypeScript

- **TS** is a **superset** to **JS** (extends Javascript)
- Most importantly it adds **static typing** to **JS**
  - JavaScript is **dynamically tipped**
- https://www.typescriptlang.org/
- full course potentially by Maxmillian
- to install
  - `npm install typescript`
  - `npx tsc file_name`- runs the compiler
- TS does NOT run in the browser
  - it needs to be compiled to javascript
  - our ts annotations are removed during these compliations, but we are notified here

````ts
// Primitives: number, string, boolean
// More complet types: arrays, objects
// Functions types, parameters

// Primitives
let age: number;
age = 12;

let userName: string;
userName = 'Max';

let isInstructor: boolean;
isInstructor = true;

// More complex types
let hobbies: string[];
hobbies = ['Sports', 'Cooking'];

type Person = {
  name: string,
  age: number;
};

let person: Person;

person = {
  name: 'Max',
  age: 32
};

let peope: Person[]; 

// Type union
let course: string | number = 'React - The Complete Guide';
course = 3;

// Functions & types
function add(a: number, b: number): number {
  return a + b;
}

function print(value: any) {
  console.log(value);
}

// Generics
function insertAtBeginning<T>(array: T[], value: T) {
  const newArray = [value, ...array];
  return newArray;
}

const demoArray = [1, 2, 3];

const updatedArray = insertAtBeginning(demoArray, -1); // [-1, 1, 2, 3]
const stringArray = insertAtBeginning(['a', 'b', 'c'], 'd');
````

## 406. Create react app with typescript

`npx create-react-app my-app --template typescript`

```jsx
import React from "react";

const Todos: React.FC<{items: string[]}> = (props) => {
  return (
    <ul>
      {props.items.map((item) => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
};

export default Todos;
```

