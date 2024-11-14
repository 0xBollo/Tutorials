# Exceptions

Kotlin treats all exceptions as unchecked, regardless of whether they inherit from `RuntimeException` or directly from `Exception`.

## Throw Exceptions
You can manually throw exceptions with the `throw` keyword.
```kotlin
throw Exception()
```

The constructors of the built-in exception classes are overloaded so you can optionally pass a message, the cause or both.
```kotlin
// With message
throw Exception("An error has occurred")

// With cause
val cause = Exception("An error has occurred")
throw Exception(cause)

// With message and cause
throw Exception("A subsequent error has occurred", cause)
```

### Precondition Functions

Kotlin offers various functions that check preconditions and automatically throw specific exceptions if they are not met.

#### `require()`
- Typically used to **validate function arguments**
- Throws an `IllegalArgumentException` if the first argument evaluates to `false`
- Optionally accepts a function object as second argument that returns the error message. The message is only calculated if the precondition is not met (to avoid unnecessary calculations).
```kotlin
fun divide(a: Double, b: Double): Double {
    require(b != 0.0) { "Division by zero is not defined" }
    return a / b
}
```

#### `requireNotNull()`
- Typically used to **ensure that a function argument or a value derived from a function argument is not null**
- Throws an `IllegalArgumentException` if the first argument is `null`
- Optionally accepts a function object as second argument that returns the error message
```kotlin
fun printUsername(user: User) {
    requireNotNull(user.username) { "Username must not be null" }
    println(user.username)
}
```

#### `check()`
- Typically used to **validate the internal object state or external variables**
- Throws an `IllegalStateException` if the first argument evaluates to `false`
- Optionally accepts a function object as second argument that returns the error message
```kotlin
val username: String = ""

fun printUsername() {
    check(username.isNotBlank()) { "Username must not be blank" }
    println(username)
}
```

#### `checkNotNull()`
- Typically used to **ensure that a value of the internal object state or an external variable is not null**
```kotlin
val username: String? = null

fun printUsername() {
    checkNotNull(username) { "Username must not be null" }
    println(username)
}
```

## Try Expression

In Kotlin, `try` is an expression. The last executed expression in the `try` or `catch` block becomes the value of the `try` expression. The `finally` block does not affect the value of the `try` expression.
```kotlin
val numberString = "13#"

 val number =
    try {
        numberString.toInt()
    } catch (e: NumberFormatException) {
        -1
    } finally {
        println("Finished")
    }
```

## References

Kotlin Programming Language (2024) 'Exceptions', available at: https://kotlinlang.org/docs/exceptions.html
