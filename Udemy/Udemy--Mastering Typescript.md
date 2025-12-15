- to compile a file to a js you can write `tsc [filename].ts`

## 3. Annotation Basics
- use inference by default
- its good to define the type if you use delayed initialization, otherwise the default type is `any`

```ts
let movieTitle: string = 'Amadeus';
```

## 4. Functions
- its usually better practice to explicitly state the return type for better readability

### Never
- represents a value that never occur. Function that always throws an exception or never finishes executing. Function does not finish executing.


## 5. Objects
```ts
function printName(person: {first: string;, last: string}): void {
	console.log(`${person.first} ${person.last}`);
}

printName({first: "Mick", last: "Jagger", age: 47}) // throws an ERROR as inline
const singer = {first: "Mick", last: "Jagger", age; 47, isAlive: true};
print(singer) // VALID as it it stored in a variable
```

### type aliases

```ts
type Point = {
	x: number
	y: number
}
```

### readonly keyword
```ts
type User = {
	readonly id: number
	username: string
}

const user: User = {
	id: 12837,
	username: "catgirl"
}

user.id = 2353  // ERROR
```

### Intersection
```ts
type Circle = {
	radius: number;
}

type Colorful = {
	color: string
}

type ColorfulCircle = Circle & Colorful;  // combination of both
```


## 6. Union Types
```ts
const age: number | string = 4;
```

### union types and arrays
```ts
const stuff: (number | string)[] = [1, '1'];
```

### literal types
```ts
const zero: 0 = 0;

let mood: 'Happy' | 'Sad' = 'Happy';
```

## 8. Tuples
- array with a fixed length and fixed order of types
- only exist in typescript
- tuple does not complain if you push something after its creation, thats a limitation of a tuple
- you rarely use them cause objects kind of do the same thing
```ts
const sfuff: string[] = []  // normal array;

const color: [number, number, number] = [255, 0, 255] // tuple
```

### enums
- allow us to define a set of named constants
- they add code to the compiled javascript
- its not that different from objects except autocomplete
```ts
enum OrderStatus {
	PENDING,  // 0
	SHIPPED,  // 1
	DELIVERED,  // 2
	RETURNED. // 3
}

const myStatus = OrderStatus.DELIVERED;
```

```ts
enum OrderStatus {
	UP = 'up'
	DOWN = 'down',
	LEFT = 'left',
	right = 'right'
}

const myStatus = OrderStatus.DELIVERED;
```

to workaround adding code to existing javascript: 

```ts
// the const keyword actually replaces the new code with a number and no new object is added
const enum OrderStatus {
	PENDING,
	SHIPPED,
	DELIVERED,
	RETURNED
}

const myStatus = OrderStatus.DELIVERED;
```

## 9. Interaces
- similar to type interfaces
- describe shape of objects (only objects)
- can also use `optional` and `readonly` properties
```ts
interface Point {
	readonly id: number;
	x: number;
	y: number;
	nickname?: string;
	sayHi: () => string;
	//sayHi(): string is the same as line above
}
```
- you can expand interfaces to add properties to them
```ts
interface Dog { 
	name: string;
	age: number
}

interface Dog {
	breed: string;
	bark: () => string;
}

// this extends the Dog to have all 4 properties
```
- you can also extend interfaces
```ts
interface ServiceDog extends Dog {
	job: "drug sniffer" | "bomb" | "guide dog"
}
```
- you can also extend multiple interfaces
```ts
interface Person { 
	name: string
}

interface Employee {
	readonly id: number,
	email: string
}

interface Engineer extends Person, Employee {
	level: string,
	languages: string[]
}
```

### interface vs type
- interface can be reopened, types cannot
- interfaces have to be objects, type can be anything
- with types you cannot use `extend` keyword, you have to use `&`
- its better to gravitate to interfaces


## 10. Compiling typescript
- bunch of options
- managed via **tsconfig.json** file
- `tsc [filename].ts` converts the file to javascript
	- or use playground online
- `tsc --watch` for hot update
- `tsc` in a specific folder converts all typescript files
	- this also includes the nested files as the default include is `**`
