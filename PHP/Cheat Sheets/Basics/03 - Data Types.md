# Data Types

In PHP, as in JavaScript, there is only a limited number of data types.

## Scalar Types

Scalar types only contain a single value.
- `int`: integers
- `float`: floating point numbers
- `string`: strings
- `bool`: boolean values

```php
$number = 9; // int
$price = 1.99 // float
$greeting = 'Hello World' // string
$exists = true // bool
```

## Compound Types

These types can contain multiple values.
- `array`: are either indexed (integers as keys) or associative (user-defined keys, usually strings)
- `object`: instances of classes

```php
$primes = [2, 3, 5, 7, 11]; // indexed array
$prices = ['apple' => 1.29, 'watermelon' => 4.99]; // associative array

class Student {}
$student = new Student(); // object
```

## Special Types

In addition, there are two special types.
- `NULL`: has the only possible value `null`
- `resource`: references to external resources (e.g. database connections or file handles)

```php
$student = null; // null
$connection = mysqli_connect('localhost', 'root', 'pw123', 'testdb'); // resource
```

## Pseudo Types

Pseudotypes are special types that do not refer directly to specific data types, but can represent several possible types. They are used to indicate that a function can accept or return different data types.
- `mixed`: any type
- `callable`: function or method that can be called
- `iterable`: array or object that implements the `Traversable` interface
- …