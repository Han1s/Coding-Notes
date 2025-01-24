https://react.dev/learn


# Describing the UI

- [x] your first component
- [x] importing and exporting components
- [x] Writing Markup with JSX
- [x] JavaScript in JSX with Curly Braces
- [x] Passing Props to a component
- [x] Conditional Rendering
- [x] Rendering lists
- [x] Keeping Components Pure
- [x] Understanding your UI as a Tree

## Your first component

- **component** is a **JavaScript** function that you can sprinkle with markup
- names must start with capital letter or they won't work
- **Never define a component inside of another component!** It is slow and causes bugs
- do not add layout styling to the abstracted components

### Keeping Components Pure

- pure means **same input same output**
- react component has to always return the same JSX given the same inputs


# Adding Interactivity

- [x] Responding to events
- [x] State: A component's memory
- [x] Render and Commit
- [x] State as a Snapshot
- [x] Queueing a Series of State Updates
- [x] Updating objects in State
- [x] Updating Arrays in State


## Responding to events
- by convention the handler functions should start with **handle** word followed by the event name
- **stopPropagation** prevents the behavior from the handlers up the tree
- **preventDefault** prevents the default behavior of the browser

## Render and Commit
- Any screen update in React app happens in three steps
	- **Trigger**
	- **Render**
	- **Commit**
- React does not touch the DOM if the rendering result is the same as last time

## State as a Snapshot
- **a state variable's value never changes within a render**, even if its event handler's code is asynchronous

## Queueing a Series of State Updates
- UI only updates after all the code in the event handler completes
- if you use an updater function (provided by setState) it is treated as **added to a queue** of updates
- if you do not use an updater, any setState is treatead as **replace**
- you can use **immer** to update nested objects
- it is common practice to name updater values with initials:
```jsx
setLastName(ln => ln.reverse());
```
or more verbose example:
```jsx
setEnabled(enabled => !enabled)`, or to use a prefix like `setEnabled(prevEnabled => !prevEnabled)
```


## Updating Objects in State
- spread operator only copies objects one level deep

## Updating Arrays in State
- another kind of object
- you should also create a copy when changing array state
- use **.slice** not **.splice** (slice copies an array or a part of it while splice mutates)
- easiest way to remove from array is **.filter** method
- copying arrays is only one level deep, you need to copy individual objects to modify nested arrays
- you can use **immer** to update nested objects


## How to use Immer
```jsx
import React, { useCallback, useState } from "react";
import {produce} from "immer";

const TodoList = () => {
  const [todos, setTodos] = useState([
    {
      id: "React",
      title: "Learn React",
      done: true
    },
    {
      id: "Immer",
      title: "Try Immer",
      done: false
    }
  ]);

  const handleToggle = useCallback((id) => {
    setTodos(
      produce((draft) => {
        const todo = draft.find((todo) => todo.id === id);
        todo.done = !todo.done;
      })
    );
  }, []);

  const handleAdd = useCallback(() => {
    setTodos(
      produce((draft) => {
        draft.push({
          id: "todo_" + Math.random(),
          title: "A new todo",
          done: false
        });
      })
    );
  }, []);

  return (<div>{*/ See CodeSandbox */}</div>)
}
```

OR

```jsx
import React, { useCallback } from "react";
import { useImmer } from "use-immer";

const TodoList = () => {
  const [todos, setTodos] = useImmer([
    {
      id: "React",
      title: "Learn React",
      done: true
    },
    {
      id: "Immer",
      title: "Try Immer",
      done: false
    }
  ]);

  const handleToggle = useCallback((id) => {
    setTodos((draft) => {
      const todo = draft.find((todo) => todo.id === id);
      todo.done = !todo.done;
    });
  }, []);

  const handleAdd = useCallback(() => {
    setTodos((draft) => {
      draft.push({
        id: "todo_" + Math.random(),
        title: "A new todo",
        done: false
      });
    });
  }, []);
```

# Managing State

- [x] Reacting to Input with state
- [x] Choosing the State structure
- [x] Sharing state between components
- [ ] Preserving and Resetting State


## Reacting to input with state
- React is **declarative** compared to **imperative** approaches
	- imperative - you need to command the interaction
	- declarative - you describe different states and react handles the rest


## Choosing the State Structure
1. **Group related state.** If you always update two or more state variables at the same time, consider merging them into a single state variable.
2. **Avoid contradictions in state.** When the state is structured in a way that several pieces of state may contradict and “disagree” with each other, you leave room for mistakes. Try to avoid this.
3. **Avoid redundant state.** If you can calculate some information from the component’s props or its existing state variables during rendering, you should not put that information into that component’s state.
4. **Avoid duplication in state.** When the same data is duplicated between multiple state variables, or within nested objects, it is difficult to keep them in sync. Reduce duplication when you can.
5. **Avoid deeply nested state.** Deeply hierarchical state is not very convenient to update. When possible, prefer to structure state in a flat way.

## Sharing State Between Components
- lifting state up means moving state to the closest common parent

