# Variables and Constants

## Variables

Variables are declared with the `var` keyword.
```kotlin
var number = 11
```

## Constants

Constants are declared with the `val` keyword.
```kotlin
val pi = 3.14
```

## Compile-Time Constants

Compile-time constants are declared with the `const val` keywords and must be initialized with a static value. They can only be defined at top level or within object declarations.
```kotlin
// At top level
const val APP_NAME = "Hello World!"

// Within a singleton object
object MySingleton {
    const val OBJECT_NAME = "MySingleton"
}

// Within a companion object
class MyClass {
    companion object {
        const val CLASS_NAME = "MyClass"
    }
}
```

## Type Annotations

Kotlin is **statically typed**. The type of a variable can be specified explicitly.
```kotlin
val greeting: String = "Hello World!"
```

In most cases, the compiler can derive the type by **type inference**, so the type annotation can be omitted.
```kotlin
val greeting = "Hello World!" // inferred type: String
```

If you want to declare a variable without initializing it, you must specify the type.
```kotlin
var greeting: String
```
