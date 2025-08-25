# COMPILER_SPEC.md
# Specs of CSpeedy Compiler **CSAOT**

## 1. Executive Summary
**CSAOT** is an experimental compiler for the Language **CSpeedy**.
His goal is aim to compile any program write on CSpeedy to be executable.

This compiler aims to be a **Functional MVP** with support for:
- Constants and Variables with basic types
- Logic flow: `if`, `else`, `do`, `while`, `for`, `stream`, `switch-case`
- Error handling: `try`, `except`, `catch`, `finally`, `throw`
- POO: Object oriented language with the 3 pilars:
- - Inheritance: 
- - Abstraction: Using `interfaces` and `enum` 
- - Encapsulation: 
        Lowest access modificator `private` for only the file container. 
        Mid access modificator `protected` for childs. 
        Highest access modificator `public` granting access for everyone.
        Optional access modificator `pkg` that gives access only to this current program being compilled. So even `public` modifier won't grant access if it is being accesses outside the compiled program.
- Functions and calls

## 2. Memory Management 
Like languages such as `Go` or `C++`, `CSpeedy` allows developers to manage memory and work with pointers across functions. However, if you don't need fine-grained control over data, `CSpeedy` handles memory management automatically.

When a `pointer` is no longer used within the method where it was created or passed as a parameter, `CSpeedy` automatically removes it. Variables that are not used as `pointers` or parameters are automatically freed once the function finishes executing.

### Benefits
- **Safety**: Automatic cleanup reduces memory leaks.
- **Flexibility**: Developers can still use pointers when needed.
- **Simplicity**: No need for manual memory management in common cases.

### Example using CSpeedy
```go
func processData(dataPointer* : any) {
    var data : Number = 1

    endsProcessingData(dataPointer)
    // `data` will be automatically freed here as the function ends
    // `dataPointer` is still valid inside `endsProcessingData`
    // In CSpeedy, memory cleanup is sequential, so this ensures safety and predictability
}

func endsProcessingData(dataPointer* : any) {
    // `dataPointer` can still be used here
    // No action needed; CSpeedy handles memory automatically
}
```

## 3. Reach
### MVP:
- Lexer: Tokenization of the Source Code, translating `reserved words` into instructions, as `IF, WHILE, RETURN`. As well as it detects lexical errors.
- Parser: Generates nodes in order to construct the language, simplifying the semantic analisis and translating code into bytes using AOT.
- Simplest semantic analisis: Checks for wrongly formed nodes.
