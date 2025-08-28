# Celeris Compiler Specification

## 1. Overview

Language for Celeris designed to be read by **CSAOT**.

---

## 2. Lexical Structure

### 2.1 Whitespace

Whitespace characters (spaces, tabs, newlines) are used to separate tokens and improve readability. They are generally ignored except when separating tokens.

### 2.2 Comments

Comments are ignored by the compiler and can be single-line or multi-line.

#### 2.2.1 Single-line Comments
Start with `//` and continue to the end of the line.

```go
// This is a single-line comment
```

#### 2.2.2 Multi-line Comments
Enclosed between `/*` and `*/`.

```go
/* This is a
     multi-line comment */
```

```go
/*
 * This is a
 * multi-line comment
 */
```

#### 2.2.3 Documentation Comments

```go
/**
 * This is a documentation comment.
 */
```

### 2.3 Identifiers

Identifiers are names for variables, functions, classes, etc. They must start with a letter (A-Z, a-z) or underscore (`_`), followed by letters, digits (0-9), or underscores.

### 2.4 Nomenclature Standards

#### 2.4.1 Packages
Package names must be singular, in lowercase. In case for composed packages, you can both keep it all in lowercase, or use an underscore. Anyway, it is recommended to use non composed names for packages. If the package name begins with a digit or any other illegal character, the suggested convention is to add an underscore aswell.

**Example:** `mathutility` or `math_utility`
**Underscore Example:** `_2025exercise`

#### 2.4.2 Classes
Class names must start with an uppercase letter, be singular, and not exceed three words.

**Example:** `UserProfile`

#### 2.4.3 Functions
Function names must be in camelCase, start with a lowercase letter, and use descriptive verbs.

**Example:** `calculateTriangleArea`

#### 2.4.4 Variables
Variable names must be in camelCase, start with a lowercase letter, and be descriptive. Avoid abbreviations unless widely recognized.

**Examples:** `userAge`, `totalAmount`

### 2.5 Literals

Literals represent fixed values in the source code:

- **Integer literals:** `42`, `-7`
- **Byte literals:** `0xFF`, `255`, `b'Z'`
- **Long literals:** `1234567890123L`, `-9876543210L`
- **Floating-point literals:** `3.14`, `-0.001`, `4F`
- **Double literals:** `3.14159D`, `-2.71828D`
- **Character literals:** `'A'`, `'9'`
- **SliceChar literals:** `"Hello, World!"`
- **Boolean literals:** `true`, `false`
- **Null literal:** `null`

#### 2.5.1 Integer Literals

An Integer can be written as `10`, `0`, `-1`, being interpreted by default a `Int<32>`.

```go
var a = 10          // By default: Int<32>
var b : Int<8> = 5  // 5 Integer of 8 bits
var c : Int<64> = 5 // 5 Integer of 64 bits
```

### 2.6 Operators, Symbols and Delimiters

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

### 2.7 Keywords

#### 2.7.1 Conditional Words

| Keyword | Explanation |
|---------|-------------|
| `IF` | Conditional statement |
| `ELSE` | Alternative conditional branch |
| `ELSE IF` | Conditional "else if" branch |
| `SWITCH` | Multi-branch selection |
| `CASE` | Case in a switch |
| `DEFAULT` | Specifies default case in switch statements |

#### 2.7.2 Flow Control Words

| Keyword | Explanation |
|---------|-------------|
| `DO` | Do-while loop |
| `WHILE` | While loop |
| `FOR` | For loop |
| `BREAK` | Exit loop or switch |
| `CONTINUE` | Skip to next iteration of loop |
| `RETURN` | Return from function |
| `DELETE` | Manual memory deallocation |
| `NEW` | Manual memory allocation (object/instance creation) |

#### 2.7.3 Error Handling Words

| Keyword | Explanation |
|---------|-------------|
| `TRY` | Start of exception handling |
| `CATCH` | Exception handling block |
| `FINALLY` | Block executed after try/catch |
| `THROW` | Raise an exception |
| `THROWS` | Declare exceptions a function can raise |

#### 2.7.4 Encapsulation Words

| Keyword | Explanation |
|---------|-------------|
| `PRIVATE` | Private access modifier |
| `PROTECTED` | Protected access modifier |
| `PUBLIC` | Public access modifier |
| `INTERNAL` | Compilation access modifier, only allows access from the same program |

#### 2.7.5 Inheritance Words

| Keyword | Explanation |
|---------|-------------|
| `ENUM` | Enumeration type |
| `CLASS` | Class declaration |
| `INTERFACE` | Interface declaration |
| `:` or `IMPLEMENTS` | Indicates a class implements an interface or class |
| `INSTANCEOF` | Checks type of an object |
| `STATIC` | Static member of a file |
| `SUPER` | Access parent class functions or constructor |
| `THIS` | Reference to the current instance |

#### 2.7.6 Miscellaneous Keywords

| Keyword | Explanation |
|---------|-------------|
| `CONST` | Constant value declaration |
| `PACKAGE` | Package declaration |
| `USING` | Import or include another package/module |
| `AS` | Used to rename an imported class or package for easier reference |
| `TRUE` | Boolean true value |
| `FALSE` | Boolean false value |
| `NULL` | Null reference |
| `SIZEOF` | Returns the size in bytes of a data type or variable |
| `VAR` | Declares a variable with inferred or explicit type |
| Data Types | Any data type is a keyword |

### 2.8 Escape Sequences

String and character literals support escape sequences such as `\n` (newline), `\t` (tab), `\\` (backslash), `\'` (single quote), and `\"` (double quote).

---

## 3. Type System

