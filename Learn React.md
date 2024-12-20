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