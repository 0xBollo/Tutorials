# Operator Overloading

Operators in Kotlin are special functions that have predefined symbolic representation (like `+`, `-`, `*`, …) and precedence.

Kotlin allows you to provide custom implementations for the predefined set of operators on types. To implement an operator function, you provide a **member function** or an **extension function** with the `operator` keyword and a specific name for the corresponding type. This type becomes the left-hand side type for binary operations and the argument type for the unary ones.

## Overview of Operators

Some operator functions require specific parameter types and/or return types.

### Arithmetic Operators

| Symbol   | Meaning                       | Operator Function  | Parameter Type      | Return Type        |
|----------|-------------------------------|--------------------|---------------------|--------------------|
| `+`      | Addition                      | `plus()`           | Any type            | Any type           |
| `-`      | Subtraction                   | `minus()`          | Any type            | Any type           |
| `*`      | Multiplication                | `times()`          | Any type            | Any type           |
| `/`      | Division                      | `div()`            | Any type            | Any type           |
| `%`      | Modulo                        | `rem()`            | Any type            | Any type           |

Code example for overloading the `+` operator with different types for the second operand:

```kotlin
class MyIntWrapper(val value: Int) {
    // Allows expressions like: MyIntWrapper(7) + MyIntWrapper(3)
    operator fun plus(other: MyIntWrapper): MyIntWrapper {
        return MyIntWrapper(this.value + other.value)
    }

    // Allows expressions like: MyIntWrapper(7) + 3
    operator fun plus(other: Int): MyIntWrapper {
        return MyIntWrapper(this.value + other)
    }
}
```

### Assignment Operators

_Note: Since you cannot implement the assignment of an instance to a variable yourself (you can only access the current instance using `this` but not the variable(s) referencing it), you can only implement the assignment operators in a way that changes the state of the current instance without assigning a new value to the variable referencing this instance._

The assignment operator `=` cannot be overloaded in Kotlin. This is a conscious design decision to keep the semantics of the assignment clear and unambiguous. An assignment should only be used to assign a new value to a variable, not to mutate the object.\
The compound assignment operators can be overloaded to do performance optimizations.

| Symbol   | Meaning                       | Operator Function  | Parameter Type      | Return Type        |
|----------|-------------------------------|--------------------|---------------------|--------------------|
| `=`      | Assignment                    | -                  | -                   | -                  | 
| `+=`     | Addition and assignment       | `plusAssign()`     | Any type            | `Unit`             |
| `-=`     | Subtraction and assignment    | `minusAssign()`    | Any type            | `Unit`             |
| `*=`     | Multiplication and assignment | `timesAssign()`    | Any type            | `Unit`             |
| `/=`     | Division and assigment        | `divAssign()`      | Any type            | `Unit`             |
| `%=`     | Modulo and assignment         | `remAssign()`      | Any type            | `Unit`             |

_Note: In Kotlin, assignments are not expressions._

If you implement one of the arithmetic operators for a type (and the operator function returns a subtype of it), Kotlin also supports the corresponding compound assignment, which performs the arithmetic operation and reassigns the result to the corresponding variable.

```kotlin
class MyIntWrapper(val value: Int) {
    operator fun plus(other: MyIntWrapper): MyIntWrapper {
        return MyIntWrapper(this.value + other.value)
    }

    operator fun plus(other: Int): Int {
        return this.value + other
    }
}

fun main() {
    var myIntWrapper = MyIntWrapper(9)

    // Works because the overloaded plus operator with a MyIntWrapper parameter 
    // also returns a MyIntWrapper that can be assigned.
    myIntWrapper += MyIntWrapper(3)

    // Does not work because the overloaded plus operator with an Int parameter
    // returns an Int, which is not a subtype of MyIntWrapper.
    myIntWrapper += 7 // Compilation error: Type mismatch
}
```

However, sometimes an actual reassignment is unnecessary, e.g. if you want to use the `+=` operator to add an element to a list. In such cases, you can implement the `plusAssign()` operator function.