Celeris supports a variety of built-in types and allows for user-defined types.

### 3.1 Primitive Types

| Type | Explanation | Size | Range |
|------|-------------|------|-------|
| `Bool` | Boolean type (true/false) | 1 byte | `true` / `false` |
| `Char` | A single character | 1 byte | 0 to 255 |
| `SliceChar` | An array of mutable chars. Length can't change but content is mutable | variable (Default 255 Chars) | Depends on length |
| `Int<T>` | Integer type of a number. You can specify the bytes this Integer will have. By default 32. If an overflow or underflow occurs, a compilation error will be thrown. | 4 bytes | -2,147,483,648 to 2,147,483,647 |
| `Byte` | Smallest data type | 1 byte | 0 to 255 |
| `Short` | Small integer | 2 bytes | -32,768 to 32,767 |
| `Long` | Large integer | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `Float` | Single precision floating point | 4 bytes | ±1.18×10⁻³⁸ to ±3.4×10³⁸ |
| `Double` | Double precision floating point | 8 bytes | ±2.22×10⁻³⁰⁸ to ±1.79×10³⁰⁸ |

### 3.2 Composite Types

#### 3.2.1 Arrays
Arrays are fixed-size and mutable, non-ordered collections of elements of the same type.

```go
var numbers : Int[5] = [1, 2, 3, 4, 5]
```

#### 3.2.2 Slices
Slices are fixed-sized and mutable sequences of elements. `SliceChar` is a built-in slice type for characters.

```go
var message : SliceChar = "Hello, World!"
```

### 3.3 Default Values

When a variable is declared but not explicitly initialized, it is assigned a default value based on its type:

| Type | Default Value |
|------|---------------|
| `Bool` | `false` |
| `Char` | `''` |
| `SliceChar` | `""` (empty string) |
| `Int` | `0` |
| `Byte` | `0` |
| `Short` | `0` |
| `Long` | `0L` |
| `Float` | `0.0F` |
| `Double` | `0.0D` |
| Object/Class | `null` |
| Array | `null` |

#### Example

```go
var flag : Bool         // flag is false
var count : Int         // count is 0
var name : SliceChar    // name is ""
var user : UserProfile  // user is null
```

### 3.4 Generics and Type Parameters

Generics are commonly used with collections, custom data structures, and utility functions. For example, `List<T>` can store elements of any type, and functions can accept or return generic types.

Generic type parameters are resolved at compile time, ensuring type correctness and performance. You can also use type constraints to require that a type parameter implements an interface or inherits from a base class.

Generics support multiple type parameters, allowing complex relationships between types. This feature is essential for building flexible APIs and reusable components.

#### 3.4.1 Generic Type Declaration

You must declare generic on the class or function declaration. Unless you do it, you won't be able to use generic on your class.

```go
class Container<T> {        // This is valid
    public var value : T 

    Container(initialValue : T) {
        this.value = initialValue
    }
}

class Container {           // This is invalid
    var value : T

    Container(initialValue : T) {
        this.value = initialValue
    }
}

class Utility {
    public static func findMax<T : Number> (a : T, b : T) (T) { // This is valid
        return a > b ? a : b
    }
}

class MathUtility<T : Number> {
    public static func findMax(a : T, b : T) (T) {              // This is valid
        return a > b ? a : b
    }
}
```

#### 3.4.2 Generic Functions

You can use Generics inside functions, as parameter or return value.

```go
class MathUtility<T : Number> {

    public static func findMax(a : T, b : T) (T) {
        return a > b ? a : b
    }
}
```

#### 3.4.3 Type Constraints

You can specify generic type constraints to restrict the types that can be used as type parameters. By default, `<T>` allows any type, but you can use syntax like `<T : Animal>` to indicate that `T` must be `Animal` or inherit from `Animal`. This enables compile-time filtering and ensures type safety for generic classes and functions.

**Example:**

```go
class PetShelter<T : Animal> {
    var animals : List<T>
}
```

#### 3.4.4 Multiple Type Parameters

You can declare multiple generic type parameters by separating them with commas in angle brackets. This allows classes and functions to work with several types simultaneously.

```go
class Pair<K, V> {
    var key : K
    var value : V

    Pair(key : K, value : V) {
        this.key = key
        this.value = value
    }
}

class Repository<T : Entity, ID : Identifier> {
    func findById(id : ID) : (T) {
        // Implementation
    }
}

func swap<A, B>(a : A, b : B) : (B, A) {
    return b, a
}
```

### 3.5 Nullably Types

Nullable types allow a variable to hold either a value of the specified type or `null`.

#### 3.5.1 Nullable Type Declaration

They are declared by adding a question mark `?` to the type:

```go
var varName : <Type>? = null
```

`varName` can be of type `<Type>` or `null`. If the `?` is not included, the variable can never be `null` and the compiler will emit an error if you try to assign `null`.

#### 3.5.2 Null Checking

To check if a value is null, use the `null` keyword in a conditional expression:

```go
func processUser(user : User?) {
    if (user != null) {
        print("Processing user: $user.name")
    } else {
        print("No user to process")
    }
}
```

This pattern ensures safe access to properties or methods only when the variable is not null.

#### 3.5.3 Safe Navigation Operator

The safe navigation operator `?.` allows you to access properties or methods of an object only if it is not `null`. If the object is `null`, the entire expression evaluates to `null` without throwing an error.

**Syntax:**

```go
var result = user?.name
```

This is equivalent to:

```go
if (user == null) {
    return null
} else {
    return user.name
}
```

You can chain safe navigation operators for nested objects:

```go
var name = entity?.data?.name
```

