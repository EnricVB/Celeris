# Celeris Programming Language Specification
## Introduction

Celeris is a general-purpose, IoT oriented, language designed by and for developers. It is inspired in Go and Kotlin, compiling with AOT to offer speed and efficiency.
Its clear syntax and strong Garbage Collector make it ideal for building scalable and portable projects.

## Notation

Celeris uses `Wirth's EBNF`, a metasyntax used by Go and Java:

```
Syntax      = { Production } .
Production  = production_name "=" [ Expression ] "." .
Expression  = Term { "|" Term } .
Term        = Factor { Factor } .
Factor      = production_name | token [ "…" token ] | Group | Option | Repetition .
Group       = "(" Expression ")" .
Option      = "[" Expression "]" .
Repetition  = "{" Expression "}" .
```

- `Syntax`      -> Represents the whole set of grammar rules.
- `Production`  -> Defines a single rule, with a `production_name` and option `Epression`.
- `Expression`  -> Represents alternatives `|` between terms.
- `Term`        -> Sequence of factors that `must` appear in order.
- `Factor`      -> Can be `Production Name`, `Literal/Range of tokens`, `Group`, `Option`, `Repetition`.
- `Group`       -> To treat several elements as one.
- `Option`      -> Which is optional.
- `Repetition`  -> Which can occur zero or more times.

You can understand a `EBNF Notation` system as a `REGEX` system to tokenize the sintaxis.

---

Examples:

**1. Syntax:**

> The whole Syntax, is a group of `Productions`.

```go
var x : Int = 10

func add(a : int, b : int) {
    return a + b
} 
```

**2. Production:**

> This production indicates how to declare variables as (Being `;` optional):

```ebnf
variable_declaration = "var" identifier ":" type "=" expression [";"] .
```

```go
var age : Int = 10
```

**3. Expression**
> Represents alternatives (`|`) between terms, so you can declare a `Production` with different ways to write it.

> This Productions allows to declare a variable with or without the type, in both cases indicating the value.

```ebnf
variable_declaration = 
    "var" identifier ":" type "=" expression [";"] |
    "var" identifier "=" expression [";"] .
```


**4. Term**
> A sequence of factors that must appear in order:

> This Production declares that any float must be a digit, or sequence of digits, with a dot between integer and decimals.
Being { digit } a sequence of 0 or more digits.

```ebnf
float = digit { digit } ["." digit { digit }] .
```

```go
float = 10.0        // Correct
float = .0          // Incorrect
float = 10          // Correct
float = 10.         // Incorrect
```

## Lexical Elements

### Whitespace

Whitespace characters (spaces, tabs, newlines) are used to separate tokens and improve readability. They are generally ignored except when separating tokens.

### Comments

Comments are ignored by the compiler, and serve as program documentation. There are three types of comments:

_1._ Inline comments start with `//` and continue to the end of the line.
_2._ Multi-line comments can comment a block of lines, starting with `/*` and ending with `*/`.
_3._ Documentation comments serve to the compiler in order to give an explanation of what your code does with a formal way. Starts with `/**` and ending with `*/`.

```go
// This is a inline comment

/* This is a
    multi-line comment */

/**
  * This is a documentation comment.
  */
```

### Identifiers

Identifiers are EBNF Productions reserved for variables, classes, interfaces, enums, etc.
This identifier must keep this expression:

```ebnf
identifier      = initial_char { subsequent_char } ;

initial_char    = letter | "_" ;
subsequent_char = letter | digit | "_" | "-" ;

letter          = UnicodeLetter ; (* any Unicode letter, e.g., a–z, á, 中文, кириллица *)
digit           = UnicodeDigit ;  (* any Unicode digit *)
```
```
a
_a
中文
_2025
aNormalVariableName
```

### Keywords

| Conditional Keyword | Explanation |
|---------|-------------|
| `if` | Conditional statement |
| `else` | Alternative conditional branch |
| `else if` | Conditional "else if" branch |
| `switch` | Multi-branch selection |
| `case` | Case in a switch |
| `default` | Specifies default case in switch statements |

| Flow Control Keyword | Explanation |
|---------|-------------|
| `do` | Do-while loop |
| `while` | While loop |
| `for` | For loop |
| `break` | Exit loop or switch |
| `continue` | Skip to next iteration of loop |
| `return` | Return from function |
| `delete` | Manual memory deallocation |
| `new` | Manual memory allocation (object/instance creation) |

