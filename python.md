# Python

## Basics - new

- Interpreted language, i.e. doesn't need to be compiled before it's run
- Dynamically typed: type checking at runtime (vs. compile-time)
- Functions are first-class objects
- In OOP, no `public` or `private` modifiers

### Comments, syntax - new

- Single line comments with `#`
- Wrap multiline comments with `'''` or `"""`
- _No semicolons in Python!!_
- `print()` to print

## Variables

### Types - new

- Numbers: int, float, complex
- Booleans: `True`, `False`
- Sequences: str, bytes/byte arrays, list, tuple
- Collections: set, dictionary

### Syntax - new

- _No need to declare **variable types**_
  ```
  x = 1          # int
  isCool = True  # bool
  name = 'John'  # str
  x = 'Great'    # re-assigned to str
  ```
- **Multiple assignment** works for vars: `x, isCool, name = (1, True, 'John')`
- `type(myVar)` returns the type of myVar
- _Cast_ variables using `str(myVar)`, `int(myVar)`, etc.

### Numbers

- Three types: int, float, complex
  - Complex numbers use `j` for the imaginary part

### Strings

- To concatenate different types to strings, need to cast them to string
- **String formatting** exists

  - Percent strings, like in C:
    ```
    print("Hello %s. You are %s." % (name, age))
    ```
  - Arguments by position:
    ```
    name = 'Joe'
    age = 66
    print('My name is {name} and I am {age}'.format(name=name, age=age))
    ```
  - **F-Strings** (3.6+), kind of like in JavaScript:
    ```
    print(f'My name is {name} and I am {age}')
    ```
    - Within the `{}` you can have literally Python expression, since f-strings are evaluated at runtime

| String methods of interest |                                              |
| -------------------------- | -------------------------------------------- |
| `str[i]`                   | charAt(i)                                    |
| `str[i:j]`                 | substring i (inclusive) to j (not inclusive) |
| `len(str)`                 | length; works for most data types            |
| `replace(str1, str2)`      | replace str1 with str2                       |
| `str.count(t)`             | counts the number of occurrences of t in str |
| `str.split()`              | turns str into a list                        |

## Array-like objects

- **List**: ordered, changeable, allow duplicates.
  - `myList = ['bob', 'joe', 'james']`
- **Tuple**: ordered, *un*changeable, allow duplicates
  - `myTuple = ('bob', 'joe', 'james')`
- **Set**: unordered, unindexed, no duplicates
  - `mySet = {'bob', 'joe', 'james'}`
- **Dictionary**: unordered, changeable, indexed, no duplicates
  - `myDict = { 'name': 'bob', 'age': 56 }`

### Lists

- Syntax: `myList = ['bob', 'joe', 'james']`
- Loop thru using for (for each) loop
- List methods of interest: `append(item)`, `remove(item)`, `pop(index)` (without index, removes the last item), `insert(index, item)`, `reverse()`, `del list[i]`, and `sort()` (also `sort(reverse=True)`)

#### List comprehension

- Create list from other iterable(s)
- Example:
  ```
  numbers = [1, 2, 3, 4]
  squares = [n**2 for n in numbers]
  ```
- More complicated example:
  ```
  lista = [1, 2, 3, 4]
  listb = [2, 3, 4, 5]
  common_num = [a for a in lista for b in listb if a == b]
  ```

### Tuples

- Syntax: `myTuple = ('bob', 'joe', 'james')`
- Loop thru using for (for each) loop
- `del myTuple` deletes it
- Tuple methods of interest: `count(item)` (counts number of times item appears in tuple), `index(item)` (returns index of item)

### Sets

- Syntax: `mySet = {'bob', 'joe', 'james'}`
- Since sets are unordered, items have a random order
- Cannot change items, but can still use `add(item)` or `remove(item)` (or `discard(item)`, which doesn't throw an error if that doesn't exist), and `clear()` (distinct from deleting)

### Dictionaries

- Syntax:
  ```
  myDict = {
    'name': 'bob',
    'age': 56
  }
  ```
- Terminology: _items_ are "tuples" that have _keys_ and _values_
- Access values (and change them) using `myDict[key]` or `myDict.get(key)`
- `keys()` to get all keys, `items()` to get all items, `copy()` to copy the dict to a new var

## Iterators

- _Iterable_: object containing a countable number of values, which can be iterated upon
  - Strings; lists, tuples, sets, dicts are all iterable containers from which you can obtain an **iterator**
  ```
  myTuple = ('bob', 'joe')
  myIter = iter(myTuple)
  print(next(myIter))   # bob
  print(next(myIter))   # joe
  ```
- Can also iterate using a `for` loop
- Can use `StopIteration` exception in `__next__()` for a condition that terminates iteration
- Iterators use **lazy evaluation**: values are computed only when asked for
  - Saves memory--good for very large lists
- _Can be iterated over only once_

### Creating a custom iterator class