This returns `null` if any part of the chain (`entity`, `data`, or `name`) is `null`.

> **Note:** The safe navigation operator improves code readability and reduces the need for explicit null checks.

#### 3.5.4 Null Coalescing Operator

The null coalescing operator `??` allows you to provide a default value when an expression evaluates to `null`. It is commonly used with nullable types and safe navigation.

**Syntax:**

```go
var displayName = user?.name ?? "Unknown"
```

This is equivalent to:

```go
var name = user == null ? null : user.name
displayName = name == null ? "Unknown" : name
```

The operator checks if the left-hand side is `null`; if so, it returns the right-hand side value. Otherwise, it returns the left-hand side value.

> **Note:** The null coalescing operator simplifies code by reducing explicit null checks and providing fallback values in a single expression.

---

## 4. Language Usage

### 4.1 Variables

Variables in Celeris are declared using the `var` keyword, followed by the variable name and an optional type annotation.

#### 4.1.1 Syntax

```go
[internal] [visibility] var <variableName> : <Type?>
```

- `[internal]`: Optional. Limits function access to the same program. You can only use this on class-scope variables, not method-scope. 
- `[visibility]`: Optional. Can be `private`, `protected`, or `public` (defaults to `private`). You can only use this on class-scope variables, not method-scope. 
- `var` is the keyword for variable declaration
- `variableName` is the identifier for the variable (must be unique in context)
- `Type` is the data type of the variable (can be infered if initialized)

##### Examples

```go
var age : Int
var name : SliceChar
var isActive : Bool
```

#### 4.1.2 Scope

The scope of variables in Celeris is always local to the block in which they are declared. If a variable is defined inside a function, it is only accessible within that function. Class member variables have class-level scope, meaning they can be accessed from anywhere you have a reference to the class instance.

Static variables have global scope within the program, provided their visibility allows access. Static members can be accessed without creating an instance of the class, and their lifetime is tied to the program execution.

The `internal` modifier restricts scope to within the same compilation program. Members marked as `internal` are only accessible from code that is part of the same compiled program, and not from external libraries or modules.

#### 4.1.3 Initialization

Initialize a variable at declaration using the assignment operator `=`:

```go
var age : Int = 25
var name : SliceChar = "Alice"
var isActive : Bool = true
```

You can also declare and initialize arrays and objects:

```go
var numbers : Int[] = [1, 2, 3]
var user : UserProfile = UserProfile()
```

#### 4.1.4 Multiple Assignment

Celeris supports multiple assignment, allowing you to assign values to several variables simultaneously:

```go
var a, b, c = 1, 2, 3
// a = 1, b = 2, c = 3
```

This feature is useful when unpacking values from functions that return multiple results:

```go
func getUserInfo() : (SliceChar, Int, Bool) {
    return "Bob", 30, true
}

var name, age, isActive = getUserInfo()
// name = "Bob", age = 30, isActive = true
```

#### 4.1.5 Type Inference

Celeris supports type inference, allowing the compiler to automatically deduce the type of a variable from its initializer:

```go
var inferred = 42        // Type inferred as Int
var message = "Hello"    // Type inferred as SliceChar
var flag = true          // Type inferred as Bool
```

> **Note:** If a variable is declared without an initializer, type inference cannot be applied. In such cases, an explicit type annotation is required.

```go
var value           // Invalid: type cannot be inferred
var value : Int     // Valid: explicit type annotation
```

### 4.2 Constants and Static

#### 4.2.1 Constants

Constants are declared using the `const` keyword. A constant is read-only and its value cannot be changed after initialization.

```go
const PI : Double = 3.14159D
const greeting : SliceChar = "Hello"
```

#### 4.2.2 Static Variables and Functions

The `static` keyword is used to declare variables or functions that belong to the class itself rather than to any instance. Static members can be accessed without creating an instance of the class.

```go
class MathUtils {
    static var counter : Int = 0

    static func increment() {
        counter = counter + 1
    }
}
```

#### 4.2.3 Combining `const` and `static`

You can use both `const` and `static` together to declare class-level constants:

```go
class Config {
    static const MAX_USERS : Int = 100
}
```

### 4.3 Functions

Functions are declared using the `func` keyword:

#### 4.3.1 Syntax

```go
[internal] [visibility] [abstract] [static] func functionName(param1 : Type1, param2 : Type2, ...) : (ReturnType) {
    // function body
}
```

```go
// Public static function with parameters and return value
public static func sum(a : Int, b : Int) : (Int) {
    return a + b
}

// Internal public function with parameters, no return value
internal public func execute(task : Task) {
    print("Executing task: $task.name")
}

// Private function with no parameters or return value
func initialize() {
    // Perform initialization logic here
}

// Abstract function in a class or interface (no body)
abstract func calculateArea() : (Double)
```

#### 4.3.2 Function Declaration Modifiers

- `[internal]`: Optional. Limits function access to the same program.
- `[visibility]`: Optional. Can be `private`, `protected`, or `public` (defaults to `private`).
- `[abstract]`: Optional. Declares that this function can be accessed without initializing the class it belongs to.
- `[static]`: Optional. Declares a class-level function.

#### 4.3.3 Function Declaration Components

- **functionName**: Required. Must follow camelCase.
- **Parameters**: Each parameter defined as `paramName : Type`, separated by commas.
- **ReturnType**: Optional. Specify in parentheses after the colon. Use `void` or omit if no return value. You can have as many return values as wanted.
- **Function Body**: Enclosed in curly braces `{}`.

#### 4.3.4 Returning Values

To return values from a function, use the `return` keyword followed by the value(s) to be returned. If the function specifies multiple return types, separate the returned values with commas.

