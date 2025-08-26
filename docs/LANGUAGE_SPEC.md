# **CSpeedy Compiler Specification**

## 1. **Overview**

Language for CSpeedy designed to be read by **CSAOT**.

---

## 2. **Lexical Structure**

The lexical structure of CSpeedy MiniLang consists of the following elements:

### 2.1 **Whitespace**

Whitespace characters (spaces, tabs, newlines) are used to separate tokens and improve readability. They are generally ignored except when separating tokens.

### 2.2 **Comments**

Comments are ignored by the compiler and can be single-line or multi-line.

#### **Single-line Comments**
Start with `//` and continue to the end of the line.
```go
// This is a single-line comment
```

#### **Multi-line Comments**
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

#### **Documentation Comments**
```go
/**
 * This is a documentation comment.
 */
```

### 2.3 **Identifiers**

Identifiers are names for variables, functions, classes, etc. They must start with a letter (A-Z, a-z) or underscore (`_`), followed by letters, digits (0-9), or underscores.

### 2.4 **Nomenclature Standards**

#### **Packages**
Package names must be singular, in lowercase, and use camelCase if composed. 
- **Example:** `mathUtility`

#### **Classes**
Class names must start with an uppercase letter, be singular, and not exceed three words. 
- **Example:** `UserProfile`

#### **Functions**
Function names must be in camelCase, start with a lowercase letter, and use descriptive verbs. 
- **Example:** `calculateTriangleArea`

#### **Variables**
Variable names must be in camelCase, start with a lowercase letter, and be descriptive. Avoid abbreviations unless widely recognized. 
- **Examples:** `userAge`, `totalAmount`

### **2.5 Literals**

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

### **2.6 Operators, Symbols and Delimiters**

| Symbol    | Explanation                                           |
|-----------|-------------------------------------------------------|
| `[ ]`     | Array declaration and indexing                        |
| `{ }` | Delimiters for functions, classes, and code blocks;  
| `+` | Addition operator;  
| `-` | Subtraction operator;  
| `*` | Multiplication operator;  
| `/` | Division operator;  
| `%` | Modulo operator;  
| `=` | Assignment operator;  
| `++` | Increment operator (increases value by 1; if used before the value, increments before the operation; if after, increments after);  
| `--` | Decrement operator (decreases value by 1; if used before the value, decrements before the operation; if after, decrements after);  
| `&&` | Logical AND operator;  
| `\|\|` | Logical OR operator;  
| `!` | Logical NOT operator;  
| `&` | Bitwise AND operator;  
| `\|` | Bitwise OR operator;  
| `^` | Bitwise XOR operator;  
| `~` | Bitwise NOT operator;  
| `<<` | Bitwise left shift;  
| `>>` | Bitwise right shift;  
| `==` | Equality comparison;  
| `!=` | Inequality comparison;  
| `<` | Less than comparison;  
| `>` | Greater than comparison;
| `<=`      | Less than or equal comparison                         |
| `>=`      | Greater than or equal comparison                      |
| `.`       | Member access or method call                          |
| `,`       | Separator for arguments or elements                   |
| `;`       | Statement terminator (Optional for inline)            |
| `:`       | Type annotation or label                              |
| `()`      | Function call or grouping expressions                 |
| `$variable` | Used for string interpolation within SliceChar literals. Example: `"Hello, $name!"` |

### **2.7 Keywords**

The language is tokenized into keywords, identifiers, literals, operators, and delimiters. Tokens are separated by whitespace or delimiters.

#### **Conditional Words**

| Keyword   | Explanation                                 |
|-----------|---------------------------------------------|
| `IF`      | Conditional statement                       |
| `ELSE`    | Alternative conditional branch              |
| `ELSE IF` | Conditional "else if" branch                |
| `SWITCH`  | Multi-branch selection                      |
| `CASE`    | Case in a switch                            |
| `DEFAULT` | Specifies default case in switch statements |

#### **Flow Control Words**

