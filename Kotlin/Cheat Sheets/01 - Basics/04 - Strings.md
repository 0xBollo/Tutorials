# Strings

## String Literals

Kotlin has two types of string literals.
- **Escaped Strings:** can contain escape characters
- **Multiline Strings:** can contain newlines and any other characters
```kotlin
// Escaped string
val text = "Hello World\n"

// Multiline string
val table = """
    id  first_name  last_name
    1   Ramona      Freitag
    2   Wolfgang    Schmidt
    3   Daniel      Holmes
""".trimIndent() // to remove indentation
```

## String Templates

A template expression starts with a dollar sign and consists of either a name or an expression in curly braces.
```kotlin
val name = "Eugene"
val age = 15

println("$name will be of age in ${18 - age} years.")
```