```go
func add(a : Int, b : Int) : (Int) {
    return a + b
}

func getCoordinates() : (Int, Int) {
    return 10, 20
}
```

If the function does not return a value, omit the `return` statement or use `return` without arguments.

```go
func logMessage(message : SliceChar) {
    print(message)
    return
}

func logMessage(message : SliceChar) {
    print(message)
}
```

#### 4.3.5 Unreachable Code Detection

If a function contains a mandatory `return` statement and unreachable code follows it, the compiler will allow compilation but will emit a warning indicating the presence of unreachable code. Unlike languages such as Golang, which treat unreachable code after a required return as a compilation error, Celeris permits it but highlights the issue to the developer during compilation.

```go
func foo() : (Int) {
    return 42
    print("This code is unreachable") // Warning: unreachable code
}
```

> **Note:** While the code compiles, it is recommended to remove unreachable statements to maintain code clarity and avoid potential logic errors.


### 4.4 Expressions

Expressions in Celeris are combinations of literals, variables, operators, and function calls that evaluate to a value.

##### Examples

```go
var sum = a + b * 2
var isAdult = age >= 18 && isActive
var message = "Hello, " + name
var result = calculateArea(width, height)
```

#### 4.4.1 String Interpolation

SliceChar literals support string interpolation using `$variable` syntax:

```go
var greeting = "Hello, $userName!"
```

#### 4.4.2 String Mutability

`SliceChar` is a mutable string type with a fixed initial size that can be changed dynamically. This means its contents can be modified (characters replaced, appended, or removed), but its mutability is limited by the current allocated size. Expanding or shrinking requires resizing the underlying storage.

#### 4.4.3 Function Calls

Functions can be called within expressions:

```go
var area = getWidth() * getHeight()
```

#### 4.4.4 Conditional Expressions

Celeris supports conditional (ternary-like) expressions:

```go
var status = isActive ? "Active" : "Inactive"
```

#### 4.4.5 Assignment Expressions

Assignment is also an expression and can be chained:

```go
var x = y = z = 0
```

#### 4.4.6 Type Casting

##### 4.4.6.1 Explicit Casting

Explicit type casting is often used when implicit casting is not possible. This typically occurs when converting between types where information may be lost. For example, casting from `Int<8>` to `Int<2>` results in the loss of 252 possible values, or casting from `Float` to `Int` discards the decimal part.

Explicit casting is also required when converting objects between types, such as casting a `Pet` object to a `Dog` object.

```go
var smallInt : Int<8> = 100
var largeInt : Int<32> = ((Int<32>) smallInt)    // Explicit cast

var floatValue : Float = 3.75F
var intValue : Int = ((Int) floatValue)          // Casts to Int, decimal part discarded

// Object casting
var pet : Pet = Dog()
var dog : Dog = ((Dog) pet)                      // Casts Pet to Dog

// If the cast is invalid, a runtime error is thrown.
```

##### 4.4.6.2 Implicit Casting

Implicit type casting occurs automatically when there is no loss of information and the conversion is safe. For example, converting from `Int<2>` to `Int<32>` preserves all data, or converting from `Int` to `Float` simply adds precision without losing values. In these cases, no additional code is required, and implicit casting is commonly used in function parameters and assignments.

### 4.5 Classes, Interfaces and Enums

#### 4.5.1 Classes

Classes are user-defined types that encapsulate data and behavior.

> **Warning:** A subclass can only inherit one single class or abstract class, and as many interfaces as desired.

```go
class UserProfile {
    var name : SliceChar
    var age : Int

    func greet() {
        // Implementation
    }
}
```

Classes can include inheritance by implementing other classes or interfaces. To inherit and implement a function from a superclass or interface, simply declare the function with the same name; there is no need to use an `override` keyword as in other languages.

```go
abstract class Pet {
    var name : SliceChar
    var age : Int

    abstract func pet()
}

class Dog : Pet {
    func pet() {
        print("$name is happy!")
    }
}
```

#### 4.5.2 Class Declaration Syntax

```go
[internal] [visibility] [abstract] class ClassName {
    // Member variables
    var property : Type

    // Member functions
    func functionName(params) : (ReturnType) {
        // Function body
    }
}
```

- `internal`: Optional modifier. When specified, the class is only accessible from within the same program after compilation. If the class is part of a library, it cannot be accessed externally, but it remains accessible within the program itself.

- `visibility`: Can be either `private` or `public`. The default is `public` if not specified.

- `abstract`: Optional modifier. When specified, the class will be considered an Abstract class.

- Both `internal` and `visibility` are independent modifiers, so combinations like `internal public` or `internal private` are valid.

#### 4.5.3 `this` and `super` Usage

- `this` refers to the current instance of the class. Use `this` to access member variables and functions from within the class.

    ```go
    class Person {
        var name : SliceChar

        func printName() {
            print(this.name) // Accesses the current instance's name
        }
    }
    ```
    
    > Note: If you have multiple variables named `name` and use `print(name)` it will choose first the closest variable, so to use class variable `name` you must use `this.name`.

- `super` is used in a subclass to access functions or constructors from its parent class. Use `super` to call the parent implementation or constructor.

    ```go
    class Animal {
        func makeSound() {
            print("Generic animal sound")
        }
    }

    class Dog : Animal {
        func makeSound() {
            super.makeSound() // Calls Animal's makeSound
            print("Woof!")
        }
    }
    ```

    You can also use `super` in constructors to initialize the parent class:

    ```go
    class Rectangle {
        var width : Int
        var height : Int

        Rectangle(w : Int, h : Int) {
            this.width = w
            this.height = h
        }
    }

    class Square : Rectangle {
        Square(size : Int) {
            super(size, size) // Calls Rectangle's constructor
        }
    }
    ```