## Preserving and Resetting State (video candidate)
- State is tied to a position in the render tree
- when react removes a component, it destroy its state
- same component at the same position preserves state
- its the position in the UI tree, not in the JSX markup, that matters to react
- different components at the same position reset state
- if you want to preserve state between re-renders, the structure of the tree needs to **match up** from one render to another
- you can also use **keys** - they are not just for lists
- don't nest component definitions, or you'll reset state by accident

## Extracting State Logic into a Reducer
- reducer can help out cut down on the code if many event handlers modify state in a similar way
- useful for more complex state updates
- it's easier to debug than `useState` 
- it's easier to test as it does not depend on the component state so it can be tested in isolation
- reducers must be pure and update objects and arrays without mutations
- you can use `useImmerReducer` for easier syntax

## Passing Data Deeply With Context
- To pass context:
	1. Create and export it with `export const MyContext = createContext(defaultValue)`.
	2. Pass it to the `useContext(MyContext)` Hook to read it in any child component, no matter how deep.
	3. Wrap children into `<MyContext.Provider value={...}>` to provide it from a parent.
- Context lets you write components that “adapt to their surroundings” and display themselves differently depending on where (or, in other words, in which context) they are being rendered.
- Before you use context, try passing props or passing JSX as `children`.
- use cases for context
	- Theming: If your app lets the user change its appearance (e.g. dark mode), you can put a context provider at the top of your app, and use that context in components that need to adjust their visual look.
	- Current account: Many components might need to know the currently logged in user. Putting it in context makes it convenient to read it anywhere in the tree. Some apps also let you operate multiple accounts at the same time (e.g. to leave a comment as a different user). In those cases, it can be convenient to wrap a part of the UI into a nested provider with a different current account value.
	- Routing: Most routing solutions use context internally to hold the current route. This is how every link “knows” whether it’s active or not. If you build your own router, you might want to do it too.
	- Managing state: As your app grows, you might end up with a lot of state closer to the top of your app. Many distant components below may want to change it. It is common to use a reducer together with context to manage complex state and pass it down to distant components without too much hassle.

- using context instead of prop drilling in combination with state:
```jsx
// Context.js
import { createContext } from 'react';

export const ImageSizeContext = createContext(100);

// App.js
import { useState, useContext } from 'react';
import { places } from './data.js';
import { getImageUrl } from './utils.js';
import { ImageSizeContext } from './Context.js';

export default function App() {
  const [isLarge, setIsLarge] = useState(false);  // use state
  const imageSize = isLarge ? 150 : 100; 
  return (
    <>
      <label>
        <input
          type="checkbox"
          checked={isLarge}
          onChange={e => {
            setIsLarge(e.target.checked);
          }}
        />
        Use large images
      </label>
      <hr />
      <ImageSizeContext.Provider value={imageSize}>  // provide context
        <List imageSize={imageSize} />
      </ImageSizeContext.Provider>
    </>
  )
}

function List({ imageSize }) {
  const listItems = places.map(place =>
    <li key={place.id}>
      <Place
        place={place}
      />
    </li>
  );
  return <ul>{listItems}</ul>;
}

function Place({ place, imageSize }) {
  return (
    <>
      <PlaceImage
        place={place}
      />
      <p>
        <b>{place.name}</b>
        {': ' + place.description}
      </p>
    </>
  );
}

function PlaceImage({ place }) {
  const imageSize = useContext(ImageSizeContext)  // consume context
  
  return (
    <img
      src={getImageUrl(place)}
      alt={place.name}
      width={imageSize}
      height={imageSize}
    />
  );
}
```


## Scaling app with reducer and Context

TODO:

# Escape Hatches

## Referencing values with refs

- when you want a component to "remember" some information but you don't want that information to trigger new renders, you can use a **ref**
- typical use cases:
	- storing **timeout ID**
	- storing and manipulating **DOM elements**
	- storing other objects that are not necessary to calculate the JSX

## Manipulating the DOM with Refs
- if you want to scroll somewhere after the state is changed use `flushSync`
```jsx
          flushSync(() => {
            if (index < catList.length - 1) {
              setIndex(index + 1);
            } else {
              setIndex(0);
            }
          });
          imgRef.current.scrollIntoView({
            behavior: 'smooth',
            block: 'nearest',
            inline: 'center'
          });
```

## Synchronizing with Effects
- effects are typically used to 'step out' of your React code and synchronize with some external systems such as APIs, widgets, network, etc.
- effects run as a result of rendering AFTER the render
- if initial `useEffect` subscribes to something, the cleanup function should unsubscribe
- if effect fetches something, the cleanup should **abort** the fetch or ignore its result;
```jsx
useEffect(() => {
  let ignore = false;

  async function startFetching() {
    const json = await fetchTodos(userId);
    if (!ignore) {
      setTodos(json);
    }
  }

  startFetching();

  return () => {
    ignore = true;
  };
}, [userId]);
```
- you cant ignore a request that already happened. But the cleanup function should ensure that the fetch that's not relevant anymore does not keep affecting the application

Effects
- Unlike events, effects are caused by rendering itself rather than a particular interaction
- effects let you synchronize a component with some external system
- in strict mode developement, react mounts components twice to stress-test effects
	- if your effect breaks because of remounting, you need to implement a cleanup function

TODO: exercises