# Basic Types

## Primitive Types

There are no direct primitive data types in Kotlin like in Java. Instead, **boxed primitive types**, which are represented as classes, are used. The bytecode uses primitives where possible, but they are not explicitly available.
```kotlin
// Integers
val b: Byte = 0
val s: Short = 13
val i: Int = 45
val l: Long = 56L

// Floating point numbers
val f: Float = 0.14F
val d: Double = 1.99

// Boolean
val bl: Boolean = true

// Character
val ch: Char = 'F'
```

## Unsigned Integer Types

Every integer type also has an unsigned version.
```kotlin
val ub: UByte = 0u
val us: UShort = 13u
val ui: UInt = 45u
val ul: ULong = 56uL
```

## Special Types

### Strings
```kotlin
val name: String = "Eugene"
```

### Unit
`Unit` corresponds roughly to `void` in Java, but is treated as a data type. `Unit` is implemented as a singleton object, which means the `Unit` class only has a single instance, the `Unit` object of the same name. It represents the absence of any meaningful value.
```kotlin
val u1: Unit = Unit
val u2: Unit = println()
```

### Any
`Any` is the root of the class hierarchy, which means that every class implicitly inherits from `Any` (equivalent to `Object` in Java).
```kotlin
val a1: Any = Any()
val a2: Any = "Hello World!"
```

### Nothing
`Nothing` has no instances. This type indicates that a function or expression will never return a value. For example, the following expressions are of type `Nothing`:
```kotlin
// For demonstration purposes only (you would never write it like that)
val n1: Nothing = throw Exception()
val n2: Nothing = return
```
`Nothing` is the so-called **bottom type**, which means that it implicitly inherits from all other types. This makes it possible to use `Nothing` at any point in the code where any other type is expected.
```kotlin
// For demonstration purposes only (you would never write it like that)
val n1: Int = throw Exception()
val n2: String = return
```
In practice, this allows us to write such expressions that would not be valid in other languages without a bottom type:
```kotlin
val username: String = if (user != null) user.name else throw Exception()
```
Another use case is to specify `Nothing` as the return type of a function so that it can be used in a context where any other type is expected.
```kotlin
fun notImplemented(): Nothing {
    throw Exception()
}

fun add(a: Int, b: Int): Int {
    notImplemented()
}
```

## Nullable Types
All types in Kotlin are non-null by default (null safety). To get the nullable type, you have to add a question mark at the end.
```kotlin
val nullableInt: Int? = null
val nullableString: String? = null
```