> **Note:** Use `this` for accessing the current object's members, and `super` for accessing parent class members or constructors.

#### 4.5.4 Abstract Classes

Abstract classes are special classes that cannot be instantiated directly and may contain abstract functions (functions without implementation). They serve as base classes for other classes to inherit and implement the abstract functions. Abstract classes may also contain functions with implementations.

```go
abstract class Animal {
    var name : SliceChar

    abstract func makeSound()

    func sleep() {
        print("$name is sleeping.")
    }
}
```

A subclass must provide implementations for all abstract functions:

```go
class Cat : Animal {
    func makeSound() {
        // Implementation required
    }
}
```

#### 4.5.5 Inheritance

A class can inherit from a single base class or abstract class and implement _multiple interfaces_:

```go
class Square : Rectangle, Drawable {            // Rectangle : Class | Drawable : Interface
    func draw() {
        print("Drawing square of size $width")
    }
}
```

#### 4.5.6 Constructors

Classes can define constructors for initialization:

```go
class Point {
    var x : Int
    var y : Int

    Point(x : Int, y : Int) {
        this.x = x
        this.y = y
    }
}
```

#### 4.5.7 Object Instantiation

To create a new object, simply call the class constructor as a function with the required parameters. The `new` keyword is not necessary; the compiler will detect object creation automatically.

```go
var origin : Point = Point(0, 0)
```

This syntax instantiates a new `Point` object with `x = 0` and `y = 0`. You can use this pattern for any class:

```go
var user : UserProfile = UserProfile("Alice", 25)
```

If the constructor requires no parameters, you can omit the arguments:

```go
var empty = UserProfile()
```

#### 4.5.8 Interfaces

Interfaces define a contract of functions that implementing classes must provide.

```go
interface Drawable {
    func draw()
}
```

#### 4.5.9 Enumerations

Enums are user-defined types representing a set of named constants.

```go
enum Color {
    RED,
    GREEN,
    BLUE
}
```

#### 4.5.9.2 Enumerations with Values

You can assign values to enum members by specifying a type in the enum declaration and providing values in the constructor. This is useful for representing enums with associated data, such as status codes.

```go
enum HttpStatus(Int) {
    OK = 200,
    NOT_FOUND = 404,
    INTERNAL_ERROR = 500
}
```

##### 4.5.9.3 Enum Methods and Properties

```go
enum Direction {
    NORTH,
    SOUTH,
    EAST,
    WEST

    func opposite() : (Direction) {
        switch (this) {
            case NORTH: return SOUTH
            case SOUTH: return NORTH
            case EAST: return WEST
            case WEST: return EAST
        }
    }

    func toString() : (SliceChar) {
        switch (this) {
            case NORTH: return "North"
            case SOUTH: return "South"
            case EAST: return "East"
            case WEST: return "West"
        }
    }
}
```

##### 4.5.9.4 Using Enumerations

```go
var currentDirection : Direction = Direction.NORTH
var status : HttpStatus = HttpStatus.OK

if (currentDirection == Direction.NORTH) {
    print("Moving north")
}

var oppositeDir = currentDirection.opposite()
print("Opposite direction: $oppositeDir.toString()")
```

### 4.6 Statements

Statements in Celeris are instructions that perform actions such as variable assignment, function calls, control flow, and exception handling. Each statement can end with a semicolon (`;`), though it may be optional for inline statements.

#### 4.6.1 Statement Types

- **Declaration Statements:** Define variables, constants, classes, functions, etc.
- **Assignment Statements:** Assign values to variables.
- **Expression Statements:** Evaluate expressions, often for side effects.
- **Control Flow Statements:** Direct program execution (e.g., `if`, `for`, `while`, `switch`).
- **Loop Statements:** Repeat actions (e.g., `for`, `while`, `do-while`, `stream`).
- **Exception Handling Statements:** Manage errors (`try`, `catch`, `finally`, `throw`).
- **Return Statements:** Return values from functions.
- **Break/Continue Statements:** Alter loop execution.

> **Note:** Statements can be nested within blocks `{}` to form compound statements.

#### 4.6.2 Control Flow Statements

Control flow statements determine the execution path of a program based on conditions or branching logic.

##### 4.6.2.1 Conditional Statements

- **If Statement:** Executes a block if the condition is true.
    ```go
    if (condition) {
        // code if condition is true
    }
    ```

- **If-Else Statement:** Executes one block if the condition is true, another if false.
    ```go
    if (condition) {
        // code if true
    } else {
        // code if false
    }
    ```

- **Else If Statement:** Chains multiple conditions.
    ```go
    if (a > b) {
        // code
    } else if (a == b) {
        // code
    } else {
        // code
    }
    ```

- **Switch Statement:** Selects execution based on the value of an expression.

    ```go
    switch (value) {
        case 1:
            // code for case 1
            break
        case 2:
            // code for case 2
            break
        default:
            // code if no case matches
            break
    }
    ```

> **Note:** If a `break` statement is omitted in a `switch` case, the compiler will not allow compilation and will emit an error.

##### 4.6.2.2 Branching Statements

- **Break:** Exits the nearest enclosing loop or switch.
    ```go
    break
    ```

- **Continue:** Skips to the next iteration of the loop.
    ```go
    continue
    ```

- **Return:** Exits a function and optionally returns a value.
    ```go
    return value
    ```

> Control flow statements can be nested and combined to express complex logic.

