# Control Structures

## Conditions

### If Expression
In Kotlin, `if` is an expression. Therefore, no ternary operator is required.

```kotlin
val number =
    if (…) {
        println("Assign the value 0 to number")
        0
    } else if (…) {
        println("Assign the value 1 to number")
        1
    } else {
        println("Assign the value 2 to number")
        2
    }
```

### When Expression
The `when` expression is similar to the `switch` statement in Java, but is much more flexible. The value of the first matching block is the value of the `when` expression. You can use arbitrary expressions (not only constants) as branch conditions.

```kotlin
val name = when (number) {
    in 1..10 -> {
        println("Assign the value \"Eugene\" to name")
        "Eugene"
    }
    11 -> {
        println("Assign the value \"Marie\" to name")
        "Marie"
    }
    else -> {
        println("Assign the value \"Dan\" to name")
        "Dan"
    }
}
```

If no argument is supplied, the branch conditions of a `when` expression are simply boolean expressions and the first branch whose condition is true is executed. This approach is a good alternative to an `if`-`else if` chain.

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
val countries: Array<String> = arrayOf("Germany", "China", "Egypt")
for (country in countries) {
    println(country)
}
```

### Break and Continue

Kotlin supports traditional `break` and `continue` operators in loops.
