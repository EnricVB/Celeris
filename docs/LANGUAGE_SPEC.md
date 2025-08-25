# COMPILER_SPEC.md
# Specs of CSpeedy MiniLang

## 1. Sumarazing
Language for CSpeedy designed to be read by **CSAOT**.

## 2. Lexical Structure
The lexical structure of CSpeedy MiniLang consists of the following elements:

### 2.1 Whitespace
Whitespace characters (spaces, tabs, newlines) are used to separate tokens and improve readability. They are generally ignored except when separating tokens.

### 2.2 Comments
Comments are ignored by the compiler and can be single-line or multi-line.

- **Single-line comments** start with `//` and continue to the end of the line.
    ```go
    // This is a single-line comment
    ```
- **Multi-line comments** are enclosed between `/*` and `*/`.
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

- **Documentation Comments**
    ```go
    /**
     * This is a documentation comment.
     */

### 2.3 Identifiers
Identifiers are names for variables, functions, classes, etc. They must start with a letter (A-Z, a-z) or underscore (`_`), followed by letters, digits (0-9), or underscores.

### 2.4 Nomenclature Standar
#### Packages
Package names must be singular, in lowercase, and use camelCase if composed. Example: `mathUtility`

#### Classes
Class names must start with an uppercase letter, be singular, and not exceed three words. Example: `UserProfile`

#### Functions
Function names must be in camelCase, start with a lowercase letter, and use descriptive verbs. Example: `calculateTriangleArea`

#### Variables
Variable names must be in camelCase, start with a lowercase letter, and be descriptive. Avoid abbreviations unless widely recognized. Example: `userAge`, `totalAmount`.


### 2.5 Literals
Literals represent fixed values in the source code:
- **Integer literals:** `42`, `-7`
- **Byte literals:** `0xFF`, `255`, `b'Z'`
- **Long literals:** `1234567890123L`, `-9876543210L`
- **Floating-point literals:** `3.14`, `-0.001`, `4F`
- **Double literals:** `3.14159D`, `-2.71828D`
- **Character literals:** `'A'`, `'9'`
- **SliceChar literals:** `"Hello, World!"`
- **Boolean literals:** `true`, `false`, `0`, `1`
- **Null literal:** `null`

### 2.5 Operators, Symbols and Delimiters
Operators and delimiters include symbols for arithmetic, logical, comparison, assignment, and grouping, as listed in the keywords section.

| Symbol                | Explanation                                         |
|-----------------------|-----------------------------------------------------|
| [ ]                   | Array declaration and indexing                      |
| { }                   | Delimiters for functions, classes, and code blocks  |
| +                     | Addition operator                                   |
| -                     | Subtraction operator                                |
| *                     | Multiplication operator                             |
| /                     | Division operator                                   |
| %                     | Modulo operator                                     |
| =                     | Assignment operator                                 |
| ++                    | Increment operator                                  |
| --                    | Decrement operator                                  |
| &&                    | Logical AND operator                                |
| \|\|                  | Logical OR operator                                 |
| !                     | Logical NOT operator                                |
| &                     | Bitwise AND operator                                |
| \|                    | Bitwise OR operator                                 |
| ^                     | Bitwise XOR operator                                |
| ~                     | Bitwise NOT operator                                |
| <<                    | Bitwise left shift                                  |
| >>                    | Bitwise right shift                                 |
| ==                    | Equality comparison                                 |
| !=                    | Inequality comparison                               |
| <                     | Less than comparison                                |
| >                     | Greater than comparison                             |
| <=                    | Less than or equal comparison                       |
| >=                    | Greater than or equal comparison                    |
| .                     | Member access or method call                        |
| ,                     | Separator for arguments or elements                 |
| ;                     | Statement terminator (Optional for inline)          |
| :                     | Type annotation or label                            |
| ()                    | Function call or grouping expressions               |
| $variable             | Used for string interpolation within SliceChar literals. Example: `"Hello, $name!"` |

### 2.6 Keywords
The language is tokenized into keywords, identifiers, literals, operators, and delimiters. Tokens are separated by whitespace or delimiters.

| Conditional Words | Explanation                                   |
|-------------------|-----------------------------------------------|
| IF                | Conditional statement                         |
| ELSE              | Alternative conditional branch                |
| ELSE IF           | Conditional "else if" branch                  |
| SWITCH            | Multi-branch selection                        |
| CASE              | Case in a switch                              |
| DEFAULT           | Specifies default case in switch statements   |

| Flow Words        | Explanation                                   |
|-------------------|-----------------------------------------------|
| DO                | Do-while loop                                 |
| WHILE             | While loop                                    |
| FOR               | For loop                                      |
| STREAM            | Functional iterator over collections          |
| BREAK             | Exit loop or switch                           |
| CONTINUE          | Skip to next iteration of loop                |
| RETURN            | Return from function                          |
| DELETE            | Manual memory deallocation                    |

| Error Words       | Explanation                                   |
|-------------------|-----------------------------------------------|
| TRY               | Start of exception handling                   |
| CATCH             | Exception handling block                      |
| FINALLY           | Block executed after try/catch                |
| THROW             | Raise an exception                            |
| THROWS            | Declare exceptions a function can raise       |

| Encapsulation Words | Explanation                                 |
|---------------------|---------------------------------------------|
| PRIVATE             | Private access modifier                     |
| PROTECTED           | Protected access modifier                   |
| PUBLIC              | Public access modifier                      |
| INTERNAL            | Compilation access modifier, only allows to access from the same program |

| Inheritance Words  | Explanation                                          |
|--------------------|------------------------------------------------------|
| ENUM               | Enumeration type                                     |
| CLASS              | Class declaration                                    |
| INTERFACE          | Interface declaration                                |
| : or IMPLEMENTS    | Indicates a class implements an interface or class   |
| INSTANCEOF         | Checks type of an object                             |
| STATIC             | Static member of a file                              |
| SUPER              | Access parent class methods or constructor           |
| THIS               | Reference to the current instance                    |

| Miscelaneous Keywords | Explanation                                          |
|-----------------------|------------------------------------------------------|
| CONST                 | Constant value declaration                           |
| PACKAGE               | Package declaration                                  |
| USING                 | Import or include another package/module             |
| TRUE                  | Boolean true value                                   |
| FALSE                 | Boolean false value                                  |
| NULL                  | Null reference                                       |
| SIZEOF                | Returns the size in bytes of a data type or variable |
| VAR                   | Declares a variable with inferred or explicit type  |
| Data Types            | Any data type is a keyword                           |

### 2.7 Escape Sequences
String and character literals support escape sequences such as `\n` (newline), `\t` (tab), `\\` (backslash), `\'` (single quote), and `\"` (double quote).

