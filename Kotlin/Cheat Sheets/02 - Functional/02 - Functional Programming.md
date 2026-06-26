# Functional Programming

Kotlin functions are first-class, which means they can be stored in variables and can be passed as arguments to and returned from other higher-order functions. You can perform any operations on functions that are possible for other non-function values.

## Function Types

Kotlin uses a family of function types to represent functions. These types have a special notation that corresponds to the parameter and return types of the functions.
- All function types have a **parenthesized list of parameter types and a return type**. `(A, B) -> C` denotes a type that represents functions with two parameters of types `A` and `B` and a return value of type `C`.
- Function types can optionally have an additional **receiver type**, which is specified before the dot in the notation. The type `A.(B) -> C` represents functions that can be called on a receiver object of type `A` with a parameter of type `B` and return a value of type `C`. A function type with a receiver type basically represents an extension function for this receiver type.

```kotlin
// Function that takes two Int arguments and returns an Int
val add: (Int, Int) -> Int = …

// Function that takes no arguments and returns Unit
val printHello: () -> Unit = …

// Function that is called on a String without arguments and returns Unit
val printUppercase: String.() -> Unit = …
```

The function type notation can optionally include names for the function parameters.
```kotlin
val greet: (name: String) -> Unit = …
```

## Function Types under the Hood

The Java bytecode does not have a first-class function type. All it has are primitives (characters, integers, …) and references (to objects). Those are the only values you can store in variables, pass as function arguments and return from functions. So the Kotlin compiler has to convert first-class functions into something the JVM can handle.

### FunctionN Interfaces

Therefore, Kotlin's runtime library defines a series of generic interfaces `Function0`, `Function1`, `Function2`, …, where the number corresponds to the number of parameters. All these interfaces declare the `invoke()` operator function with the corresponding number of parameters. For example, you can imagine the `Function2` interface as follows: 

```kotlin
interface Function2<in P1, in P2, out R> {
    operator fun invoke(p1: P1, p2: P2): R
}
```

Function types like `(A, B) -> C` are mapped to the corresponding function interfaces like `Function2<A, B, C>` for the bytecode. Anonymous functions, lambda expressions and callable references are, under the hood, anonymous objects of these function interfaces that implement the invoke operator.

For example, this:
```kotlin
val add: (Int, Int) -> Int = { a, b -> a + b }
```
is essentially the same as here:
```kotlin
val add = object : Function2<Int, Int, Int> {
    override fun invoke(a: Int, b: Int): Int {
        return a + b
    }
}
```
_Note: Starting from Kotlin 2.0, a JVM mechanism called `invokedynamic` is used to implement lambdas more efficiently without creating anonymous classes. Learn more about it [here](https://www.ej-technologies.com/blog/2024/01/how-invokedynamic-makes-lambdas-fast/) and [here](https://youtrack.jetbrains.com/issue/KT-45375)._

### Function Types with Receiver Type

When calling functions on a receiver object, the receiver object is passed as the first argument to the `invoke()` operator function. At bytecode level, types such as `A.(B) -> C` and `(A, B) -> C` do not differ. Both are mapped to the interface `Function2<A, B, C>`. They only differ in the way they are called with the invoke operator symbol in the source code.

### Comparison with Java

The Java equivalents to the `FunctionN` interfaces in Kotlin are the functional interfaces, such as `Function`, `Supplier`, `Consumer`, `Predicate` and so on.

## Instantiating Function Types

There are several ways to instantiate function types:
- Use a **function literal**
    - Lambda expressions
    - Anonymous functions
- Use a **callable reference** to an existing declaration
- Provide a **custom implementation** of a function type

### Lambda Expressions

Lambda expressions generally have the following syntax: `{ Parameters -> Body }`
- The **parameters** are separated by commas and may have type annotations.
- **`->`** seperates parameters from the body.
- The **body** can contain several statements and expressions. If the expected return type of the lambda is not `Unit`, the last expression is treated as the return value.

```kotlin
val add: (Int, Int) -> Int = { x: Int, y: Int -> x + y }
```

#### Type Annotations
If the function type of a lambda cannot be inferred from the context, the type annotations of the parameters are mandatory.
```kotlin
// Parameter types can be inferred from the explicit function type of add
val add: (Int, Int) -> Int = { a, b -> a + b }

// Type of the number parameter can be inferred from the expected function
// type of the parameter of the forEach function
val numbers = intArrayOf(1, 2, 3)
numbers.forEach { number -> println(number) }

// Parameter types cannot be inferred because the type of add is not explicitly
// specified
val add = { a: Int, b: Int -> a + b }
```

#### Implicit Name of a Single Parameter
If a lamda expression has a single parameter, it does not have to be declared explicitly. The parameter will be implicitly declared under the name `it`.
```kotlin
val isEven: (Int) -> Boolean = { it % 2 == 0 }
```

#### Returning a Value
You can explicitly return a value from the lambda using a qualified return. Otherwise, the value of the last expression is implicitly returned. Therefore, the two following snippets are equivalent:
- non local return
- local return / qualified return
- implicit return
```kotlin
numbers.filter {
    val shouldFilter = it > 0
    shouldFilter
}

numbers.filter {
    val shouldFilter = it > 0
    return@filter shouldFilter
}
```

#### Trailing Lambdas
If the last parameter of a function is a function type, then a lambda expression passed as the corresponding argument can be placed outside the parentheses:
```kotlin
val product = items.fold(1) { acc, e -> acc * e }
```
If the lambda is the only argument in that call, the parentheses can be omitted entirely:
```kotlin
items.forEach { item -> println(item) }
```

### Anonymous Functions
`fun (Parameters): ReturnType { Body }`

An anonymous function looks like a regular function declaration, except its name is omitted. In contrast to a lambda expression, the return type can be specified explicitly here.
```kotlin
val add: (Int, Int) -> Int = fun (a: Int, b: Int): Int = a + b
```

#### Type Annotations
If the function type of an anonymous function can be inferred from the context, the type annotations can be omitted.
```kotlin
// Parameter types cannot be inferred because the type of add is not explicitly
// specified
val add1 = fun (a: Int, b: Int): Int = a + b
// Notice that the return type can still be inferred and does not have to be 
// specified explicitly
val add2 = fun (a: Int, b: Int) = a + b

// Parameter types can be inferred from the explicit function type of add
val add3: (Int, Int) -> Int = fun (a, b) = a + b
```

## Interchangeability of Function Types with and without Receiver Type

Non-literal values of function types with and without a receiver are interchangeable (see: [Function types with receiver type under the hood](#function-types-with-receiver-type)), so the receiver can stand in for the first parameter, and vice versa.

```kotlin
val add1: (Int, Int) -> Int = { a, b -> a + b }
val add2: Int.(Int) -> Int = add1
```

Literals, on the other hand, must match the expected parameter scheme exactly.

```kotlin
// Error: Expected one parameter of type Int
val add2: Int.(Int) -> Int = { a, b -> a + b } // { a -> this + a } would be correct
```

## Invoking Function Type Instances

## References

Kotlin Programming Language (2024) 'Higher-order functions and lambdas', available at: https://kotlinlang.org/docs/lambdas.html.

Kotlin Discussions (2022) 'Function Type is an Interface', available at: https://discuss.kotlinlang.org/t/function-type-is-an-interface/24902.