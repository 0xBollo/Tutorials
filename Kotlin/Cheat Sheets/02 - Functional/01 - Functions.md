# Functions

## Function Declaration and Usage

Functions are declared using the `fun` keyword:
```kotlin
fun greet() {
    println("Hello World!")
}
```

Functions are called using the standard approach:
```kotlin
greet()
```

Member functions are called with the dot notation:
```kotlin
obj.toString()
```

## Parameters

Parameters are separated by commas and must be explicitly typed.
```kotlin
fun greet(greeting: String, name: String) {
    println("$greeting $name!")
}
```

## Default Arguments

Function parameters can have default values, which are used when you skip the corresponding argument. This reduces the number of overloads.
```kotlin
fun greet(name: String, greeting: String = "Hello") {
    println("$greeting $name!")
}

fun main() {
    greet("Alice")
    greet("Bob", "Good morning")
}
```

Overriding methods must not specify default values for its parameters, as this would break the contract. Overriding methods always use the base method's default parameter values.
```kotlin
interface Cat {
    // The contract specifies that makeNoise() is the same as makeNoise(“meow”)
    fun makeNoise(noise: String = "meow")
}

class BengalCat : Cat {
    override fun makeNoise(noise: String) {   // Default value is not allowed
        println("Bengal cat makes $noise")
    }

    // This is not allowed because makeNoise() now corresponds to
    // makeNoise(“woof”) and not to makeNoise(“meow”) as specified in the
    // contract.
//    override fun makeNoise(noise: String = "woof") {
//        println("Bengal cat makes $noise)
//    }
}
```

## Named Arguments

You can name one or more of a function's arguments when calling it. This can be helpful when a function has many arguments and it's difficult to associate a value with an argument, especially if it's a boolean or `null` value.
```kotlin
fun reformat(
    str: String,
    normalizeCase: Boolean = true,
    upperCaseFirstLetter: Boolean = true,
    divideByCamelHumps: Boolean = false,
    wordSeparator: Char = ' ',
) { /*...*/ }
```

Named arguments can be passed in any order. Named and positioned arguments can also be mixed, but as soon as a named argument is not listed in its original position, all subsequent arguments must also be named.
```kotlin
// Allowed because the normalizeCase argument is in its original position
reformat(
    "hello world",
    normalizeCase = false, // named argument in original position
    false,
    true,
)

// Allowed, as all arguments after upperCaseFirstLetter are also named
reformat(
    "hello world",
    upperCaseFirstLetter = false, // named argument in different position
    divideByCamelHumps =  true,
    wordSeparator = '_',
)

// Not allowed because upperCaseFirstLetter is not in its original position
// and the arguments after it are not named
// reformat(
//     "hello world",
//     upperCaseFirstLetter = false,
//     true,
//     '_',
// )
```

## Variable Number of Arguments

You can pass a variable number of arguments to a function via the `vararg` parameter.
```kotlin
fun printAllStrings(vararg strings: String) {
    for (s in strings) {
        println(s)
    }
}
```
To pass an array containing a variable number of arguments to a function, use the **spread** operator `*`. The spread operator passes each element of the array as individual argument to the function.
```kotlin
val names = arrayOf("Dan", "Jane", "Carlo")
printAllStrings(*names)
```

## Single Expression Functions

When the function body consists of a single expression, the curly braces can be omitted and the body specified after an `=` symbol.
```kotlin
fun double(x: Int): Int = x * 2
```

Explicitly declaring the return type is optional when this can be inferred by the compiler.
```kotlin
fun double(x: Int) = x * 2
```

## Explicit Return Types

Functions with block body must always specify the return type explicitly, unless the return type is `Unit`.

## Infix Functions

Functions marked with the `infix` keyword can also be called using the **infix notation** (omitting the dot and the parentheses for the call). Infix functions must meet the following requirements:
- They must be member functions or extension functions.
- They must have a single parameter.
- The parameter must not accept variable number of arguments and must have no default value.

```kotlin
infix fun Int.add(x: Int) = this + x

fun main() {
    println(4 add 1) // call function with infix notation
}
```

## Function Scope

In contrast to Java, where there are only methods at class level, functions in Kotlin have different scopes.
- **Top level functions**
    - Declared at the top level in a file
    - Depending on visibility, can be called within the file, within the module or from anywhere
    - Can access top level elements
- **Local functions**
    - Functions inside other functions
    - Can only be called within the surrounding function
    - Can access top level elements and local variables of outer functions (the closure)
- **Member functions**
    - Functions that are defined inside a class or object
    - Can only be called on instances of the class or the object
    - Can access top level elements and class members

## References

Kotlin Programming Language (2024) 'Functions', available at: https://kotlinlang.org/docs/functions.html.