```kotlin
class MyList<T>  {
    private val items = mutableListOf<T>()

    operator fun plus(item: T): MyList<T> {
        val newList = MyList<T>()
        newList.items.addAll(this.items)
        newList.items.add(item)
        return newList
    }

    operator fun plusAssign(item: T) {
        items.add(item)
    }
}

fun main() {
    val myList = MyList<Int>()
    myList += 8
    myList += 9
}
```

By default, the `+=` operator would create a new list with the new item and reassign it to the operand on the left. The implementation of the `plusAssign()` function avoids this unnecessary reassignment and simply adds the item to the existing list.

### Increment and Decrement Operators

The operator functions `inc()` and `dec()` should return a new instance without mutating the current instance. You do not have to (and cannot) worry about reassigning the new value to the variable, the compiler takes care of that.

| Symbol   | Meaning                       | Operator Function  | Return Type             |
|----------|-------------------------------|--------------------|-------------------------|
| `++`     | Increment                     | `inc()`            | Subtype of the receiver |
| `--`     | Decrement                     | `dec()`            | Subtype of the receiver |

Practical example:

```kotlin
class Counter(var value: Int) {
    operator fun inc(): Counter {
        return Counter(value + 1)
    }
}

fun main() {
    var counter = Counter(5)

    counter++
    println(counter.value) // output: 6
}
```

### Comparison Operators

| Symbol   | Meaning                       | Operator Function  | Parameter Type      | Return Type        |
|----------|-------------------------------|--------------------|---------------------|--------------------|
| `==`     | Structural equality           | `equals()`         | `Any?`              | `Boolean`          |
| `!=`     | Structural inequality         | `equals()`         | `Any?`              | `Boolean`          |
| `===`    | Referential equality          | -                  | -                   | -                  |
| `!==`    | Referenctial inequality       | -                  | -                   | -                  |
| `<`      | Less than                     | `compareTo()`      | Any type            | `Int`              |
| `>`      | Greater than                  | `compareTo()`      | Any type            | `Int`              |
| `<=`     | Less or equal                 | `compareTo()`      | Any type            | `Int`              |
| `>=`     | Greater or equal              | `compareTo()`      | Any type            | `Int`              |

### Logical Operators

The `!` operator is the only logical operator that can be overloaded.

| Symbol   | Meaning                       | Operator Function  | Return Type        |
|----------|-------------------------------|--------------------|--------------------|
| `!`      | Logical negation              | `not()`            | Any type           |
| `&&`     | Logical and                   | -                  | -                  |
| `\|\|`   | Logical or                    | -                  | -                  |

Practical example:

```kotlin
class Light(var isOn: Boolean) {
    operator fun not(): Light {
        return Light(!isOn)
    }
}
```

### Indexed Access Operator

The indexed access operator is used to access elements by index.

The operator function `get()` can be overloaded with at least one to any number of parameters for the indices.

The operator function `set()` can be overloaded with at least one to any number of parameters for the indices and the parameter for the value to be assigned (which must be the last one).

| Symbol              | Meaning                | Operator Function  | Parameter Types   | Return Type      |
|---------------------|------------------------|--------------------|-------------------|------------------|
| `[i_1, …, i_n]`     | Access to index        | `get()`            | Any types         | Any type         |
| `[i_1, …, i_n]=`    | Assignment to index    | `set()`            | Any types         | Any type         |

Practical example:

```kotlin
class Matrix<T>(private val items: MutableList<MutableList<T>>) {
    operator fun get(i: Int, j: Int) = items[i][j]

    operator fun set(i: Int, j: Int, value: T) {
        items[i][j] = value
    }
}

fun main() {
    val matrix = Matrix(
        mutableListOf(
            mutableListOf(1, 2, 3),
            mutableListOf(3, 4, 5)
        )
    )

    println(matrix[0, 2]) // output: 3
    matrix[0, 2] = 17
    println(matrix[0, 2]) // output: 17
}
```

### Range Operators

