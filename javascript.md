# JavaScript

## Language basics

### Typing

- Java, C, OCaml are **statically typed**: the type of a variable is known at compile time. In Java, C, etc. variable types are _explicitly specified_ while in OCaml the types are _inferred_
  - Examples: C, C++, Java, Rust, Go, Scala, OCaml, Kotlin
- JavaScript is **dynamically typed**: types are associated with runtime values, not named variables/fields

### Scope

- Variables declared globally (outside any function) have **global scope**
- Variables declared in a function have scope inside that function (**local/function scope**)
  - `var` and `let`
  - Variables declared with `var` inside `{ }` can be accessed from outside the block
- `let` vars inside `{ }` _cannot_ be accessed from outside the block: they have **block scope**
- `const` defines a constant _reference to a value_
  - We cannot change constant primitive values, but we can change/add properties of constant objects
  - Semantically, tells you that this variable won't change values
- <ins>ES6: should only be using `let` and `const`</ins>

### Syntactic sugar

- **Template literals** are strings allowing embedded expressions, between backticks. Placeholders are indicated by `${expr}`
  - `'x+y makes' + x + y + 'in total'` becomes `x+y makes ${x+y} in total` between backticks

## Basic concepts

- Types:
  - boolean + number or number + number -> addition (false = 0, true = 1)
  - All others are concatenation
- Equality: `=` is assignment, `==` is equality (comparison), `===` checks for equality of data type as well
  - **Associativity**: assignment operator is right to left

### Variables

- Defined with `let` or `const` no matter the type (incl. arrays)
- A variable that is called but never defined is `not defined`, but its _type_ is `undefined`

##### Hoisting

- Using a var/function before it's declared, in the code
- Vars declared with `let` and `const` are not hoisted
- Only _declarations_ are hoisted, NOT _initializations_!
- Only functions, and not function expressions are hoisted
- These examples give different results:
  ```
  // Example 1
  var x = 5;
  var y = 7;
  console.log(x+y);

  // Example 2
  var x = 5;
  console.log(x+y);
  var y = 7;

  // Equivalent to example 2:
  var x = 5;
  var y;
  console.log(x+y);
  y = 7;
  ```

### Arrays

- Add obj to an array using `arr.push(obj)`
- Reverse an array using `arr.reverse()`
- Empty an array by setting `arr.length = 0`
- Check to see if it's an array using `Array.isArray(obj)`
- Higher order iterator functions: `myArr.map(myFunc)`, `.filter()`, `.reduce()` (fold left), `.reduceRight()` (fold right), `.every()` (for all), `.some()` (exists)

### Maps

- **Maps** hold key-value pairs, like dicts in Python
- Keys must be unique, but you can overwrite an existing key's value
- `keys()` and `values()` return Iterator objects
- `set('id', 10)` to set map pairs
  ```
  let myMap = new Map();
  ```

### Sets

- **Sets** hold _unique_ values of any type
- Adding duplicate values (with `add('a')`) doesn't throw an error, just doesn't add them

### Spread attributes

- Spread operator: `...`
- _"Spread"_ the given function; expands an array to a list of elements (e.g. as arguments for function calls), or a list of elements to an array
  ```
  let nums = [1, 2, 3];             // Array
  myFunc(...nums);                  // legal assuming a normal function call is myFunc(1,2,3), i.e. myFunc(nums) is illegal
  let nums2 = [...nums, 4, 5, 6];   // [1,2,3,4,5,6]
  ```

### Loops

- `for` and `while` loops are pretty standard
- **`forEach`** loops: available only in Arrays, Maps, Sets. Takes a callback function and invokes it once for each array element. Callback can access index and value of array elements
  ```
  var numbers = [1, 2, 3, 4, 5];
  numbers.forEach((number) => {
      ...
  })
  ```
- **`for of`**: new in ES6; for iterating collections, like Arrays, Maps, etc.
  ```
  for (let var of iterableObj)
  ```
- **`for in`**: loop thru _**enumerable properties** of an object_. Can access keys of object, but not values. Works for arrays and even strings
  ```
  for (let prop in obj)
  ```

### Conditionals

- `if` statements are the same as in Java
- **`switch`** statements:
  ```
  var name = 'Jeremy';
  switch(name) {
      case "David":
          alert("Hello David!");
          break;
      case "Jeremy":
          alert("Hello Jeremy!);  // This will be called
          break;
      default:
          alert("Hello there!");
  }
  ```
- **Ternary operator** `condition ? exprT : exprF`: if condition is true, return exprT, if false, return exprF

### Functions

- *Functions return `undefined` unless specified otherwise*
- Can have _default values_, e.g. `function name(param1 = 56, param2) { ... }`
- Function **declaration**:
  - Defined at parse time
  - Is **hoisted**--you can call the function before it's actually defined in the code
  ```
  function name(params) {
      ...
  }
  ```
- Function **expression**:
  - Defined at runtime--can only be called after its definition
  - Not hoisted
  ```
  let name = function(params) {
      ...
  }
  ```

