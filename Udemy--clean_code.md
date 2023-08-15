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



## 21. Naming Classes - Theory

- describe the object
  - `User, Product`
- Provide more details without redundancy
  - `Customer, Course`
- Avoid redundant suffixes - `DatabaseManager`



## 22. Naming Classes - Examples

| What Is Stored | Bad Names         | Okay Names       | Good Names            |
| -------------- | ----------------- | ---------------- | --------------------- |
| A User         | UEntity, ObjA     | UserObj, AppUser | User, Admin           |
| A Database     | Data, DataStorage | Db, Data         | Database, SQLDatabase |



## 24. Common Errors & Pitfalls

- Don't include redundant information in names

  - ```jsx
    userWithNameAndAge = User('Max', 31)
    ```

- Avoid Slang, Unclear Abbreviations and Disinformation

- Choose Distinctive Names

- Be consistent with naming

## 26. Challenge problem

```python
# Problem
class Point:
    def __init__(self, coordX, coordY):
        self.coordX = coordX
        self.coordY = coordY


class Rectangle:
    def __init__(self, starting_point, broad, high):
        self.starting_point = starting_point
        self.broad = broad
        self.high = high

    def area(self):
        return self.broad * self.high

    def end_points(self):
        top_right = self.starting_point.coordX + self.broad
        bottom_left = self.starting_point.coordY + self.high
        print('Starting Point (X)): ' + str(self.starting_point.coordX))
        print('Starting Point (Y)): ' + str(self.starting_point.coordY))
        print('End Point X-Axis (Top Right): ' + str(top_right))
        print('End Point Y-Axis (Bottom Left): ' + str(bottom_left))


def build_stuff():
    main_point = Point(50, 100)
    rect = Rectangle(main_point, 90, 10)

    return rect


my_rect = build_stuff()

print(my_rect.area())
my_rect.end_points()

# Solution
class Pointt
	def __init__(self, x, y):
        self.x = x
        self.y = y
        
class Rectangle:
    def __init__(self, origin, width, height):
        self.origin = origin
        self.width = width
        self.height = height
        
    def get_area(self):
        return self.height * self.width
    
    def print_coordinates(self):
        top_right = self.origin.x + self.width
        bottom_left = self.origin.y + self.height
        print('Starting Point (X)): ' + str(self.origin.x))
        print('Starting Point (Y)): ' + str(self.origin.y))
        print('End Point X-Axis (Top Right): ' + str(top_right))
        print('End Point Y-Axis (Bottom Left): ' + str(bottom_left))
        
def build_rectangle():
    rectangle_origin = Point(50, 100)
    return Rectangle(main_point, 90, 10)

rectangle = build_rectangle()

print(rectangle.getArea())
print(rectangle.print_coordinates)
        
```

# II. Code Structure, Comments & Formatting

- comments are (mostly) bad
- Generally avoid them

## 30. Bad comments

- typically you want to avoid them as they convey redundant information
- divider comments are also bad, usually its better to split file into multiple files instead
- commented-out code is also bad practice. Just remove it.

## 31. Good Comments

- legal information
- add explanation that cannot be replaced by proper naming (e.g. regex or something)
- comment that warns you of something
- TODO notes
- Documentation string especially when sharing code

## 32. What is Code Formatting About?

- **vertical formatting**
  - any formatting from the top to the bottom (spacing lines, grouping code, etc)
- **horizontal formatting**
  - everything that happens horizontally (indentation, space between code, line width)
- Formatting is important and greatly improves readability
- Differs between languages
- follow language-specific conventions and guidelines

## 33. Vertical Formatting

- Code should be readable top-bottom without too many jumps
- Consider splitting files with multiple concepts into multiple files
  - as a rule of thumb its good to have only one class per file
- Different concepts should be separated by spacing
- Similar concepts shouldn't be separated by spacing
- Related concepts should be kept close to each other to avoid jumps
- Ordering also matters based on the language you are using



## 35. Horizontal Formatting

- avoid very long unreadable sentences
- break long statements into multiple shorter ones
- use clear but not unreadably long names

## 36. Challenge

