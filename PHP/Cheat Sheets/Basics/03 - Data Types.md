# Data Types

PHP's type system supports various atomic types that can be composed together to create more complex types.

## Atomic Types

### Scalar Types

Scalar types only contain a single value.
- `bool`: boolean values
- `int`: integers
- `float`: floating point numbers
- `string`: strings

```php
$exists = true; // bool
$number = 9; // int
$price = 1.99; // float
$greeting = 'Hello World'; // string
```

### Complex Types

These types can contain multiple values.
- `array`: are either indexed (integers as keys) or associative (user-defined keys, usually strings)
- `object`: instances of classes

```php
$primes = [2, 3, 5, 7, 11]; // indexed array
$prices = ['apple' => 1.29, 'watermelon' => 4.99]; // associative array

class Student {}
$student = new Student(); // object
```

### Special Types

In addition, there are two special types.
- `NULL`: has the only possible value `null`
- `resource`: references to external resources (e.g. database connections or file handles)

```php
$student = null; // null
$connection = mysqli_connect('localhost', 'root', 'pw123', 'testdb'); // resource
```

### Pseudo Types

Pseudo types are not actual data types. They serve as placeholders in type declarations, representing a range of possible types or specific characteristics a value must satisfy.
- `void`: return-only type indicating that a function does not return a value, but can still return
- `never`: return-only type indicating that a function never returns (PHP's bottom type)
- `mixed`: any type
- `callable`: function or method that can be called
- `iterable`: array or object that implements the `Traversable` interface
- Value types: `true` and `false`
- Relative class types: `self`, `parent` and `static`

### Class Types (User-defined Types)

Class types represent objects that are instances of specific classes or their subclasses. However, the underlying data type of each object is `object`, regardless of its class type.
```php
class Student {}
$student = new Student();

$student instanceof Student; // true
gettype($student); // 'object'
```

## Composite Types

It is possible to combine multiple atomic types into composite types. The `mixed` type and all return-only types are standalone and cannot be used in composite types.

### Intersection Types

An intersection type accepts values that satisfy multiple class-type declarations. The individual types are joined by the `&` symbol.

```php
class A implements InterfaceA {}
class B implements InterfaceB {}
class AB implements InterfaceA, InterfaceB {}

// Parameter $ab must implement both InterfaceA and InterfaceB
function testAB(InterfaceA&InterfaceB $ab) {}

testAB(new A()); // TypeError because argument is not of type B
testAB(new B()); // TypeError because argument is not of type A
testAB(new AB()); // works because argument is of type A and B
```

### Union Types

A union type accepts values of multiple different types. The individual types are joined by the `|` symbol.

```php
// Parameter $x must be of type object or null
function testUnion(object|null $x) {}

testUnion(44); // TypeError because argument is not of type object or null
testUnion(new stdClass()); // works because argument is of type object
testUnion(null); // works because argument is of type null
```

### Nullable Types

For union types of the form `A|null` there is a simplified notation `?A`.

```php
// Parameter $x must be of type int or null
function testUnion(?int $x) {}

testUnion("Hello"); // TypeError because argument is not of type int or null
testUnion(44); // works because argument is of type int
testUnion(null); // works because argument is of type null
```

### Type Aliases

PHP supports two type aliases.
- `mixed`: corresponds to the union type of `bool|int|float|string|array|object|null|resource`
- `iterable`: corresponds to the union type of `array|Traversable`

PHP does not support user-defined type aliases.

## References

PHP: Hyptertext Preprocessor (no date) 'Type System', available at: https://www.php.net/manual/en/language.types.type-system.php.