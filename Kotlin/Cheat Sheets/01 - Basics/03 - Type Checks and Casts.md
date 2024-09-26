# Type Checks and Casts

## Explicit Casting

Explicit casting can be done in two different ways:
- **Unsafe cast operator `as`:** throws an exception if the cast isn't possible
- **Safe cast operator `as?`:** returns null if the cast isn't possible
```kotlin
val language: Any = "Kotlin"

val languageString = language as String // type: String
val languageNullableString = language as? String // type: String?
```

## Type Checks
Type checks can be done with the `is` operator.
```kotlin
if (language is String) {
    println((language as String).length)
}
```

## Smart Casts
If the type of a variable remains unchanged after a type check, the compiler can perform automatic casts to the checked type.
```kotlin
if (language is String) {
    println(language.length)
}
```