#### 4.6.3 Loop Statements

Celeris supports several loop constructs for iterative execution:

- **For Loop:** Iterates a block of code a specific number of times.

    ```go
    for (var i = 0; i < 10; i++) {
        print(i)
    }
    ```

    - Initialization: `var i = 0`
    - Condition: `i < 10`
    - Step: `i++` (increment after each iteration)

- **While Loop:** Repeats a block as long as the condition is true.

    ```go
    while (condition) {
        // code to execute
    }
    ```

- **Do-While Loop:** Executes the block at least once, then repeats while the condition is true.

    ```go
    do {
        // code to execute
    } while (condition)
    ```

- **Stream Loop:** Iterates over collections in a functional style.

    ```go
    for (element in collection) {
        // code using element
    }
    ```

> **Note:** All loop statements can use `break` to exit early or `continue` to skip to the next iteration.

##### Example

```go
var numbers : Int[] = [1, 2, 3, 4, 5]

for (var i = 0; i < numbers.length; i++) {
    print(numbers[i])
}

while (flag) {
    // Repeat while flag is true
}

do {
    // Execute at least once
} while (shouldRepeat)

for (num in numbers) {
    print(num)
}
```

#### 4.6.3 Exception Handling Statements

Exception handling in Celeris is performed using `try`, `catch`, `finally`, and `throw` statements. These constructs allow you to manage errors and exceptional conditions gracefully.

##### 4.6.3.1 Try-Catch-Finally Syntax

```go
try {
    // Code that may throw an exception
} catch (e : ExceptionType) {
    // Handle exception
} finally {
    // Code that always executes (optional)
}
```

- The `try` block contains code that may raise exceptions.
- The `catch` block handles exceptions of the specified type.
- The `finally` block executes regardless of whether an exception was thrown.

##### 4.6.3.2 Throwing Exceptions

Use the `throw` statement to raise an exception:

```go
throw ExceptionType("Error message")
```

##### 4.6.3.3 Multiple Catch Blocks

You can use multiple `catch` blocks to handle different exception types:

```go
try {
    // Code
} catch (e : IOException) {
    // Handle IO error
} catch (e : NullPointerException) {
    // Handle null pointer error
}
```

###### Example

```go
func readFile(path : SliceChar) : (SliceChar) {
    try {
        var content = File.read(path)
        return content
    } catch (e : FileNotFoundException) {
        print("File not found: $path")
        throw e
    } finally {
        print("Read operation finished.")
    }
}
```

> **Note:** If an exception is not caught, it propagates up the call stack. Use `throws` in function signatures to declare possible exceptions.

### 4.7 Collections

#### 4.7.1 Type of Collections

Celeris provides several built-in list and collection types:

| Type                | Description                                                                  |
|---------------------|------------------------------------------------------------------------------|
| `List<T>`           | Ordered list of elements of type `T`. Supports indexing and iteration.       |
| `Set<T>`            | Unordered collection of unique elements of type `T`. No duplicates allowed.  |
| `Map<K, V>`         | Key-value mapping from type `K` to type `V`. Keys are unique.                |
| `Queue<T>`          | FIFO (First-In, First-Out) queue of elements of type `T`.                    |
| `Stack<T>`          | LIFO (Last-In, First-Out) stack of elements of type `T`.                     |
| `PriorityQueue<T>`  | Priority queue; elements of type `T` must inherit from `PriorityType`.       |
| `PriorityStack<T>`  | Priority stack; elements of type `T` must inherit from `PriorityType`.       |

Each collection type provides methods for adding, removing, and accessing elements according to its semantics.

#### 4.7.2 Collection Inheritance

Collections in Celeris can be extended to create custom data structures. You can inherit from built-in collection types and override or add methods as needed.

```go
class CustomList : List<Int> {
    func sum() : (Int) {
        var total : Int = 0
        for (item in this) {
            total += item
        }
        return total
    }
}
```

You can also implement interfaces to provide additional behaviors:

```go
class UniqueList : List<Int>, Set<Int> {
    func add(item : Int) {
        if (!this.contains(item)) {
            this.append(item)
        }
    }
}
```

> **Note:** When inheriting from a collection type, ensure that you maintain the semantics of the base type (e.g., ordering for `List`, uniqueness for `Set`).

#### 4.7.3 Generic Collections

Collections can be generic, allowing you to specify the type of elements they contain:

```go
var stringList : List<SliceChar> = List<SliceChar>()
var intSet : Set<Int> = Set<Int>()
```

### 4.8 Using

`using` keyword imports classes, interfaces, or entire packages into the current file, granting access to their public members. Example:

```c++
package dev.zanckor.Main

using dev.zanckor.MathUtility  // imports just MathUtility
using dev.zanckor.UserProfile  // imports just UserProfile
using dev.zanckor.*            // imports all members from package dev/zanckor
```

#### 4.8.1 Renaming to avoid conflicts
You can rename an imported class or package using the `as` keyword for easier reference. For example:

```c++
using dev.zanckor.MathUtility as Math
```

#### 4.8.2 Rules

- Just public members are accessible
- `internal` cannot be used outside the same program
- Avoid using Wildcard imports to avoid namespace conflicts.

#### 4.9 Advanced Language Features

##### 4.9.1 Lambda Expressions

##### 4.9.2 Function Extension

---


## 5. Memory Management

Memory management in Celeris is designed to balance safety, performance, and developer control. The language provides both automatic and manual memory management mechanisms, allowing developers to choose the most appropriate strategy for their use case.

### 5.1 Automatic Memory Management