| Erorr Handling Keyword | Explanation |
|---------|-------------|
| `try` | Start of exception handling |
| `catch` | Exception handling block |
| `finally` | Block executed after try/catch |
| `throw` | Raise an exception |
| `throws` | Declare exceptions a function can raise |

| Encapsulation Keyword | Explanation |
|---------|-------------|
| `private` | Private access modifier |
| `protected` | Protected access modifier |
| `public` | Public access modifier |
| `internal` | Compilation access modifier, only allows access from the same program |

| Inheritance Keyword | Explanation |
|---------|-------------|
| `enum` | Enumeration type |
| `class` | Class declaration |
| `interface` | Interface declaration |
| `:` or `implements` | Indicates a class implements an interface or class |
| `instanceof` | Checks type of an object |
| `static` | Static member of a file |
| `super` | Access parent class functions or constructor |
| `this` | Reference to the current instance |

| Keyword | Explanation |
|---------|-------------|
| `const` | Constant value declaration |
| `package` | Package declaration |
| `using` | Import or include another package/module |
| `as` | Used to rename an imported class or package for easier reference |
| `true` | Boolean true value |
| `false` | Boolean false value |
| `null` | Null reference |
| `sizeof` | Returns the size in bytes of a data type or variable |
| `var` | Declares a variable with inferred or explicit type |
| `escape` | Storage modifier that instructs the compiler to allocate an object directly in the heap, bypassing escape analysis |

### Operators

| Symbol | Explanation |
|--------|-------------|
| `[ ]` | Array declaration and indexing |
| `{ }` | Delimiters for functions, classes, and code blocks |
| `+` | Addition operator |
| `-` | Subtraction operator |
| `*` | Multiplication operator |
| `/` | Division operator |
| `%` | Modulo operator |
| `=` | Assignment operator |
| `++` | Increment operator |
| `--` | Decrement operator |
| `&&` | Logical AND operator |
| `\|\|` | Logical OR operator |
| `!` | Logical NOT operator |
| `&` | Bitwise AND operator |
| `\|` | Bitwise OR operator |
| `^` | Bitwise XOR operator |
| `~` | Bitwise NOT operator |
| `<<` | Bitwise left shift |
| `>>` | Bitwise right shift |
| `==` | Equality comparison |
| `!=` | Inequality comparison |
| `<` | Less than comparison |
| `>` | Greater than comparison |
| `<=` | Less than or equal comparison |
| `>=` | Greater than or equal comparison |
| `.` | Member access or function call |
| `,` | Separator for arguments or elements |
| `;` | Statement terminator (Optional for inline) |
| `:` | Type annotation or label |
| `()` | Function call or grouping expressions |
| `$variable` | Used for string interpolation within SliceChar literals |

### Literals

Literals are representations of fixed values:

**Intenger Literals**
An Integer Literal is a sequence of digits representing a nubmer without decimals.
You can use `_` for readability for bigger numbers.

```
22      // Valid
2_000   // Valid

_20     // Invalid
20_     // Invalid
2_0     // Invalid
```
**Byte Literals**  
Byte literals represent single byte values, typically in the range `0` to `255`. They can be written in decimal, hexadecimal (`0x`), or binary (`0b`) notation.

```
255         // Decimal byte
0xFF        // Hexadecimal byte
0b11111111  // Binary byte
```

**Long Literals**  
Long literals represent 64-bit integer values. They are suffixed with `L` or `l` to distinguish from regular integers.

```
1234567890123L
0x1FFFFFFFFFFFFFL
```

**Floating Literals**  
Floating literals represent single-precision floating-point numbers. They include a decimal point and may use scientific notation.
It is infered that numbers with less than 8 digits are Float, otherwise it may be a Double.
They can be suffixed with `F` or `f` to distinguish from Double or regular integers.

```
3.14F
0.001F
```

**Double Literals**  
Double literals represent double-precision floating-point numbers.
It is infered that numbers with more than 8 digits are Doubles, otherwise it may be a Float.
They are suffixed with `D` or `d`.

```
3.1415926535D
1.0e-5d
```

**Character Literals**  
Character literals represent single Unicode characters, enclosed in single quotes.

```
'a'
'中'
'\n'   // Newline character
```