| Keyword    | Explanation                                |
|------------|--------------------------------------------|
| `DO`       | Do-while loop                              |
| `WHILE`    | While loop                                 |
| `FOR`      | For loop                                   |
| `STREAM`   | Functional iterator over collections       |
| `BREAK`    | Exit loop or switch                        |
| `CONTINUE` | Skip to next iteration of loop             |
| `RETURN`   | Return from function                       |
| `DELETE`   | Manual memory deallocation                 |

#### **Error Handling Words**

| Keyword   | Explanation                               |
|-----------|-------------------------------------------|
| `TRY`     | Start of exception handling               |
| `CATCH`   | Exception handling block                  |
| `FINALLY` | Block executed after try/catch            |
| `THROW`   | Raise an exception                        |
| `THROWS`  | Declare exceptions a function can raise   |

#### **Encapsulation Words**

| Keyword     | Explanation                                                                      |
|-------------|----------------------------------------------------------------------------------|
| `PRIVATE`   | Private access modifier                                                          |
| `PROTECTED` | Protected access modifier                                                        |
| `PUBLIC`    | Public access modifier                                                           |
| `INTERNAL`  | Compilation access modifier, only allows access from the same program           |

#### **Inheritance Words**

| Keyword      | Explanation                                            |
|--------------|--------------------------------------------------------|
| `ENUM`       | Enumeration type                                       |
| `CLASS`      | Class declaration                                      |
| `INTERFACE`  | Interface declaration                                  |
| `:` or `IMPLEMENTS` | Indicates a class implements an interface or class |
| `INSTANCEOF` | Checks type of an object                               |
| `STATIC`     | Static member of a file                                |
| `SUPER`      | Access parent class methods or constructor             |
| `THIS`       | Reference to the current instance                      |

#### **Miscellaneous Keywords**

| Keyword      | Explanation                                          |
|--------------|------------------------------------------------------|
| `CONST`      | Constant value declaration                           |
| `PACKAGE`    | Package declaration                                  |
| `USING`      | Import or include another package/module             |
| `TRUE`       | Boolean true value                                   |
| `FALSE`      | Boolean false value                                  |
| `NULL`       | Null reference                                       |
| `SIZEOF`     | Returns the size in bytes of a data type or variable |
| `VAR`        | Declares a variable with inferred or explicit type   |
| Data Types   | Any data type is a keyword                           |

### **2.8 Escape Sequences**

String and character literals support escape sequences such as `\n` (newline), `\t` (tab), `\\` (backslash), `\'` (single quote), and `\"` (double quote).

---

## **3. Type System**

CSpeedy supports a variety of built-in types and allows for user-defined types.

### **3.1 Primitive Types**

| Type        | Explanation                                     | Size                         | Range                                                     |
|-------------|-------------------------------------------------|------------------------------|-----------------------------------------------------------|
| `Bool`      | Boolean type (true/false)                       | 1 byte                       | `true` / `false`                                          |
| `Char`      | A single character                              | 1 byte                       | 0 to 255                                                  |
| `SliceChar` | An array of resizable chars. Length can change | variable (Default 255 Chars) | Depends on length                                         |
| `Int<T>`       | Integer type of a number. You can specify the bytes this Integer will have. By default 32.                        | 4 bytes                      | -2,147,483,648 to 2,147,483,647                           |
| `Byte`      | Smallest data type                              | 1 byte                       | 0 to 255                                                  |
| `Short`     | Small integer                                   | 2 bytes                      | -32,768 to 32,767                                         |
| `Long`      | Large integer                                   | 8 bytes                      | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807   |
| `Float`     | Single precision floating point                 | 4 bytes                      | ±1.18×10⁻³⁸ to ±3.4×10³⁸                                  |
| `Double`    | Double precision floating point                 | 8 bytes                      | ±2.22×10⁻³⁰⁸ to ±1.79×10³⁰⁸                               |

### **3.2 Composite Types**

#### **Arrays**

Arrays are fixed-size and mutable, non-ordered collections of elements of the same type.

```go
var numbers : Int[5] = [1, 2, 3, 4, 5]
```

#### **Slices**

