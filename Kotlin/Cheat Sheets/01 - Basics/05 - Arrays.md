# Arrays

## Types Of Arrays

### Object Arrays / Typed Arrays
Object arrays **can store all data types**, including primitive types (but the JVM will use their wrapper classes). They are represented by the `Array` class.

### Primitive-Type Arrays
Primitive-type arrays **can only store primitive data types** and the JVM will use the actual primitive types, so there is no boxing overhead. They are represented by the following classes:
- `ByteArray`
- `ShortArray`
- `IntArray`
- `LongArray`
- `FloatArray`
- `DoubleArray`
- `BooleanArray`
- `CharArray`

There are also primitive-type arrays for the **unsigned integer types**, as these are stored on the JVM as the corresponding signed integer types.
- `UByteArray`
- `UShortArray`
- `UIntArray`
- `ULongArray`

All these classes have no inheritance relation to the `Array` class, but they have the same set of functions and properties.

## Create Arrays

To create arrays, you can use different **functions**.
```kotlin
// Create some object arrays
val countries: Array<String> = arrayOf("Germany", "China", "Egypt") // ["Germany", "China", "Egypt"]
val nulls: Array<Int?> = arrayOfNulls(3) // [null, null, null]
val empty: Array<Any> = emptyArray() // []

// Create some primitive-type arrays
val primes: IntArray = intArrayOf(2, 3, 5, 7, 11, 13) // [2, 3, 5, 7, 11, 13]
val prices: DoubleArray = doubleArrayOf(1.99, 2.59, 0.59) // [1.99, 2.59, 0.59]
val booleans: BooleanArray = booleanArrayOf(true, false, true) // [true, false, true]
```
Alternatively you can use the `Array` **constructor** or the constructor of the corresponding primitive-type array class. It takes the array size and a function that returns values for array elements given its index.
```kotlin
// Create an object array with the Array constructor
val evenNumbers = Array<Int>(5) { i -> i * 2 } // [0, 2, 4, 6, 8]

// Create a primitive-type array with the IntArray constructor
val oddNumbers: IntArray = IntArray(5) { i -> i * 2 + 1 } // [1, 3, 5, 7, 9]
```

## Nested Arrays

There are no real multidimensional arrays in Kotlin (just like in Java), as these are not supported by the JVM. Instead, you simply use **arrays of arrays**. For this reason, there are no data types for multidimensional primitive-type arrays.

```kotlin
// Create an object array of primitive-type arrays
// [[4, 7, 1], [0, 5, 0], [8, 7, 3]]
val matrix: Array<IntArray> = arrayOf(intArrayOf(4, 7, 1), intArrayOf(0, 5, 0), intArrayOf(8, 7, 3))

// Create an object array of object arrays
// [["Name", "Age"], ["Dan", "38"], ["Jane", "29"]]
val table: Array<Array<String>> = arrayOf(arrayOf("Name", "Age"), arrayOf("Dan", "38"), arrayOf("Jane", "29"))

// Create a multidemsional array with constructors
// [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
val numpad: Array<IntArray> = Array(3) { i -> IntArray(3) { j -> i * 3 + j + 1 } }
```

## Iterate Through Arrays

You can use a normal `for` loop to iterate over the elements of an array.
```kotlin
for (country in countries) {
    println(country)
}
```
Use the `indices` property to iterate over the range of valid indices of an array.
```kotlin
for (i in countries.indices) {
    println(countries[i])
}
```
Use the `withIndex` extension function to iterate over the indexed values of an array.
```kotlin
// For demonstration purposes only
// indexWithCountry is of type IndexedValue<String>
for (indexWithCountry in countries.withIndex()) {
        println("${indexWithCountry.index}: ${indexWithCountry.value}")
}

// In practice, the IndexedValue is destructured
for ((i, country) in countries.withIndex()) {
    println("$i: $country")
}
```
There are, of course, many other ways to iterate over arrays, such as functional approaches.

## Variable Number Of Arguments

You can pass a variable number of arguments to a function via the `vararg` parameter.
```kotlin
fun printAllStrings(vararg strings: String) {
    for (s in strings) {
        println(s)
    }
}
```
To pass an array containing a variable number of arguments to a function, use the **spread** operator `*`. The spread operator passes each element of the array as individual argument to the function.
```kotlin
val names = arrayOf("Dan", "Jane", "Carlo")
printAllStrings(*names)
```

## Compare Arrays

To compare whether two arrays have the same elements in the same order, use the infix functions `contentEquals` and `contentDeepEquals` (for nested arrays).
```kotlin
if (names contentEquals arrayOf("Dan", "Jane", "Carlo")) {
    …
}
```
Don't use equality `==` and inequality `!=` operators to compare the contents of arrays. These operators call the `equals()` method internally, and in Java `equals()` for arrays compares the references and not the contents of the arrays.

## Transform Arrays

Kotlin has many useful functions to transform arrays. [Read more here](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/).
```kotlin
println(prices.sum()) // sum of all elements
println(prices.average()) // average of all elements
println(primes.binarySearch(7)) // search for the index of a specific element using binary search
```