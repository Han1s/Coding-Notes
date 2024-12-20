# Elementary

- Define a variable in JS (or other language) and assign it a value
- how would you access last element in an array
## Primary (project)

- Show any of the projects you worked at and walk us through.
	- What did you enjoy / not enjoy?
	- What was difficult for you?
	- What could be improved / added / optimized in the future?


# Advanced (applicant knows front end)

## Basic (JavaScript, html, CSS)

- What is a **CSS class**?
	- A:  an attribute used to define a group of HTML elements in order to apply unique styling and formatting to those elements with CSS
- Explain REST + CRUD
- difference between **let** and **const**  in JS?
	- **let** allows the variable to be reassigned multiple times, while **const** creates a variable that cannot be reassigned after it has been assigned a value.
- How to handle **exceptions** in JS?
	- A: **try / catch / finally**
- What is a **media query** and how do you use it?
	- Media queries is a feature of CSS 3 allowing content rendering to adapt to different conditions such as screen resolution.
- (Open) How to make a **website faster**? (can be within context of react)
	- A:
		- Run profiling tools and tackle the biggest problem first
		- bundling / minification / tree-shaking
		- async loading
		- small / no libraries
		- lazy loading
		- image placeholders
		- CDN's
		- image sizing
		- cache
		- less js, more css
		- etc...

## React (from the least difficult, applicant knows react)

- Q: How can you share a single state between multiple components?
	- A: Move the state up the component tree into a common parent
- Q: How do you render a list of elements in react?
	- A: **map()** function
- Q: What are some of the differences between **state** and **props**?

|                        **Props**                        |                                      **State**                                      |
| :-----------------------------------------------------: | :---------------------------------------------------------------------------------: |
|    The Data is passed from one component to another.    |                    The Data is passed within the component only.                    |
|          It is Immutable (cannot be modified).          |                          It is Mutable ( can be modified).                          |
| Props can be used with state and functional components. | The state can be used only with the state components/class component (Before 16.0). |
|                  Props are read-only.                   |                        The state is both read and write.<br>                        |
|                                                         |                                                                                     |

- Q: What does **useEffect** hook do? When is it generally used? **What are some of the pitfalls**?
	- usually for synchronization with external systems
	- it does trigger additional rerender if you change state inside
- Q: What happens if we use useEffect with empty dependency array?
	- it triggers the effect only on component mount
- Q: What is react fragment? When is it generally used?
	- when you need a react component to return more than one element and not clutter the html with additional divs
- Q: what is the difference between **controlled** and **uncontrolled** input?
	- A: controlled input takes state as a value and is controlled by this state, uncontrolled input is not managed by a state. An advantage of uncontrolled input is that it does not trigger re-render as it does not trigger state change, the disadvantage is that you cannot control the value with a state change.
- Q: What is **key** property for and when would you use it?
- Q: what is the difference between **ref** and **state**
	- A: change in the ref does not trigger re-render, you can also use **ref** to reference parts of the UI to access it later (input to gather value from, element to focus/scroll to, etc.)
- Q: When do you use **useMemo** hook?
	- to memoize components or functions and define when should those components rerender / functions redefine. Will no longer be necessary after react 19

##### Exercise

```jsx

// TODO: Fix the code
function Form() {  
	const [firstName, setFirstName] = useState('Taylor');  
	const [lastName, setLastName] = useState('Swift');  
	
	const [fullName, setFullName] = useState('');  
	
	useEffect(() => {  
		setFullName(firstName + ' ' + lastName);  
	}, [firstName, lastName]);  
	// ... 
	return <p>My name is {fullName};
}
```

- solution:
```jsx
function Form() {  
	const [firstName, setFirstName] = useState('Taylor');  
	const [lastName, setLastName] = useState('Swift');  

	// SOLUTION 1 - reduces the amount of rerenders by one as it removes the unnecessary useState call
	const fullName = firstName + ' ' + lastName;
	// ... 
	return <p>My name is {fullName}</p>;

	// --- OR ---
	return <p>My name is {firstname + ' ' + lastName};
}