**SliceChar Literals**  
SliceChar literals represent sequences of characters (similar to strings), enclosed in double quotes. They support string interpolation using `$variable`.

```
"Hello, World!"
"Value is $x"
```

**Boolean Literals**  
Boolean literals represent truth values: `true` or `false`.

```
true
false
```

**Null Literal**  
The `null` literal represents the absence of a value or reference.

```
null
```

### Nomenclature Standard

**Packages**
Package names must be singular, in lowercase. 
For compound packages, use all lowercase or separate words with an underscore. Prefer non-compound names. 

If the name starts with a digit or illegal character, prefix with an underscore.

```
mathutility
math_utility
_2025exercise
```

**Classes**
Class names start with an uppercase letter, are singular, and should not exceed three words.

```
UserProfile
```

**Functions / Properties / Variables**
They must use camelCase, start with a lowercase letter, and should be descriptive verbs.
Avoid abbreviations unless widely recognized.

```
increaseAge
userAge
age
```

## Variables
A variable is a function scope storage location for holdign a value or pointer into one.
Memory Management explains how variables work, storing a value for primitives or small objects, or a pointer to a memory address for bigger objects.

**Formal EBNF**
```ebnf
variable_declaration_full =
    [ "escape" ] 
    "var" identifier 
    ( ":" variableType "?" | ":" variableType "=" expression | "=" expression )
    [ ";" ] ;
```

**Simplified Notation**
```
[escape] var variable_declaration : <variableType?> = expression [;]
```

- `escape`: keyword for memory scope escape declaration.
- `var`: Keyword for variable declaration.
- `variable_declaration`: Identifier for the variable (must be unique in context).
- `[":" variableType["?"]]`: Data type of the variable (can be infered if initialized). Can be nullable (`?`). Optional if infered.
- `=`: Declares the expression to store
- `expression`: Value expression to store
- `;`: Optional, can help visually to determine the end of a variable. 


## Properties
A property is a class scope variable, can be accessed if you have access to the object instance, and the visibility allows you.

**Formal EBNF**
```ebnf
variable_declaration_full =
    [ "internal" ] 
    [ ( "public" | "private" | "protected" ) ]
    "var" identifier 
    ( ":" variableType "?" | ":" variableType "=" expression | "=" expression )
    [ ";" ] ;
```

**Simplified Notation**
```
[internal] [public | private | protected] [static] var variable_declaration : <variableType?> = expression [;]
```

- `[internal]`: Optional. Limits function access to the same program. You can only use this on properties, not variables. 
- `[visibility]`: Optional. Can be `private`, `protected`, or `public` (defaults to `public`). You can only use this on properties, not variables. 
- `[static]`. Optional. Can be assigned to declare a static property.
- `var`: Keyword for variable declaration.
- `variable_declaration`: Identifier for the variable (must be unique in context).
- `[":" variableType["?"]]`: Data type of the variable (can be infered if initialized). Can be nullable (`?`). Optional if infered.
- `=`: Declares the expression to store
- `expression`: Value expression to store
- `;`: Optional, can help visually to determine the end of a variable. 

## Parameters
A parameter is a variable defined in the signature of a function, method, or constructor, representing an input value that must be provided when calling the function.

**Formal EBNF**
```ebnf
parameter_declaration =
    identifier ( ":" variableType "?" | ":" variableType "=" expression | "=" expression ) [ "=" defaultValue ] ;
```

**Simplified Notation**
```
parameterName : <parameterType?> [= defaultValue]
```

- `parameterName`: Identifier for the parameter (must be unique within the parameter list).
- `parameterType`: Data type of the parameter. Allow nullability.
- `defaultValue`: Optional. If provided, the parameter becomes optional and uses the default value if not specified.

**Examples:**
```go
func add(a : Int, b : Int) {
    return a + b
}

func greet(name : SliceChar = "World") {
    print("Hello, $name")
}
```

Parameters can be passed by value or by reference, depending on the type. The language supports variadic parameters using the `...` syntax:

```ebnf
variadic_parameter = identifier ":" "..." parameterType ;
```

**Example:**
```go
func sum(numbers : ...Int) {
    // numbers is a list of Int
}
```

## Unique Identifier

