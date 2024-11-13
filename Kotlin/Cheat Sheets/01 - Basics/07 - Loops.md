# Loops

## While Loop
Kotlin provides the traditional `while` loop.

```kotlin
var i = 0
while (i < 3) {
    println(i)
    i++
}
```

## Do-While Loop
There is also the traditional `do-while` loop.

```kotlin
var i = 0
do {
    println(i)
    i++
} while (i < 6)
```

## For Loop
In Kotlin there is no traditional for loop, but a foreach loop. The `for` loop can iterate over all types that provide an implementation of the **operator function** `iterator()`.

```kotlin
val countries = arrayOf<String>("Germany", "China", "Egypt")
for (country in countries) {
    println(country)
}
```

## Break and Continue

Kotlin supports traditional `break` and `continue` keywords in loops.
