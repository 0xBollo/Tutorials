# Control Structures

## Conditions

### If Expression
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

### When Expression
The `when` expression is similar to the `switch` statement in Java, but is much more flexible. 
The value of the first matching branch becomes the value of the `when` expression. A branch can
be a single expression or a block. If it is a block, the last expression within the block is the
value of the branch. The `when` expression can be used with or without a subject.

#### With Subject
If an argument is supplied, `when` matches it against the branches. You can use arbitrary expressions (not only constants) as branch conditions.

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

#### Without Subject
If no argument is supplied, the branch conditions of a `when` expression are simply boolean expressions. This approach is a good alternative to an `if`-`else if` chain.

```kotlin
when {
    0 == 0 -> println("This will be printed")
    1 == 1 -> println("This will not be printed")
}
```

## Loops

### While Loop
Kotlin provides the traditional `while` loop.

```kotlin
var i = 0
while (i < 3) {
    println(i)
    i++
}
```

### Do-While Loop
There is also the traditional `do-while` loop.

```kotlin
var i = 0
do {
    println(i)
    i++
} while (i < 6)
```

### For Loop
In Kotlin there is no traditional for loop, but a foreach loop. The `for` loop can iterate over all types that provide an implementation of the **operator function** `iterator()`.

```kotlin
val countries = arrayOf<String>("Germany", "China", "Egypt")
for (country in countries) {
    println(country)
}
```

### Break and Continue

Kotlin supports traditional `break` and `continue` keywords in loops.