A unique identifier is a name that must be distinct within its scope. In Celeris, two identifiers cannot share the same name within the same scope (e.g., two variables in a function or two properties in a class). However, identifiers with the same name can exist in different, nested scopes—such as a variable inside a function and a property in the enclosing class. This allows for shadowing, where the innermost declaration takes precedence.

## Constants

A constant is an immutable value defined at compile time, which cannot be changed during program execution.
Constants are always immutable and cannot be reassigned after their initial definition. Attempting to modify a constant will result in a compilation error.

Depending on the scope, it has the same syntaxis as `variable` or `property`, changing the keyword `var` to `const`

**Examples:**
```go
const PI : Double = 3.1415926535D

const maxUsers = 100
```

## Statics
A static is a property or method associated with the class itself, rather than with any instance of the class.
Statics are declared using the `static` keyword, and can be combined with properties to create properties. Static properties and methods are accessed directly via the class name.

Attempting to access a static property or method through an instance will result in a compilation error.

**Examples:**
```go
class MathUtils {
    static const PI : Double = 3.1415926535D
    static var counter : Int = 0

    static func incrementCounter() {
        counter = counter + 1
    }
}
```

Statics can complement properties by providing shared state or behavior that does not depend on individual instances.

## Types

Celeris is a strongly typed language, meaning all variables and properties must have an explicitly defined type at the moment of declaration. If a variable or property is declared without specifying its type, the compiler will throw an exception and prevent the program from compiling.

In addition to strict typing, Celeris enforces rigorous nullability control. This makes it difficult for unpredictable null values to appear in code, as the type system requires explicit declaration if a variable can be null (using the `?` modifier). The compiler thoroughly checks all possible cases of nullability, helping to prevent common errors related to null references.

### Primitive Types

Primitive types are simplest values that Celeris handle. These primitive types include basic data such as numbers, booleans, text, and simple sets.
Because primitives are small and simple to store in memory, they are always allocated on the stack. This reduces overhead and allows for fast access.

Primitives are the simplest data to work with, as they cannot be referenced. When they go out of function scope, these values are immediately discarded.


| Type | Explanation | Size | Range |
|------|-------------|------|-------|
| `Bool` | Boolean type (true/false) | 1 byte | `true` / `false` |
| `Char` | A single character | 1 byte | 0 to 255 |
| `SliceChar` | An array of mutable chars. Length can't change but content is mutable | variable (Default 255 Chars) | Depends on length |
| `Int<T>` | Integer type of a number. You can specify the bytes this Integer will have. By default 32. If an overflow occurs, a compilation error will be thrown. | 4 bytes | -2,147,483,648 to 2,147,483,647 |
| `Byte` | Smallest data type | 1 byte | 0 to 255 |
| `Short` | Small integer | 2 bytes | -32,768 to 32,767 |
| `Long` | Large integer | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `Float` | Single precision floating point | 4 bytes | ±1.18×10⁻³⁸ to ±3.4×10³⁸ |
| `Double` | Double precision floating point | 8 bytes | ±2.22×10⁻³⁰⁸ to ±1.79×10³⁰⁸ |


#### Integer Types
Integer types allow to store any type of number (byte, short, int, long) meanwhile it does not have decimals.

Int value allows to specify the `Bit` quantity of the number, allowing to use `Int<1>` as a Bool, as it allows `0 - 1`.
In case an overflow occurs during compiling time, it will throw a compiling exception.

By default, as other languages, Int without <Specification> uses 32 bits to store data.

On inference, integers just check not to overflow data, in case `100` is stored in `Int<1>`, as it will loose data.
Otherwise, runtime integer operations also check overflow data, as Java.

For data conversion, it is possible to realize an automatic conversion if no overflow occurs. As using a `Int<32>` value as parameter for a `Int<64>` function.
This wouldn't be possible backwards, as it loose data. (Explicit conversion is allowed in this case)

#### Integer Operations

In Celeris, integers support a variety of operations:

**Comparative Operations**  
Used to compare integer values:
- `<`  Less than
- `>`  Greater than
- `<=` Less than or equal to
- `>=` Greater than or equal to

**Equality Operations**  
Used to check if integer values are equal or not:
- `==` Equal to
- `!=` Not equal to

**Quantitative Operations**  
Used for arithmetic calculations:
- `+`  Addition
- `-`  Subtraction
- `*`  Multiplication
- `/`  Division
- `%`  Modulo (remainder)