Automatic memory management in Celeris is primarily handled through a built-in garbage collector (GC). The GC automatically tracks object lifetimes and reclaims memory that is no longer referenced, reducing the risk of memory leaks and freeing developers from manual deallocation for most use cases.

Objects allocated on the heap are monitored by the GC, which periodically scans for unreachable objects and releases their memory. Stack allocation is managed automatically by the compiler, with memory being reclaimed when variables go out of scope.

Developers do not need to explicitly free memory for objects managed by the GC. However, for performance-critical scenarios or when working with resources outside the GC's control (such as file handles or network sockets), manual memory management features are available.

The GC is designed to minimize pause times and system impact, using incremental and generational collection strategies. This ensures responsive applications even under heavy allocation workloads.

> **Note:** While automatic memory management simplifies development, understanding GC behavior and object lifetimes is important for writing efficient and predictable code.

#### 5.1.1 Garbage Collection (GC)

Celeris uses a hybrid generational GC designed for multi-threaded environments, with the following structure:

- **Heap Layout:**
  - **Young Spaces:** Each thread has its own Young Space, starting at 256 KB–1 MB.
  - **Old Generation:** Shared among all threads, organized in segregated heaps for large objects.
- **Allocation:**
  - Objects are allocated in the Young Space using a bump pointer.
  - Large objects (>256 KB) are allocated faster in the Old Generation.
- **Promotion:**
  - Objects survive **3 Young GC cycles** before promotion to the Old Generation.
  - Large objects survive **1 Young GC Cycle** before promotion to the Old Generation. 
  - Static or global objects are promoted immediately.
- **Reference Counting:**
  - Young Space uses immediate RC.
  - Old Generation uses Lazy RC.
- **Cycle Collector:** Incremental CC runs on both Young and Old generations.
- **Compactation:** Old Generation uses incremental compaction to reduce pauses.
- **Caching & Locality:** Objects allocated by the same thread are contiguous to improve cache hits.

#### 5.1.2 GC Behaviour & System Impact

##### System Impact

- **Thread-local Young Spaces:** Reduces lock contention and improves cache locality.
- **Shared Old Generation:** Access controlled by region locks and write barriers.
- **Incremental GC:** Minimizes pause times by processing Old Generation in regions.
- **Lazy RC & CC:** Reduces GC overhead by deferring checks and collecting cycles incrementally.
- **Memory Movement:** Handled via handle tables to avoid scanning all references.
- **Large Object Handling:** Allocated in segregated OG regions to prevent frequent copying.
- **Impact on Performance:**
  - Thread-local allocations minimize synchronization overhead.
  - Incremental and lazy approaches minimize long GC pauses.
  - Compacting OG ensures low fragmentation and maintains spatial locality.
##### GC Behaviour

###### Life Cycle

The **Garbage Collector (GC)** in Celeris manages memory by automatically allocating, promoting, and reclaiming objects. Its main goal is to efficiently handle short-lived and long-lived objects, minimizing pauses and maximizing throughput.

##### Memory Regions

Memory is divided into **two main regions**:

###### 1. Young Generation (YG)

* Contains objects that are newly created and are expected to have a short lifespan
* Collected frequently with fast, efficient algorithms (e.g., *minor GC*)
* Designed to be small and thread-local for fast allocation

###### 2. Old Generation (OG)

* Holds objects that survived multiple Young Generation collections
* Collected less frequently, usually with a more expensive *major GC*
* Can grow backward using a **bidirectional bump pointer**, absorbing extra Free Space dynamically
* **Memory requests are handled by the compiler**, which always requests additional heap memory **before OG** to avoid moving OG and maintain contiguity
* If, for any reason, the system provides memory at the end instead of before OG, the GC still handles it according to the standard plan with minimal impact

> **The GC Life Cycle** in Celeris is the process through which memory is managed across these regions, including allocation in the Young Generation, promotion to the Old Generation, and reclamation of unused memory.

---

###### Local-Thread Dynamic Young Generations

**1. Initial Assignment**

Each Thread starts with **\~256 KB to 1 MB**, depending on software requirements. The total Young Generation space is about `30%` of the initial heap.

**Memory Map (initial)**

```
[ YG T1 ][ Slack 1 ][ YG T2 ][ Slack 2 ][ Free Space ][ OG ]
```

Where:

* **OG** = Old Generation
* **YG Tx** = Young Generation Thread X

**2. Dynamic Increase**

Celeris reserves a `[ Slack ]` after each Young Generation so that a thread can extend its memory if it uses all its space.

```
[ YG T1 ][ Slack 1 ][ YG T2 ][ Slack 2 ][ Free Space ][ OG ]
```

**3. Maximum Space Reached**

When a Young Generation reaches its memory pool `[YG T1 + Slack 1]`:

* Memory is copied to Free Space if contiguous space is not available
* If there is Free Space directly after the YG, no copy is needed; a new Slack is allocated there

**Example State:**

```
[ YG T1 ][ Free Space ][ OG ]
```

**After Expansion:**

```
[ YG T1 ][ New Slack 1 ][ Free Space ][ OG ]
```

> This reduces unnecessary copying when memory is already contiguous.

**4. Heap Bump Pointer**

* Points to the next free memory location within a YG for fast allocation
* When it reaches the end of YG, it uses the thread's Slack
* If Slack is exhausted, memory is relocated or Free Space is expanded

**5. Heap Bump Pointer on Free Memory**

* When memory is released, bump pointers are not immediately updated
* They are adjusted during the **Relocate Memory** process to point to the last allocated memory after relocation

---

###### Global-Thread Bidirectional Old Generation

**1. Initial Assignment**

