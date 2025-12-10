## You are a Junior Dev if You Don’t Know These 18 TypeScript Utility Types

```tsx
type User = {
	id: string
	name: string
	age: number
	address?: {
		street: string
		city: string
	}
}

function createUserWithAddress(user: User) {}

// Omit: Pass User object except the id property
function createUser(user: Omit<User, "id">) {}

// Partial: make basically all properties optional
function createUserWithAddress(user: Partial<User>) {}

// Pick: pass only name and age properties of the user object
function createUserWithAddress(user: Pick<User, "name" | "age">) {}

// Record says that every instance of that object has to have a key of a type PropertyKey and value of a { test: string }
type T = Record<PropertyKey, { test: string }>
const a: T = {
	admin: {
		test: "sdf"
	}
}

// EXTRACT
type Role = 'admin' | 'user' | 'security'
type OtherRole = 'testing' | 'admin' | 'user' | 'security'

type T = Extract<Role, OtherRole>  // T is 'admin' | 'user'
type T = Exclude<Role, OtherRole>  // T is 'security'


// ReturnType
function getUser(id: string) {
	return { name: 'John', id, age: 30}
}
type T = ReturnType<typeof getUser>  // T is the object from the function

// Parameters: array of function parameters
function getUser(id:string, other: boolean) {...}ß
type P = Parameters<typeof getUser>  // P is [string, boolean]


// NonNullable
type A = string | null | undefined
type T = NonNullable<A>  // string


// Awaited - gives you what promise returns
async function getUser(id: string) {
	return Promise.resolve({name: 'john'})
}
type T = Awaited<ReturnType<typeof getUser>> // {name: 'john'}


// String manipulation types
type S = 'Hello World'
type T = Lowercase<s>
Type T2 = Uppercase<S>
Type T3 = Capitalize<S>

```