```py
# PROBLEM
# (c) Maximilian Schwarzmüller / Academind GmbH

# *********
# Imports
# *********
from os import path, makedirs
from pathlib import Path

# *********
# Main
# *********
# A class which allows us to create DiskStorage instances


class DiskStorage:
    def __init__(self, directory_name):
        self.storage_directory = directory_name

    def get_directory_path(self):
        return Path(self.storage_directory)

    # This must be called before a file is inserted
    def create_directory(self):
        if (not path.exists(self.get_directory_path())):
            makedirs(self.storage_directory)

    # Warning: Directory must exist in advance
    def insert_file(self, file_name, content):
        file = open(self.get_directory_path() / file_name, 'w')
        file.write(content)
        file.close()
        # Todo: Add proper error handling


log_storage = DiskStorage('logs')

log_storage.insert_file('test.txt', 'Test')


# SOLUTION
# (c) Maximilian Schwarzmüller / Academind GmbH
from os import path, makedirs
from pathlib import Path

class DiskStorage:
    def __init__(self, directory_name):
        self.storage_directory = directory_name

    def get_directory_path(self):
        return Path(self.storage_directory)

    def create_directory(self):
        if (not path.exists(self.get_directory_path())):
            makedirs(self.storage_directory)

    # Warning: Directory must exist in advance
    def insert_file(self, file_name, content):
        file_path = self.get_directory_Path() / file_name
        file = open(file_path, 'w')
        file.write(content)
        file.close()
        # TODO: Add proper error handling


log_storage = DiskStorage('logs')

log_storage.create_directory()
log_storage.insert_file('test.txt', 'Test')
```



# III. Functions

## 40. Analyzing Key Function Parts

- calling the function should be readable
  - the number and order of the arguments matter
- working with the function should be easy / readable
  - the length of the function body matters



## 41. Keep the number of Parameters low!

- minimize the number of parameters
  - 0 is ideal
  - 1 is good
  - 2 is acceptable but use with caution
  - 3 tends to be challenging, avoid if possible
  - 3 + Should absolutely be avoided



## 44. Two parameters & when to refactor

- minimize the number of parameters
- understand when number of parameters is readable
- code should minimize the cognitive load
- sometimes rather than a function taking two parameters its better to divide it into two functions
- sometimes its better to replace multiple parameters with one mapping or normal object



## 47. Avoid output parameters

- avoid functions that modify parameters and return them if possible
- its better to use object-oriented approach. E.g. `user.addId()` function call



## 48. Functions should be small and do one thing!

- should be very small
- they should do exactly **one thing**
  - the thing is usually related to the level of abstraction (e.g. validating via low level function and saving via higher level interface)
- you can achieve that by splitting functions into multiple functions



## 49. Why levels of abstraction matter

Functions should do work that's **one level of abstraction below their name**



## 50. When should you split?

- can you extract a code that work on a same functionality from the function?
- can you extract a code that requires more interpretation than the surrounding code? (viz. Level of abstraction)
- for reusability (Dry)



## 54. Don't Overdo It

- Being as granular as possible wont automatically improve readability
- you probably shouldn't split if 
  - you have problem coming up with a name for the extracted function
  - you're just renaming the operation 
  - finding the new function will take longer than reading the extracted code

## 55. Understanding & Avoiding (Unexpected) Side Effects

- try keeping functions **pure**
  - same input generates same output (meaning the same parameter sent there generates the same output)
- What is **side effect**
  - operation which changes the overall system or program state `startSession(...)`
  - they are not bad but unexpected side effects should be avoided (e.g. changing global variable)
  - The name of a function should signal that a side effect occurs
  - if you have a side effect choose a function name that implies it or move it to another function / place

## 56. Side Effects - A Challenge

Problem

```js
function connectDatabase() {
  const didConnect = database.connect();
  if (didConnect) {
    return true;
  } else {
    console.log('Could not connect to database!');
    return false;
  }
}

function determineSupportAgent(ticket) {
  if (ticket.requestType === 'unknown') {
    return findStandardAgent();
  }
  return findAgentByRequestType(ticket.requestType);
}

function isValid(email, password) {
  if (!email.includes('@') || password.length < 7) {
    console.log('Invalid input!');
    return false;
  }
  return true;
}
```



Solution

```js
function initApp() {
	const success = connectDatabase();
    if (!success) {
        console.log('Could not connect to database!');  // could be abstracted as well
    }
    // ...
}

function connectDatabase() {
    const didConnect = database.connect();
    return didConnect();
}

function determineSupportAgent(ticket) {
  if (ticket.requestType === 'unknown') {
    return findStandardAgent();
  }
  return findAgentByRequestType(ticket.requestType);
}

function createUser(email, password) {
    if (!isValid(email, password)) {
        console.log('Could not connect to database!')
    }
    //...
}

function isValid(email, password) {
  if (!email.includes('@') || password.length < 7) {
    return false;
  }
  return true;
}
```



## 57. Unit Testing Helps!

- Can you easily test a function?
  - If yes then its likely a clean code
  - If no consider splitting it
- Small functions are way easier to test than big functions

# V. Control Structures & Errors

- you wanna avoid deeply nested control structures if possible



## 60. Useful Concepts - Overview

- **Avoid Deep Nesting**
- **Using Factory Functions & Polymorphism**
- **Prefer Positive Checks**
- **Utilize Errors**