| Symbol   | Meaning                       | Operator Function  | Parameter Type      | Return Type        |
|----------|-------------------------------|--------------------|---------------------|--------------------|
| `..`     | Create Range                  | `rangeTo()`        | Any type            | Any type           |
| `in`     | Value is in range             | `contains()`       | Any type            | `Boolean`          |
| `!in`    | Value is not in range         | `contains()`       | Any type            | `Boolean`          |

### Destructuring Operators

The destructuring operator can be used to split objects into several variables by extracting components.

| Symbol              | Meaning                  | Operator Function                 | Return Type  |
|---------------------|--------------------------|-----------------------------------|--------------|
| `(var_1, …, var_n)` | Destructuring Components | `component1()`, …, `componentN()` | Any type     |

```kotlin
class Book(val title: String, val author: String) {
    operator fun component1() = title
    operator fun component2() = author
}

val book = Book("1984", "George Orwell")
val (title, author) = book
```

Typical examples from the standard library are the classes `Pair`, `Triple` and `Map.Entry`, which implement the desctructuring operator.

### Invoke Operator

The invoke operator is used to call objects as if they were functions.

| Symbol              | Meaning       | Operator Function  | Parameter Types     | Return Type        |
|---------------------|---------------|--------------------|---------------------|--------------------|
| `(arg_1, …, arg_n)` | Invoke object | `invoke()`         | Any types           | Any type           |

There are **two main use cases** for the invoke operator:
- Call instances of function types as if they were normal functions
- Design objects like configurable functions that maintain state or have specific initialization requirements

#### Function Types
In Kotlin, lambdas and callable references under the hood are anonymous objects of type `Function0`, `Function1`, …, `FunctionN` (depending on the number of parameters) that implement the invoke operator. This allows them to be called like normal functions, although they are actually objects.

For example, this:
```kotlin
val add = { a: Int, b: Int -> a + b }
```
is essentially the same as here:
```kotlin
val add = object : Function2<Int, Int, Int> {
    override fun invoke(a: Int, b: Int): Int {
        return a + b
    }
}
```

Thanks to the invoke operator, the function object can be called directly to execute the lambda function.
```kotlin
val result = add(3, 4)
```

For comparison: In Java you have to call the method of the functional interface to execute the lambda function.
```java
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
int result = add.apply(3, 4);
```

## Declaring and Overriding Operator Functions

### Abstract Operator Functions
Interfaces and abstract classes can declare abstract operator functions, forcing their implementations to overload certain operators with certain parameter types and return types. Here are some examples from the standard library:

```kotlin
interface Comparable<in T> {
    operator fun compareTo(other: T): Int
}

interface Collection<out E> : Iterable<E> {
    operator fun contains(element: E): Boolean
}

interface List<out E> : Collection<E> {
    operator fun get(index: Int): E
    operator fun set(index: Int, element: E): E
}
```

### Overriding Operator Functions
Operator functions can be overridden in subclasses or interface implementations. In such cases, the `operator` keyword does not need to be specified again. In this way, for example, you can override the operator function `equals()` from the class `Any`.

```kotlin
class Person(val id: Long, val name: String) {
    override fun equals(other: Any?): Boolean {
        return other is Person && this.id == other.id
    }
}
```

## References

Kotlin Programming Language (2024) 'Operator overloading', available at: https://kotlinlang.org/docs/operator-overloading.html.

Dehghani, A. (2024) 'Operator Overloading in Kotlin', Baeldung On Kotlin, available at: https://www.baeldung.com/kotlin/operator-overloading

Duggu (2023) 'Mastery on Invoke Kotlin', Medium, available at: https://medium.com/@dugguRK/mastery-on-invoke-kotlin-8f1ebb4828d0.

Barbini, U. (2019) '[Kotlin Pearls 4] It’s an Object… It’s a Function… It’s an Invokable', Medium, available at: https://proandroiddev.com/kotlin-pearls-3-its-an-object-it-s-a-function-it-s-an-invokable-bc4bfed2e63f.