## 3. Types

CSpeedy supports a variety of built-in types and allows for user-defined types.

### 3.1 Primitive Types

| Type          | Explanation                                   | Size                          | Range                                                     |
|---------------|-----------------------------------------------|-------------------------------|-----------------------------------------------------------|
| Bool          | Boolean type (true/false)                     | 1 byte                        | true / false                                              |
| Char          | A single character                            | 1 byte                        | 0 to 255                                                  |
| SliceChar     | An array of slizable chars. Length can change | variable (Default 255 Chars)  | Depends on length                                         |
| Int           | Integer type of a number                      | 4 bytes                       | -2,147,483,648 to 2,147,483,647                           |
| Byte          | Smallest data type                            | 1 byte                        | 0 to 255                                                  |
| Short         | Small integer                                 | 2 bytes                       | -32,768 to 32,767                                         |
| Long          | Large integer                                 | 8 bytes                       | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807   |
| Float         | Single precision floating point               | 4 bytes                       | ±1.18×10⁻³⁸ to ±3.4×10³⁸                                  |
| Double        | Double precision floating point               | 8 bytes                       | ±2.22×10⁻³⁰⁸ to ±1.79×10³⁰⁸                               |

### 3.2 Composite Types

#### Arrays

Arrays are fixed-size and mutable, non-ordered collections of elements of the same type.

```go
var numbers : Int[5] = [1, 2, 3, 4, 5]
```

#### Slices

Slices are dynamically-sized sequences of elements. `SliceChar` is a built-in slice type for characters.

```go
var message : SliceChar = "Hello, World!"
```

#### Classes