Slices are dynamically-sized sequences of elements. `SliceChar` is a built-in slice type for characters.

```go
var message : SliceChar = "Hello, World!"
```

#### **Classes**

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

Classes can include inheritance by implementing other classes or interfaces.

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

#### **Abstract Classes**

Abstract classes are special classes that cannot be instantiated directly and may contain abstract methods (methods without implementation). They serve as base classes for other classes to inherit and implement the abstract methods. They may or may not contain functions with implementations.

```go
abstract class Animal {
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
    func makeSound() {
        // Implementation required
    }
}
```

#### **Interfaces**

Interfaces define a contract of methods that implementing classes must provide.

```go
interface Drawable {
    func draw()
}
```

#### **Enumerations**

Enums are user-defined types representing a set of named constants.

```go
enum Color {
    RED,
    GREEN,
    BLUE
}
```

### **3.3 Default Values**

When a variable is declared but not explicitly initialized, it is assigned a default value based on its type:

| Type          | Default Value       |
|---------------|---------------------|
| `Bool`        | `false`             |
| `Char`        | `null`              |
| `SliceChar`   | `""` (empty string) |
| `Int`         | `0`                 |
| `Byte`        | `0`                 |
| `Short`       | `0`                 |
| `Long`        | `0L`                |
| `Float`       | `0.0F`              |
| `Double`      | `0.0D`              |
| Object/Class  | `null`              |
| Array         | `null`              |

#### Example

```go
var flag : Bool         // flag is false
var count : Int         // count is 0
var name : SliceChar    // name is ""
var user : UserProfile  // user is null
```

---

## **4. Language Usage**

### **4.1 Variables**

Variables in CSpeedy are declared using the `var` keyword, followed by the variable name and an optional type annotation. Initialization can be performed at the time of declaration.

#### **Declaration Syntax**

```go
var <variableName> : <Type?>
```

- `var` is the keyword for variable declaration
- `variableName` is the identifier for the variable (must be unique in context)
- `Type` is the data type of the variable (must be inferred)

#### Examples

```go
var age : Int
var name : SliceChar
var isActive : Bool
```

#### **Initialization**

Initialize a variable at declaration using the assignment operator `=`:

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

#### **Multiple Assignment**

CSpeedy supports multiple assignment, allowing you to assign values to several variables simultaneously:

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

#### **Type Inference**

CSpeedy supports type inference, allowing the compiler to automatically deduce the type of a variable from its initializer:

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

### **4.2 Constants and Static**

#### **Constants**

Constants are declared using the `const` keyword. A constant is read-only and its value cannot be changed after initialization.

```go
const PI : Double = 3.14159D
const greeting : SliceChar = "Hello"
```

#### **Static Variables and Methods**

The `static` keyword is used to declare variables or methods that belong to the class itself rather than to any instance. Static members can be accessed without creating an instance of the class.

```go
class MathUtils {
    static var counter : Int = 0

    static func increment() {
        counter = counter + 1
    }
}
```

#### **Combining `const` and `static`**

You can use both `const` and `static` together to declare class-level constants:

```go
class Config {
    static const MAX_USERS : Int = 100
}
```

### **4.3 Functions**

Functions are declared using the `func` keyword:

#### **Syntax**

```go
[internal] [visibility] [static] func functionName(param1 : Type1, param2 : Type2, ...) : (ReturnType) {
    // function body
}
```

- **[internal]:** Optional. Limits function access to the same program
- **[visibility]:** Optional. Can be `private`, `protected`, or `public` (defaults to `private`)
- **[static]:** Optional. Declares a class-level function
- **functionName:** Required. Must follow camelCase
- **Parameters:** Each parameter defined as `paramName : Type`, separated by commas
- **ReturnType:** Optional. Specify in parentheses after the colon. Use `void` or omit if no return value
- **Function Body:** Enclosed in curly braces `{}`

#### Examples

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

### **4.4 Expressions**

Expressions in CSpeedy are combinations of literals, variables, operators, and function calls that evaluate to a value.

#### Examples