* OG starts at the end of the heap and grows **backward** using a backward bump pointer
* Initially sized to accommodate expected long-lived objects
* **All memory requests for expansion are made by the compiler before OG** to maintain contiguity and avoid moving OG

**2. Dynamic Increase**

* If the system assigns more heap memory, the **extra Free Space** can be absorbed incrementally by OG
* Bump pointer moves backward to include Free Space extra without moving existing OG objects immediately when memory is relocated
* If memory is assigned at the end instead of before OG, the GC continues using the existing plan with minimal impact

**Example of memory being assigned at the end of the heap**

*Example State Before Absorption:*

```
[ YG1 ][ YG2 ][ Free Space ][ OG ← backward bump pointer ][ Free Space extra ]
```

*After Absorption of Free Space Extra:*

```
[ YG1 ][ YG2 ][ Free Space ][ OG + Free Space extra ← backward bump pointer ]
```

**3. Incremental Relocation**

OG data can be **moved gradually** toward the new end of OG for contiguity:

**Before:**

```
[ YG1 ][ YG2 ][ Free Space ][ ########### OOOOOOOOOO ]
```

**After:**

```
[ YG1 ][ YG2 ][ Free Space ][ OOOOOOOOOO ← backward bump pointer ########### ]
```

Legend:

* `O` = New Empty memory
* `#` = Old Space memory

> Minimizes pause times by avoiding a full OG copy.

**4. Free Space Release**

If the old OG space becomes larger than a threshold (e.g., 50% of heap), it is released:

```
[ YG1 ][ YG2 ][ Free Space + Previous OG ][ OOOOOO ########### ]
```

This ensures efficient reuse of memory while keeping OG contiguous.

**5. Heap Bump Pointer**

* Indicates the current end of OG (backward)
* Adjusted as OG absorbs Free Space extra or relocates objects
* Never allows new YG allocations **behind OG**

**6. Heap Bump Pointer on Free Memory**

* When OG memory is no longer used, bump pointer is updated during the **Relocate Memory** process to point to the last allocated memory of OG

###### Behaviour

1. **Memory Dictionary Allocation Phase:**

2. **Memory Allocation Phase:**

3. **Minor Collection (Young GC):**  

4. **Promotion:**

5. **Major Collection (Old GC):**  

6. **Cycle Collection:**  

7. **Finalization:**  


---

##### Reference Counting

###### Fast Reference Counting

###### Lazy Reference Counting

###### Behaviour

---

##### Cycle Collector

---

##### Relocate Memory

###### Incremental Relocation

###### Concurrent Relocation

###### Behaviour


---

##### Range Segregation

---

##### Multi-Thread Heap 


### 5.2 Manual Memory Management

#### 5.2.1 Allocate / Delete (heap management)

#### 5.2.2 Scope-based resource management allocation

#### 5.2.3 Ownership & responsabilidades

#### 5.2.4 Avoiding double free & dangling pointers

#### 5.2.5 Memory pools & object reuse

### 5.3 Punteros (Pointers)

#### 5.3.1 Declaration & unreference (* y &)

#### 5.3.2 Null pointers & runtime errors

#### 5.3.3 Const pointers & punteros read-only

#### 5.3.4 Pointers and functions (Reference parameters)

#### 5.3.5 Difference between pointers and safe references (ref)

#### 5.3.6 Pointer arithmetic

### 5.4 Memory Safety

#### 5.4.1 Dangling pointers & safe usage

#### 5.4.2 Bounds checking on arrays / slices

#### 5.4.3 Immutable vs mutable objects

#### 5.4.4 Thread-safe memory access

### 5.5 Performance Considerations

#### 5.5.1 Minimize GC pauses

#### 5.5.2 Avoid memory fragmentation

#### 5.5.3 Optimization for threads and concurrency

#### 5.5.4 Memory pooling & caching

### 5.6 Advanced Features

#### 5.6.1 Smart pointers / RAII wrappers

#### 5.6.2 Weak references for temporary objects

#### 5.6.3 Finalizers / destructors


---

## 6. Package System

*[Content to be added]*

### 6.1 Package Declaration

*[Content to be added]*

### 6.2 Import System

*[Content to be added]*

### 6.3 Module Resolution

*[Content to be added]*

---

## 7. Error Handling

*[Content to be added]*

### 7.1 Exception Types

*[Content to be added]*

### 7.2 Try-Catch-Finally

*[Content to be added]*

### 7.3 Custom Exceptions

*[Content to be added]*

---

## 8. Compilation Model

*[Content to be added]*

### 8.1 Compilation Phases

*[Content to be added]*

### 8.2 Code Generation

*[Content to be added]*

### 8.3 Optimization

*[Content to be added]*

---

## 9. Standard Library

*[Content to be added]*

### 9.1 Core Types

*[Content to be added]*

### 9.2 Collections

*[Content to be added]*

### 9.3 I/O Operations

*[Content to be added]*

### 9.4 Utility Functions

*[Content to be added]*

---

## 10. Advanced Features

*[Content to be added]*

### 10.1 Generics

*[Content to be added]*

### 10.2 Reflection

*[Content to be added]*

### 10.3 Annotations

*[Content to be added]*

---

## 11. Performance Considerations

*[Content to be added]*

### 11.1 Runtime Performance

*[Content to be added]*

### 11.2 Memory Usage

*[Content to be added]*

### 11.3 Optimization Guidelines

*[Content to be added]*

---

## 12. Appendices

### Appendix A: Grammar Reference

*[Content to be added]*

### Appendix B: Keyword Index

*[Content to be added]*

### Appendix C: Examples and Use Cases

*[Content to be added]*