**Additive Operations**  
Used to increment or decrement integer values:
- `++` Increment by one
- `--` Decrement by one

The placement of the increment/decrement operator affects the result:
- `++var` or `--var`: The value is changed before the expression is evaluated (prefix).
- `var++` or `var--`: The value is changed after the expression is evaluated (postfix).
This distinction is important in inline operations.

**Bitwise Operations**  
Used for manipulating individual bits:
- `<<`  Left shift
- `>>`  Right shift
- `>>>` Unsigned right shift
- `~`   Bitwise NOT
- `&`   Bitwise AND
- `^`   Bitwise XOR
- `|`   Bitwise OR

These operations allow for efficient low-level manipulation of integer data.
#### Floating Types

Floating types in Celeris represent numbers with fractional parts. The two main floating types are:

- `Float`: Single-precision floating-point number (4 bytes).
- `Double`: Double-precision floating-point number (8 bytes).

Floating types can be declared explicitly or inferred by the compiler. Scientific notation is supported, and suffixes (`F`/`f` for Float, `D`/`d` for Double) can be used to specify the type.

**Examples:**
```java
var temperature : Float = 36.6F
var pi : Double = 3.1415926535D
var smallValue = 0.001F
```

#### Floating Operations

Floating-point types support arithmetic, comparison, and assignment operations:

**Arithmetic Operations**
- `+` Addition
- `-` Subtraction
- `*` Multiplication
- `/` Division

**Comparison Operations**
- `<`, `>`, `<=`, `>=` for ordering
- `==`, `!=` for equality

**Assignment**
- `=` for assignment

**Increment/Decrement**
- `++`, `--` (only for simple increments/decrements)

**Examples:**
```go
var a : Float = 1.5F
var b : Float = 2.5F
var sum = a + b      // 4.0F
var isGreater = a > b // false
```

#### Boolean Types

The `Bool` type represents logical values: `true` or `false`. Booleans are used for control flow, logical expressions, and conditions.

**Examples:**
```go
var isActive : Bool = true
var isValid = false
```

#### Boolean Operations

Boolean values support logical and comparison operations:

- `&&` Logical AND
- `||` Logical OR
- `!`  Logical NOT
- `==` Equality
- `!=` Inequality

**Examples:**
```go
var a = true
var b = false
var result = a && b   // false
var negation = !a     // false
```

#### Char Types

The `Char` type represents a single Unicode character. Characters are enclosed in single quotes.

**Examples:**
```go
var letter : Char = 'A'
var symbol = '$'
var newline = '\n'
```

#### Char Operations

Char types support comparison and assignment operations:

- `==`, `!=` for equality/inequality
- `<`, `>`, `<=`, `>=` for ordering (based on Unicode value)
- Assignment (`=`)

**Examples:**
```go
var a : Char = 'a'
var b : Char = 'b'
var isEqual = a == b      // false
var isLess = a < b        // true
```

#### Mixed-Type Operations

When performing operations between different numeric types, Celeris automatically promotes the result to the most precise type. For example, if you add a `Float` and a `Double`, the result will be a `Double`:

```go
var a : Float = 1.5F
var b : Double = 2.5D
var sum = a + b      // sum is Double (4.0D)
```

This ensures that precision is preserved in mixed-type expressions.

### Complex Types
Complex types are composed of one or more primitive types using object-oriented programming (OOP) principles. Due to their increased size and complexity, these types may coexist with primitive data on the stack, but are typically allocated on the heap, where they are managed by the Garbage Collector.

Unlike primitives, complex types are not referenced by value (copy), but by pointers that reference the object in the heap. This approach allows multiple objects to reference the same complex type, enabling updates to be reflected everywhere without costly and risky copying operations.

#### Classes
Classes are complex data that can contain several primitive or complex data within them in the form of properties, in addition to one or more constructors that allow the creation of instances/objects of the class, and functions that allow operations to be performed with data of the class itself and/or external data passed by parameters, which perform operations and may or may not return data.

TODO: Explicar como se gestionan referencias en memoria

0. Visibility
Classes in Celeris have visibility modifiers similar to variables. You can use public, private, or internal.

- Public (default) allows anyone to access the class.
- Private restricts access so that no code outside the class can access it. Useful for classes like Main.
- Internal is different from public and private. It can be combined with other modifiers and limits access at compile time, making it useful for sensitive libraries.