```go
var sum = a + b * 2
var isAdult = age >= 18 && isActive
var message = "Hello, " + name
var result = calculateArea(width, height)
```

#### **String Interpolation**

SliceChar literals support string interpolation using `$variable` syntax:

```go
var greeting = "Hello, $userName!"
```

#### **String Mutability**

`SliceChar` is a mutable string type with a fixed initial size that can be changed dynamically. This means its contents can be modified (characters replaced, appended, or removed), but its mutability is limited by the current allocated size. Expanding or shrinking requires resizing the underlying storage.

#### **Function Calls**

Functions can be called within expressions:

```go
var area = getWidth() * getHeight()
```

#### **Conditional Expressions**

CSpeedy supports conditional (ternary-like) expressions:

```go
var status = isActive ? "Active" : "Inactive"
```

#### **Assignment Expressions**

Assignment is also an expression and can be chained:

```go
var x = y = z = 0
```

#### **Type Casting**

##### **Explicit Casting**
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

###### **Implicit Casting**
Implicit type casting occurs automatically when there is no loss of information and the conversion is safe. For example, converting from `Int<2>` to `Int<32>` preserves all data, or converting from `Int` to `Float` simply adds precision without losing values. In these cases, no additional code is required, and implicit casting is commonly used in function parameters and assignments.


### **4.5 Classes, Interfaces and Enums**

*[Content to be added]*

### **4.6 Statements**

*[Content to be added]*

#### **4.6.1 Control Flow Statements**

*[Content to be added]*

#### **4.6.2 Loop Statements**

*[Content to be added]*

#### **4.6.3 Exception Handling Statements**

*[Content to be added]*

### **4.7 Lists**

#### **4.7.1 Type of Lists**

*[Content to be added]*

#### **4.7.2 Lists Inheritance**

*[Content to be added]*

#### **4.7.3 Stream Operations**

Stream provides functional iteration over collections:

```go
func example() {
    var data : Number[] = null

    for (obj in data) {
        // Stream operations
    }
}
```

---

### **4.8 Using**

*[Content to be added]*

## **5. Memory Management**

*[Content to be added]*

### **5.1 Automatic Memory Management**

*[Content to be added]*

### **5.2 Manual Memory Management**

*[Content to be added]*

### **5.3 Garbage Collection**

*[Content to be added]*

---

## **6. Package System**

*[Content to be added]*

### **6.1 Package Declaration**

*[Content to be added]*

### **6.2 Import System**

*[Content to be added]*

### **6.3 Module Resolution**

*[Content to be added]*

---

## **7. Error Handling**

*[Content to be added]*

### **7.1 Exception Types**

*[Content to be added]*

### **7.2 Try-Catch-Finally**

*[Content to be added]*

### **7.3 Custom Exceptions**

*[Content to be added]*

---

## **8. Compilation Model**

*[Content to be added]*

### **8.1 Compilation Phases**

*[Content to be added]*

### **8.2 Code Generation**

*[Content to be added]*

### **8.3 Optimization**

*[Content to be added]*

---

## **9. Standard Library**

*[Content to be added]*

### **9.1 Core Types**

*[Content to be added]*

### **9.2 Collections**

*[Content to be added]*

### **9.3 I/O Operations**

*[Content to be added]*

### **9.4 Utility Functions**

*[Content to be added]*

---

## **10. Advanced Features**

*[Content to be added]*

### **10.1 Generics**

*[Content to be added]*

### **10.2 Reflection**

*[Content to be added]*

### **10.3 Annotations**

*[Content to be added]*

---

## **11. Performance Considerations**

*[Content to be added]*

### **11.1 Runtime Performance**

*[Content to be added]*

### **11.2 Memory Usage**

*[Content to be added]*

### **11.3 Optimization Guidelines**

*[Content to be added]*

---

## **12. Appendices**

### **Appendix A: Grammar Reference**

*[Content to be added]*

### **Appendix B: Keyword Index**

*[Content to be added]*

### **Appendix C: Examples and Use Cases**

*[Content to be added]*