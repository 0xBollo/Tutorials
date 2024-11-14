# Conditions

## If Expression
In Kotlin, `if` is an expression. The value of the selected branch becomes the value of the `if` expression.
A branch can be a single expression or a block. If it is a block, the last expression within the block is the value of the branch.
```kotlin
// Branches are single expressions
val number = if (true) 77 else 99

// Branches are blocks
val name =
    if (false) {
        println("Set name to \"Eugene\"")
        "Eugene"
    } else if (true) {
        println("Set name to \"Marie\"")
        "Marie"
    } else {
        println("Set name to \"Dan\"")
        "Dan"
    }
```

## When Expression
The `when` expression is similar to the `switch` statement in Java, but is much more flexible. 
The value of the first matching branch becomes the value of the `when` expression. A branch can
be a single expression or a block. If it is a block, the last expression within the block is the
value of the branch. The `when` expression can be used with or without a subject.

### With Subject
If a subject is supplied, all branch conditions are evaluated in relation to it. You can use arbitrary expressions (not only constants) as branch conditions.

```kotlin
val name = when (number) {
    in 1..10 -> {
        println("Set name to \"Eugene\"")
        "Eugene"
    }
    11 -> {
        println("Set name to \"Marie\"")
        "Marie"
    }
    else -> {
        println("Set name to \"Dan\"")
        "Dan"
    }
}
```
You can capture the subject in a variable. The scope of this variable is restricted to the body of the `when` expression.
```kotlin
fun Request.getBody() =
    when (val response = executeRequest()) {
        is Success -> response.body
        is HttpError -> throw HttpException(response.status)
    }
```

### Without Subject
If no subject is supplied, the branch conditions are simply boolean expressions. This approach is a good alternative to an `if`-`else if` chain.

```kotlin
when {
    0 == 0 -> println("This will be printed")
    1 == 1 -> println("This will not be printed")
}
```