1. Properties
Class properties are similar to variables and provide additional information to a class. These properties can be either primitive types or other classes.
Unlike languages such as Java, getters and setters are not required by default; properties are public by default and can be accessed directly via the instance.

Properties follow strict visibility rules:

- Private: accessible only from within the class.
- Protected: accessible from the class and its subclasses.
- Public: accessible from any scope that has access to the instance.

The `internal` modifier limits access at compile time to the same program, useful for building sensitive libraries.

Properties can also be nullable using `?`:

```c++
var lab : Laboratory?
```

This ensures that any operation on the property must handle the posibility of `null`.

2. Constructors
Constructors are functions responsible for initializing objects and returning an instance. Their syntax is similar to functions but with small differences:

```C++
class User {

    User(name : SliceChar) {

    }
}
```
- The `func` keyword is not used.
- The constructor name matches the class name.
- Parameters can be passed to initialize properties with developer-provided values.

Celeris allows classes without constructors; the compiler will generate a public empty constructor automatically.

Constructors support the same visibility modifiers as properties: `public`, `private`, `protected`, `internal`.
Secondary constructors with different parameters are also allowed.

```c++
class User {
    var name : SliceChar
    var age : Int

    User(name : SliceChar) {
        this.name = name
        this.age = 0
    }

    User(name : SliceChar, age : Int) {
        this.name = name
        this.age = age
    }
}
```

In Celeris, `this`is a keyword that refers to the actual instance of the class, primarly used to:

- Difference between properties and parameters/variables: In this case, the constructor has a `name` parameter, aswell as `name` for the class property. Using `this`, tells compiler you are referencing to insntace's property.

```c++
User(name : SliceChar) {
    this.name = name // Assigns parameter's name value to instance's name property
    name = name      // Reassigns parameter's name value to itself
}
```

3. Functions
Functions provide additional functionality to classes.

Two types of functions exist:
- Static functions: can be called without an instance, as long as the class is public. They cannot access instance-specific properties.
- Instance functions: depend on the object instance and can access instance properties.

4. Inheritance
Celeris supports single class inheritance and interface implementation (multiple allowed).
- Class inheritance: allows access to all properties and functions of the parent class.
- Interface implementation: enforces that the subclass has the same properties and functions as the interface.

```c++
class Animal {
    var age : Int

    Animal() {
        age = 0
    }

    func crawl() {
        print("Rawr")
    }
}

class Pet : Animal {

    Pet() {
        super()
    }

    func growth() {
        age += 1
        crawl()
    }
}
```

- `Pet` inherits `age` from `Animal`, allowing it use `pet.crawl()` and `pet.age` from `Animal`.
- The subclass must call `super()` to initialize the parent before. `super()` must be teh first instruction unless the parent has a default constructor that can be used automatically.


Function `override` occours in the previous example, allowing to change functions from `Animal` inside `Pet` class.
In order to override a function, you need to replicate the same function inside the child's class with same `parameters` and `returns`.
Furthermore, you can use `super` keyword from overrided function to call `parent's function`, executing it whenever you call `super()`, as if you wirte `animal.function()`.

5. Encapsulation
Encapsulation controls the visibility of properties and functions.

- By default, classes, functions, and properties are public; getters and setters are automatically generated.
- For `protected` or `private` members, you may need to create public functions to access values from subclasses or external scopes.

6. Polymorphism
Polymorphism in Celeris allows objects to be treated as instances of their parent class or interface, enabling flexible and reusable code. Through polymorphism, a single function or method can operate on objects of different types, as long as they share a common superclass or interface.

There are two main forms of polymorphism in Celeris:

- **Subtype Polymorphism (Inheritance-based):**
    When a class inherits from a parent class or implements an interface, it can override methods to provide specialized behavior. The overridden method is called based on the actual object's type at runtime, not the reference type.

    **Example:**
    ```go
    class Animal {
         func speak() {
              print("Animal sound")
         }
    }

    class Dog : Animal {
         override func speak() {
              print("Woof")
         }
    }

    func makeSound(animal : Animal) {
         animal.speak()
    }

    var pet : Dog = Dog()
    makeSound(pet) // Output: Woof
    ```

