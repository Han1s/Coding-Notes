books recommendation:
- introduction to algorithms
- For programmers who dont know how to dataStructure and would like to do other things well too

## Basics
- Big O complexity
	- if your input grows, how fast does computation or memory grow?
	- the algorithm **O(N)** means it grows linearly
		- e.g. for loop
	- we always drop constats, meaning O(10N) is just O(N)
	- we usually measure the worst case scenario
	- **O(1)** is constat time that is always the same, say lookup in array
	- O(logn)
	- O(N^2) double nested for loops
	- O(N^3) triple nested loops
	- O(n log n) is quicksort (phonenumber book)
	- O(logn) binary search trees
- Array data structure
	-  array is a space in memory

## Search
- Linear search
	-its a very good practice to first visualize the problem, discuss it with boxes and arrows, and then program it.
 - Binary search (if it is ordered)

## Linked Lists
- ordering of operations is very important
- deleting and inserting is **O(1)**
- to get a specific value you have to traverse the list
- foundation concept
```tsx
interface LinkedList<T> {
	get length(): number;
	insertAt(item: T, index: number): void;
	remove(item: T): T | undefined;
	removeAt(index: number): T | undefined;
	append(item: T): void;
	prepend(item: T): void;
	get(index: number): T | undefined;
}
```
### Queue
- fifo structure
- singly linked list

### Stack
- opposite (backwards) of a queue
- you only add or remove from a head

## Arrays
- **Arrays vs list**
	- cannot insert, you can only overwrite
	- O(1) everything
	- size is fixed
	- arrays list operate best when treated like stack.
		- you dont have remove from the front
	- arrays have allocated memory that cannot be expanded, array list (like in javascript) can get expanded. They provide popping and pushing but indexing stays at O(1).
- **RingBuffer**
	- we have index based head and index based tail
	- for example logs

## Recursion
- function that calls itself until it returns a base case