# I. Getting Started

## 2. What is Clean Code

- Clean Code
  - should be readable and meaningful
  - should reduce cognitive load
  - should be concise and to the point
  - should avoid unintuitive names, complex nesting and big code blocks
  - should follow best practices and patterns
  - should be fun to write and maintain
- Dirty Code
  - hard to understand

## 3. Key Pain Points

- Names
  - variables
  - functions
  - classes
- Structure and Comments
  - code formatting
  - good & bad comments
- Functions
  - length
  - parameters
- Conditionals & Error handling
  - Deep nesting
  - missing error handling
- Classes & Data Structures
  - missing distinction
  - bloated classes

## 8. Learning Community

https://academind.com/community/

## 10. Clean Code, Principles & Patterns & Clean Architecture

- Clean Code
  - Code that is readable and easy to understand
  - Focuses on single problems / files
- Patterns & Principles
  - write code which is maintainable and extensible
- Clean Code vs Clean Architecture
  - Clean Code is about writing a code
  - How you structure the project, separate entities and store data
  - **Where** you write your code

## 11. Clean Code vs Quick Code

- Always refactor
- Always improve the code
- Always review and improve
- Its iterative process
- Embrace refactoring
- Codebase can only stay alive if you continuously refactor and improve it
- Clean Code should be priority in any project you start

# II. Naming - Variables, Functions, Classes and more

## 14. Why good names matter

- names should be meaningful
- well named things allow readers to understand the code without going through it in detail

## 15. Choosing Good Names

- **Variables & Constants**
  - data containers
  - usually use **nouns** or short phrases with **adjectives**
- **Functions / Methods**
  - Commands or calculated values
  - typically **verbs** or short phrases with **adjectives**
- **Classes**
  - to create things / objects
  - typically **nouns** or short phrases with **nouns**

## 16. Casing conventions & Programming Languages

- **snake_case**
  - Python
- **camelCase**
  - Java, JavaScript
- **PascalCase**
  - Python, Java, Javascript for class names
- **kebab-case**
  - Ruby, html

## 17. Naming Variables & Properties - Theory

- Value is an object
  - describe the value 
    - `user, database`
  - you can provide more details without introducing redundancy
    - `authenticatedUser, sqlDatabase`

- Value is Number or String
  - describe the value
    - `name, age`
  - you can provide more details without introducing redundancy
    - `firstName, age`
- Value is Boolean
  - answer a true / false question
    - `isActive, loggedIn`
  - you can provide more details without introducing redundancy
    - `isActiveUser`

## 17. Naming Variables & Properties - Examples

| What Is Stored                              | Bad Names | Okay Names              | Good Names         |
| ------------------------------------------- | --------- | ----------------------- | ------------------ |
| user object (name, email, age)              | u, data   | userData, person        | user, customer     |
| user input validation result (true / false) | v, val    | correct, validatedInput | isValid, isCorrect |



## 19. Naming Functions & Methods - Theory

- functions performs an operation
  - describe that operation
    - `getUser(), response.send()`
  - provide more details without redundancy
    - `getUserByEmail()`
- function computes a Boolean
  - answer true or false question
    - `isValid, purchase.isPaid()`
  - provide more details without redundancy
    - `emailIsValid, purchase.isPaid()`

# 20. Naming Functions & Methods - Examples

| What Is Stored                              | Bad Names           | Okay Names              | Good Names            |
| ------------------------------------------- | ------------------- | ----------------------- | --------------------- |
| Save user data to a database                | process(), handle() | save, storeData         | saveUser, user.store  |
| user input validation result (true / false) | process(), save()   | validateSave(), check() | validate(), isValid() |