- **Interface Polymorphism:**
    Interfaces define a contract of methods that implementing classes must provide. Functions can accept parameters of the interface type, allowing any implementing class to be used interchangeably.

    **Example:**
    ```go
    interface Drawable {
         func draw()
    }

    class Circle : Drawable {
         override func draw() {
              print("Drawing circle")
         }
    }

    class Square : Drawable {
         override func draw() {
              print("Drawing square")
         }
    }

    func render(shape : Drawable) {
         shape.draw()
    }

    render(Circle()) // Output: Drawing circle
    render(Square()) // Output: Drawing square
    ```

Polymorphism enhances code flexibility, maintainability, and extensibility by allowing new types to be introduced with minimal changes to existing code.

7. **Static Members**

Static members are properties or functions that belong to the class itself, rather than to any instance of the class. They are declared using the `static` keyword and can be accessed directly via the class name. Static members are useful for storing shared data or utility functions that do not depend on instance-specific state.

**Example:**
```go
class Counter {
    static var count : Int = 0

    static func increment() {
        count += 1
    }
}

// Accessing static member
Counter.increment()
print(Counter.count)
```
Static members cannot access instance properties or methods. Attempting to access a static member through an instance will result in a compilation error.

8. **Nested Classes**

Nested classes are classes defined within the scope of another class. They are used to logically group classes that are only used in one place, increasing encapsulation and readability. Nested classes can access the members of their enclosing class, depending on visibility modifiers.

**Example:**
```go
class Outer {
    var outerProperty : Int = 10

    class Inner {
        func show() {
            print("This is a nested class.")
        }
    }
}

// Creating an instance of a nested class
var innerInstance = Outer.Inner()
innerInstance.show()
```
Nested classes are useful for organizing related functionality and limiting the scope of helper classes to their enclosing class.

##### Generics
Generics allow you to define classes, interfaces, and functions that can operate with dynamic data types, such as lists or containers.

```c++
func<T> foo(value : T) {
    // Generic function accepting any type T
}
```

### 1. Optional Type Inference on Call

The type of the generic parameter can be inferred automatically when the argument type is evident:

```c++
foo(5)      // Infers T = Int
foo(5.5)    // Infers T = Float

var user = User("")
foo(user)   // Infers T = User
```

### 2. Monomorphization

Each time a generic is instantiated, the compiler generates a concrete version of the function or class for the specific type.  
This enables strict typing and improves runtime performance, as type checks are resolved at compile time.

### 3. Constraints

You can restrict generics to require inheritance from a specific type using `:`:

```c++
func<T : User> foo(value : T) {
    // T must inherit from User
}
```
###### Generics in Classes

Classes can be generic, allowing them to store or operate on data of any type. Generic classes are declared by specifying type parameters in angle brackets after the class name.

**Example:**
```go
class Box<T> {
    var value : T

    Box(value : T) {
        this.value = value
    }
}

var intBox = Box<Int>(10)
var stringBox = Box<SliceChar>("Hello")
```

###### Generics in Functions

Functions can also be generic, enabling them to accept parameters of any type. The type parameter is declared before the function name.

**Example:**
```go
func<T> identity(x : T) : T {
    return x
}

var a = identity(5)         // a is Int
var b = identity("World")   // b is SliceChar
```

###### Constraints

Constraints restrict generic type parameters to types that inherit from a specific class or implement an interface. Use `:` to specify constraints.

**Example:**
```go
func<T : Comparable> max(a : T, b : T) : T {
    if a > b {
        return a
    }
    return b
}
```

###### Generics in Interfaces

Interfaces can be generic, allowing them to define contracts for multiple types.

**Example:**
```go
interface Repository<T> {
    func add(item : T)
    func get(id : Int) : T
}

class UserRepository : Repository<User> {
    // Implementation for User type
}
```

#### Objects

#### Enumerations

#### Interfaces

## Scope

## Functions

## Statements

### Declaration

### Assignment

### Expression

### Control Flow

### Loop

### Exception

### Return

### Break/Continue

## Collections

## Error Handling

## Debugging / Testing

## OOP Concepts

### Encapsulation

### Abstraction

### Polymorphism

### Inheritance 

## Concurrency / Parallelism

## Type System Extras

### Nullity

### Type Casting

### Type Inference

### Unreachable Code Detection

## Package System / Imports

### Namespaces

## Memory Management

## Compilation Model

## STD Library

## Program Initialization and Execution

## Performance Considerations