- bunch of config you can use, like subfiles you want to compile etc.
- **outDir** specifies the output directory
- **target** specifies the ES version


## 11. DOM mini project
- **type assertions**
```ts
const mysterty: unknown = "Hello World";
const numChars = (mystery as string).length;
```

## 14. Generics
- allow us to define reusable functions and classes that work with multiple types.
- these types have relationship between input and output

```ts
function identity<T>(item: T): T {
	return item;
}

// to call
identity<numver>(7);
```

```ts
function getRandomElement<T>(list: T[]): T {
	const randIdx = Math.floor(Math.random() * list.length);
	return list[randIdx];
}

getRandomElement<string>(['a', 'b', 'c', 'd']);
```
- in many cases TS can infer the type from the function call, but not in every case
```ts
getRandomElement(['a', 'b', 'c', 'd']) // works as well

const btn = document.querySelector<HTMLButtonElement>('.btn'); // cannot infer
```
- in arrow functions you have to add trailing coma when working in **jsx** files due to recognition of html elements
```ts
const getRandomElement = <T,>(element: T): T =>  {...}
```
- when working with multiple types:
```ts
function merge<T, U>(object1: T, object2: U) {
	return {
	...object1,
	...object2
	}
}
```
- adding **type constraints**:
```ts
function merge<T extends object, U extends object>(object1: T, object2: U) {
	return {
	...object1,
	...object2
	}
}
```
- **default type parameters**
```ts
function makeEmptyArray<T = number>(): T[] {
	return [];
}

const bools = makeEmptyArray<boolean>();
```
- you can also write **generic classes**
```ts
interface Song {
	title: string
	artist: string
}

interface Video {
	title: string;
	creator: string;
	resolution: string
}

class Playlist<T> {
	public queue: T[] = [];
	add(el: T) {
		this.queue.push(el);
	}
}

const songs = new Playlist<Song>();
const videos = new Playlist<Video>();
videos.add(...)
```


## 15. Type narrowing
- works great when working with primitive types
```ts
typeof 'abc' // 'string'
typeof 12345 // number
typeof ['1'] // object
```
- trythy guard
```ts
const el = document.getElementById('idk');
if (el) {
	el.something // ts knows it is not null;
}
```
- **equalitty narrowing**
```ts
function someDemo(x: string | number, y: string | boolean) {
	if (x === y) {
		// x and y must both be string according to ts
		// if I used == it could be a string / number
	}
}
```
- **narrowing with the in operator**
```ts
interface Movie { 
	title: string,
	duration: number
}

interface TVShow {
	title: string,
	numEpisodes: number,
	episodeDuration: number
}

function getRuntime(media: Movie | TVSHow) {
	if ('numEpisodes')  in media) {
		... // ts knows it is TVShow
	}
}
```
- **instance of** tells us whether it is instance of a class
```ts
function printFullDate(date: string | Date) {
	if (date instanceof Date) {
		console.log(date.toUTCString());
	} else {
		console.log(new Date(date).toUTCString());
	}
}
```
- **exhaustive checking**
```ts
function getFarmAnimalSound(animal: Pig | Rooster | Cow | Sheep) {
	switch (animal.kind) {
		case "pig":
			return "Oink!";
		case "cow":
			return "Moooo!":;
		case "rooster";
			return "Cockadoodledoo!";
		default:
			// gets triggered cause sheep is not caught
			const _exhaustiveCheck: never = animal;
			return _exhaustiveCheck;
	}
}
```


### Type predicates
- allows us to write custom functions to narrow the type of a value
- these functions have **predicate** return type
```ts
function isCat(animal: Cat | Dog): animal is Cat {
	return (animal as Cat).numLives !== undefined;
}
```

### Discriminated unions
- a property based on which we can discriminate the type
- sort of like a **__typename** in GQL


## 16. Type Declarations
- **.d.ts** files
	- these are files that contain type declarations
- if a library does not have a type declaration
	- you can usually just install it from **@types/....** package **DefinitelyTyped**
	- `npm install --save-dev @types/[packageName]`
	- the list available at https://www.typescriptlang.org/dt/search