- Need to implement the methods `__iter__()` (must return `self`) and `__next__()` (must return next object in sequence) in the object

### Generators and `yield`

- Allow us to create iterators in a simpler way
- `yield` is like "return", but it saves the _state_ of the function.
  - The next time the function is called, execution continues _from where it left off_, with the same variable values it had before yielding
- **Generator expression**: like list comprehensions, but use `()` instead of `[]`
  ```
  squares = (n**2 for n in range(2, 1000000))
  ```

## If statements

```
 if x > y:
    print('Greater')
 elif x == y:
    print('Equals')
 else
    print('Less')
```

## Operators

- _Logical_ operators are written, i.e. `and`, `or`, `not`
- _Identity_: `x is y` returns true if x and y are the same object
- _Membership_: `x in y` returns true if x is present in the object y
- No `++` in Python, use `x += 1`

## Loops

### Standard

- `while` loops are pretty standard; again, no parentheses
- `break` and `continue` are standard

### New things

- `for` loops must iterate over a _sequence_ (list,
  tuple, dict, set, or string [loop thru chars in a
  string])
  - Think of these as _iterators_, or **for each** loops
- `else` keyword after a loop is like a "finally" block

#### `range()` function

- Starts from 0 by default and ends at the specified number
  ```
  for x in range(6):
    print(x)
  ```
- Prints numbers 0, 1, 2, 3, 4, 5 (new line for each)
  - `range(2, 6)` prints 2, 3, 4, 5
  - `range(2, 6, 2)` prints 2, 4

##### `xrange()` function

- Deprecated in Python 3, as `range()` behaves like this by default
- `xrange()` returns an `xrange` object, which creates a **lazy list**
  - So, better for gigantic ranges as `xrange` will generate numbers on demand
- But if you want to iterate over a list multiple times, use `range()` instead

## Functions

- Syntax uses `def` keyword, `:`, then indentation
  ```
  def getSum(num1=1, num2=1):   # default values, will be used if called as getSum()
     return num1 + num2
  ```

### Lambda functions

- Syntax uses `lambda` keyword

  ```
  addTwoNums = lambda x, y : x + y    # : is like => in JS
  print(addTwoNums(5, 6))   # prints 11
  ```

- Powerful when used as anonymous functions inside another function
  - e.g. having an addNum(x) function that has a lambda expression, then passing in 5 to make an addFive function

## Classes and objects

- `class` keyword creates a class; once again, use `:` instead of { }
- `self` is like Java's 'this', referring to the current instance of the class.
  - _But, you need to pass in `self` as the first parameter to **any** object method, including the constructor!!_
  - You don't actually have to pass in self when you call, Python does it for you
- The **constructor** is called `__init__()` in Python
- Any object method needs `self` passed in as the first parameter--but doesn't have to be named `self`, can be named anything
- Delete object properties, or objects themselves, using `del` (just like in JavaScript)

  ```
  class Employee:
    empCount = 0    # static variable

    def __init__(self, name, salary):
      self.name = name;
      self.salary = salary
      Employee.empCount += 1

    def displayEmployee(self):
      print "Name : ", self.name,  ", Salary: ", self.salary
  ```

  | Class methods of interest |                                                                     |
  | ------------------------- | ------------------------------------------------------------------- |
  | `getattr(objName, attr)`  | equivalent to `objName.attr`                                        |
  | `hasattr(objName, attr)`  | checks if it has that attribute or not                              |
  | `__str__(self)`           | toString()                                                          |
  | `__repr__(self)`          | like toString, but mainly for debugging. Point is to be unambiguous |


### Inheritance

- When defining a child class, pass in the parent class:
  ```
  class Stegosaur(Dinosaur):
    ...
  ```
- Can use the `pass` keyword when you don't want to add any additional properties or methods to the class
  - This is a null operation that is used when a statement is syntactically required, but you don't want any command/code to execute
- Can override methods

## Modules

- **Module**: like a code library, a file containing a set of functions you want to include in an app
- Use `import myModule`, then use `myModule.myFunc()`
  - `import myModule as mm`
  - `from myModule import myFunc`

### JSON Module

- `json.loads(someJSON)` to convert JSON => Python dictionary
- `json.dumps(obj)` to convert Python objects => JSON
  - works with dict, list, tuple, str, int, float, True, False, None

## RegEx

- import the `re` module to search with **regular expressions**
- `search()` function searches the string for a match, then returns a Match object if there is one
- Regular expressions: https://www.w3schools.com/python/python_regex.asp#matchobject

## Try-except

- `try` = try, `except` = catch, `finally` = finally
- `else` block runs if no errors are raised
- `finally` block executes regardless of if try block raises an error or not

# Advanced Concepts

## Decorators

- Functions return a value based on given args
- Functions are **first-class objects** in Python, i.e. they can be passed around or used as args (remember _higher-order functions_???)
- **Decorators** are defined with `@`
