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