Classes are user-defined types that encapsulate data and behavior.
Warning: A subclass can only inherit one single class or abstract class, and how much interfaces it wants.

```go
class UserProfile {
    var name : SliceChar
    var age : Int

    func greet() {
        // Implementation
    }
}
```

Classes can include inheritance implementing other classes or interfaces.

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

#### Abstract Classes
Abstract classes are special classes that cannot be instantiated directly and may contain abstract methods (methods without implementation). They serve as base classes for other classes to inherit and implement the abstract methods. And may or may not contain functions with features

```go
class Animal {
    var name : SliceChar

    abstract func makeSound()

    func sleep() {
        print("$name is sleeping.")
    }
}
```

A subclass must provide implementations for all abstract methods:

```go
class Cat : Animal {
    func makeSound()
}
```

#### Interfaces

Interfaces define a contract of methods that implementing classes must provide.

```go
interface Drawable {
    func draw()
}
```

#### Enum

Enums are user-defined types representing a set of named constants.

```go
enum Color {
    RED,
    GREEN,
    BLUE
}
```

### 3.3 Default Values

When a variable is declared but not explicitly initialized, it is assigned a default value based on its type:

| Type        | Default Value       |
|-------------|---------------------|
| Bool        | `false`             |
| Char        | `null`              |
| SliceChar   | `""` (empty string) |
| Int         | `0`                 |
| Byte        | `0`                 |
| Short       | `0`                 |
| Long        | `0L`                |
| Float       | `0.0F`              |
| Double      | `0.0D`              |
| Object/Class| `null`              |
| Array       | `null`              |

#### Example

```go
var flag : Bool         // flag is false
var count : Int         // count is 0
var name : SliceChar    // name is ""
var user : UserProfile  // user is null
```

## 4. Language Usage

### 4.1 Variables

Variables in CSpeedy are declared using the `var` keyword, followed by the variable name and an optional type annotation. Initialization can be performed at the time of declaration.

#### Declaration

To declare a variable in CSpeedy, use the following syntax:

```go
var <variableName> : <Type?>
```

- `var` is the keyword for variable declaration.
- `variableName` is the identifier for the variable. Must be unique in the context, as not having 2 variables named exactly the same on a function or class.
- `Type` is the data type of the variable. Must be inferenced.

#### Example

```go
var age : Int
var name : SliceChar
var isActive : Bool
```

#### Initialization

To initialize a variable at the time of declaration, assign a value using the assignment operator `=`:

```go
var age : Int = 25
var name : SliceChar = "Alice"
var isActive : Bool = true
```

You can also declare and initialize arrays and objects:

```go
var numbers : Int[] = [1, 2, 3]
var user : UserProfile = new UserProfile()
```

#### Multiple Assignment

CSpeedy supports multiple assignment, allowing you to assign values to several variables simultaneously in a single statement. The values are assigned in the order they appear.

```go
var a, b, c = 1, 2, 3
// a = 1, b = 2, c = 3
```

This feature is useful when unpacking values from functions that return tuples or multiple results.

```go
func getUserInfo() : (SliceChar, Int, Bool) {
    return "Bob", 30, true
}

var name, age, isActive = getUserInfo()
// name = "Bob", age = 30, isActive = true
```

#### Type Inference

CSpeedy supports type inference, allowing the compiler to automatically deduce the type of a variable from its initializer. When a variable is declared without an explicit type annotation, the compiler infers its type based on the assigned value.

#### Example
```go
var inferred = 42        // Type inferred as Int
var message = "Hello"    // Type inferred as SliceChar
var flag = true          // Type inferred as Bool
```

Type inference improves code readability and reduces verbosity, but explicit type annotations can still be used for clarity or when the type cannot be determined from the initializer.

> **Note:** If a variable is declared without an initializer, type inference cannot be applied. In such cases, an explicit type annotation is required.

#### Example
```go
var value           // Invalid: type cannot be inferred
var value : Int     // Valid: explicit type annotation
```


### 4.2 Constants and Static

#### Constants

Constants are declared using the `const` keyword. A constant is read-only and its value cannot be changed after initialization.

```go
const PI : Double = 3.14159D
const greeting : SliceChar = "Hello"
```

#### Static Variables and Methods

