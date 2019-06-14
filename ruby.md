# Ruby

## Introduction

- OOP, server-side scripting (like Python)
- Can be embedded into HTML
- No need for `;`

## Odds and ends

- `#` defines comments
- `BEGIN` **block** defines code to be called before the program is run
- `END` for code to be run at the end of the program
- **Heredoc** is a way to define a multiline string, while maintaining original indentation and formatting
  ```
  print <<EOF
    Multi-line
        string with
    preserved formatting
  EOF
  ```

## Types

- _Numbers_: ints, floats (scientific notation supported)
- **Strings**
  - Within a string, can use `#{}` to sub in the value of any expr
    - If using `#{}` or escaped characters `\`, need to use `" "` instead of `' '`
  - Ruby has **unpack directives** which perform small actions like extractions on strings--google these
- **Ranges**: define an interval of numbers. Can be used as conditionals
  - Inclusive: `(1...5)` includes 5
  - Exclusive: `(1..5)` excludes 5
  
### Arrays and Hashes

- **Arrays**: `arr = ["Fred", 13, 3.14]`
  - Indexed starting at 0. Negative indexes go backwards from the end of the array, e.g. -1 is the last element, -2 the second-last, etc.
  - There are _A BUNCH of array methods!!_
    - Define new array using `[]` or `Array.new`
  - **String arrays**, can initialize using `%w(Fred, Johnson, Holden)` to get `["Fred", "Johnson", "Holden"]`
- **Hashes**: `colors = { "red" => 0xf00, "green" => 0x0f0, "blue" => 0x00f }`
  - Like dictionaries
  - Access keys or values with `.keys` or `.values`


## Operators

- Interestingly, operators are actually method calls. `a+b` is interpreted as `a.+(b)` where `+` is a method of `a` that accepts `b` as its argument
- `**` for exponent
- `+=` and others assignment operators exist
- _Parallel assignment_ (like in Python)
- **Logical operators** can be words (`and`, `or`) or symbols (`&&`, `||`)
- `defined?` operator returns a description string of an expr if it is defined, or `nil` if undefined


## Variable types

- **Local variables**: defined in a method, not available outside that method
  - Start with lowercase
- **Instance variables**: available across methods for any instance/object = NONSTATIC
  - preceded by `@` then var name
- **Class variables**: available across different objects. Belongs to the class = STATIC
  - preceded by `@@` then var name
- **Global variables**: available across classes. Unitialized global variables have the value `nil`
  - preceded by `$`
- **Constants**: supposed to remain constant. Not actually enforced by Ruby lol
  - `UPPERCASE`
- **Pseudo-variables**: special "variables" that behave like constants. Can't assign value to these vars.
  - `self`, `true`, `false`, `nil`, `__FILE__`, `__LINE__`

## Conditionals

- Standard if/else clause
  ```
  if x > 2
    puts "x is greater than 2"
  elsif x < 2
    puts "x is less than 2"
  else
    puts "x is 2"
  end
  ```
- **If modifier** also exists
  ```
  x = 3;
  puts "x=2" if x==2
  ```
- `unless` clause and modifier also exist, works the way you'd think
- `case` clause also exists

## Loops

- `while` has statement and modifier forms
  ```
  while $i < $num do
    puts "Ok"
  end
  ```
- `until` statement and modifier executes code while conditional is false, like `unless` conditional
- `for` is a for each
  ```
  for i in 0..5
    puts "Value of local var is #{i}"
  end
  
  # Equivalent to

  (0..5).each do |i|
    puts "Value of local var is #{i}"
  end
  ```
- `break` terminates loop
- `next` is like `continue`

## Methods

- Start with `def`, end with `end`, parameters within `()`
- If no `return` specified, last statement is the return value
- To **call a method**, just write the method name
  - With parameters, list them after the method name with commas
  ```
  printfive  # printfive is a method that takes no parameters
  add 2, 5   # add is a method that takes two parameters
  ```
- Can also have variable number of parameters

## Blocks

- **Block**: a chunk of code, given a name, enclosed in `{}`
- Invoked from a function with the same name as that of the block using the `yield` keyword
  ```
  def test
    puts "You are in the method"
    yield
    puts "You are again back to the method"
    yield
  end
  test {puts "You are in the block"}
  ```
- Whenever `yield` is called, "You are in the block" prints

## Classes

```
class Bicycle
...
end
```

- **Constructor** is called `initialize` and can take parameters. The `initialize` method will be executed every time the `new` method of the class is called

## Modules

- **Modules**: grouping of methods, classes, and constants under a single name
  - Provide a **namespace** (container for objects), prevent name changes
  - Lets you package functionality into classes
  - Implement mixins (multiple inheritance)
- Use `require` keyword, like Java's IMPORT, to use a module in a program
- Can also embed a module in a class using `include`. Must use `require` first though if the module is defined in a different class.
- **Mixins**: a version of multiple inheritance (a class inheriting features from more than one parent class)
- Dot `.` vs. colon `::` operator: both are used to call methods from another class.
  - No difference when calling class methods
  - `::` can access constants and other namespaced things, `.` can't

## Threading

- A **process** is basically an executing program
- All threads within one process share the same heap memory but contain their own execution stacks = threads can share data but not function calls
- MRI: reference implementation for Ruby prior to 1.9
  - Global Interpreter Lock: prevents multiple Ruby threads from executing at the same time
  - But we can still run certain code while other code is blocked
- Use `Thread.new` with a block to create a new thread
  - Then tell the main thread to wait for the child thread to complete, using `#join`


## Embedded Ruby (ERB) Templating

- Allows you to generate any kind of text from templates (web pages, XML, RSS, etc.)
- Combine plain text with Ruby code for variable substitution and flow control. Copies text portions directly to generated document, and only processes code identified by markers:
  - `<%= ... %>` identifies an **expression**, which will evaluate then be displayed as a string in the template
  - `<%  ... %>` identifies a **scriptlet**, caught and executed, and the final result of the code is injected into the output point of scriptlet. 
    - Used mainly for conditionals or loops
  - 