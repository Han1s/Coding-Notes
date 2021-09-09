Notes for work:

- debouncing into return
- refactor using context

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
  
First way:
  
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



  
