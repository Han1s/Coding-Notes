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



## 2. Code Structure, Comments & Formatting

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