The `static` keyword is used to declare variables or methods that belong to the class itself rather than to any instance. Static members can be accessed at any time during execution, without creating an instance of the class.

```go
class MathUtils {
    static var counter : Int = 0

    static func increment() {
        counter = counter + 1
    }
}
```

#### Combining `const` and `static`

You can use both `const` and `static` together to declare class-level constants.

```go
class Config {
    static const MAX_USERS : Int = 100
}
```

- `const` makes a variable read-only.
- `static` allows access without instantiating the class.
- Both can be combined for global constants.

### 4.3 Functions

Functions are declared using the `func` keyword as follows:

```go
[internal] [visibility=private] [static] func functionName(param1 : Type1, param2 : Type2, ...) : (ReturnType) {
    // function body
}
```

- **[internal]**: Optional. Limits function access to the same program.
- **[visibility]**: Optional. Can be `private`, `protected`, or `public`. Defaults to `private`.
- **[static]**: Optional. Declares a class-level function.
- **functionName**: Required. Must follow camelCase.
- **Parameters**: Each parameter is defined as `paramName : Type`, separated by commas.
- **ReturnType**: Optional. Specify in parentheses after the colon. Use `void` or omit if no return value.
- **Function Body**: Enclosed in curly braces `{}`.

- `internal` is optional and specifies that the function is accessible only within the same program.
- `visibility` is optional and can be `private`, `protected`, or `public`. If omitted, the default is `private`.
- `static` is optional and declares class-level functions that do not require an instance.
- `functionName` is the name of the function and must follow camelCase naming conventions.
- Parameters are defined as `<paramName : <type>>`, separated by commas. They can be omitted if the function takes no arguments.
- The return type is specified in parentheses after the colon. If the function does not return a value, it can be omitted or use `void`.
- The function body is enclosed in curly braces `{}`.

Example of a public static function with parameters and a return value:
```go
// Example: Public static function with parameters and a return value
public static func sum(a : Int, b : Int) : (Int) {
    return a + b
}

// Example: Public function accessible only within the same compiled program, with parameters and no return value
internal public func execute(task : Task) {
    print("Executing task: $task.name")
}

// Example: Private function with no parameters and no return value
func initialize() {
    // Perform initialization logic here
}

// Example: Abstract function in a class or interface (no body)
abstract func calculateArea() : (Double)
```

Functions can be declared globally, as class members, or within interfaces. Abstract functions omit the body and must be implemented by subclasses or implementing classes.

### 4.4 Expressions

Expressions in CSpeedy are combinations of literals, variables, operators, and function calls that evaluate to a value. They can be used wherever a value is expected, such as in assignments, function arguments, or control statements.

#### Examples

```go
var sum = a + b * 2
var isAdult = age >= 18 && isActive
var message = "Hello, " + name
var result = calculateArea(width, height)
```

Expressions can include arithmetic, logical, comparison, and method call operations. Parentheses can be used to group sub-expressions and control evaluation order.

#### String Interpolation

SliceChar literals support string interpolation using `$variable` syntax:

```go
var greeting = "Hello, $userName!"
```

### String Mutability

SliceChar is a mutable string type with a fixed initial size X, which can be changed dynamically. This means its contents can be modified (characters replaced, appended, or removed), but its mutability is limited by the current allocated size. Expanding or shrinking the SliceChar requires resizing the underlying storage, which is supported by the language. This design provides faster access and manipulation compared to fully dynamic strings, while still allowing controlled mutability.

#### Function Calls

Functions can be called within expressions:

```go
var area = getWidth() * getHeight()
```

#### Conditional Expressions

CSpeedy supports conditional (ternary-like) expressions using the following syntax:

```go
var status = isActive ? "Active" : "Inactive"
```

#### Assignment Expressions

Assignment is also an expression and can be chained:

```go
var x = y = z = 0
```

#### Type Casting

Explicit type casting can be performed using the cast operator:

```go
var value : Double = (Double) intValue
```

### 4.5 Classes, Interfaces and Enum

### 4.6 Statements

## 3.1 Stream

```go
func foo() {
    var data : Number[] = null

    stream (obj in data) => {
        // Anything
    }
}

func foo() {
    var data : Number[] = null

    for (obj : data) {
        // Anything
    }
}
```