#### Arrow function expressions

- Shorter syntax for function expressions
  - Can't use `this`; they use the `this` of the scope in which the object enclosing them is defined
    - Don't use arrow functions as object methods
  - Not hoisted
  ```
  let name = (params) => {
    ...
  }
  ```

## Concepts

### Object-oriented programming

#### Objects

- **Objects** comprise everything that's not a primitive: `undefined`, `null`, `boolean`, `number` (incl. int and float), `string`
- **Object literal**:
  ```
  var person = {
      firstName: 'Jeremy',
      lastName: 'Hansen',
      age: 44
  }
  ```
  - Delete properties from an object using `delete prop1`
    - Doesn't work for prototype properties

### Prototype-based inheritance

- _Doesn't have a class implementation like Java or C++_
  - `class` keyword in ES6 is syntactical sugar
- Inheritance has only one construct, **objects**. Think of an object as a bag of properties
  - Each object has a **prototype**, a private property that holds a link to another object. 
  - Goes on etc. until an object is reached with `null` as its prototype
  - `null` has no prototype and is the final link in the **prototype chain**
  ```
  function boogie(){}
  boogie.prototype.foo = "bar";
  const myBoogie = new boogie();
  myBoogie.prop = "some value";
  console.log(myBoogie);
  
  // returns the following:

  prop: "some value"
  <prototype>: {…}
    constructor: function boogie()
    foo: "bar"
  ```

- No "methods", rather can add functions to an object in the form of a property

#### "Classes"

- Class declarations are not hoisted
- Constructor made with `constructor()`
- `static` methods exist
 
### Event loop

- **Event loop**: JS is single-threaded, but it can "fake" concurrency
- How `setTimeout(*callback*, *ms*)` really works:

  - Run the following steps in parallel:
    1. Wait _ms_ milliseconds (side thread)
    2. Queue a task to run the following steps (side thread)
       a. Invoke _callback_ (main thread)

- **Task queues**:

### Asynchronous programming

- **Asynchronous execution** means there is no **blocking**, i.e. code doesn't necessarily have to execute in the order it's written

  ```
  // Example 1 - Synchronous (blocks)
  var result = database.query("SELECT * FROM hugetable");
  console.log("Query finished");
  console.log("Next line");

  // Example 2 - Asynchronous (doesn't block)
  database.query("SELECT * FROM hugetable", function(result) {
      console.log("Query finished");
  });
  console.log("Next line");
  ```

  - Here, example 1 would print `Query finished` before `Next line`, while example 2 would print `Next line` first
    - The callback is executed after the query finishes, but the console log doesn't have to wait for the query to finish

#### Promises

- **Callback function**: a function that is to be executed after another function has finished executing
  - Callbacks are passed as args in other functions (_higher-order functions_)
  - Used to make sure certain code doesn't execute until other code has already finished execution, i.e. an "I'm done!" notice
- **Promise**: check for a certain condition. If true, expected result returned by calling `resolve()`, then execute the "callback" function. If false, send a rejection message by using `reject()`.

  ```
  function kevin() {
      return new Promise((resolve, reject) => {
          var keepsHisWord = true;
          if (keepsHisWord) {
              resolve('Kevin keeps his word');
          } else {
              reject('Kevin's a POS');
          }
      });
  }

  kevin()
  .then(quasiCallback())
  .catch(err => console.log(err));

  ```

  - A value called `PromiseStatus` updates according to what's happening; a promise can be `pending`, `resolved`, or `rejected`
  - quasiCallback is called if myFunc passes the condition

##### Promise object

- _All methods return a Promise object_
- Has three _prototype_ (non-static) methods. One or more of these will run when a Promise is settled, depending on `PromiseStatus`
  - `Promise.then(onFulfilled, onRejected)`: use for **resolving** promises. Can be chained
  - `Promise.catch(onRejected)`: Use for **rejecting** promises. Can be chained
  - `Promise.finally(onFinally)`: executed whenever a promise is settled regardless of status

![](https://cdn-images-1.medium.com/max/1000/1*0mBlni5vsYZE2wFzfVv8EA.png)

- Has four _static_ methods:

  - `Promise.reject()` and `Promise.resolve()` quickly create promises
  - `Promise.all(iterable)` returns one Promise that resolves when

    1. The Promises in the argument have resolved, or
    2. When the argument has no Promises

    - Rejects with the reason of the first Promise it rejects
    - Parallel execution

  - `Promise.race(iterable)` returns a Promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects, with the value or reason from that Promise

#### Async await

- **`async` functions** operate asynchronously in the **event loop**, using an implicit Promise to return its result. _But they are written syntactically like synchronous functions._
  - Can contain an **`await`** expression that pauses the execution of the async function until the Promise is resolved, then resumes the async function's execution and returns the resolved value
  - Uses general `try` `catch` for error handling (instead of the `.catch`)
  -
