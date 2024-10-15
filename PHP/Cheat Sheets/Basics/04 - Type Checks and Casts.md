# Type Checks and Casts

## Type Checks

### `getType()`

This function returns the data type of a variable as a string.
```php
$number = 4;
echo gettype($number); // output: integer
```
Possible return values:
- `'integer'`
- `'double'` (alias for `float`)
- `'string'`
- `'boolean'`
- `'array'`
- `'object'`
- `'NULL'`
- `'resource'`
- `'resource (closed)'`
- `'unknown type'`

### `is_*()`

PHP offers a number of specific functions to check **whether a variable has a specific type**:
- `is_int()` / `is_integer()` / `is_long()`
- `is_float()` / `is_double()` / `is_real()`
- `is_bool()`
- `is_string()`
- `is_array()`
- `is_object()`
- `is_null()`
- `is_resource()`

```php
$greeting = 'Hello World';
is_string($greeting); // true
```

You can also check for specific **pseudo types**:
- `is_callable()`
- `is_iterable()`

```php
$add = function($a, $b) {
    return $a + $b;
};

// Check the pseudo type
is_callable($add); // true

// Check the underlying data type
gettype($add); // 'object'
```

You can also do some other checks:
- `is_scalar()` (whether it is a scalar type)
- `is_numeric()` (whether it is a number or a numeric string)
- …

### `var_dump()`

This function outputs the data type and the value. This is particularly useful for debugging.
```php
$number = 14;
var_dump($number); // output: int(14)
```

### `instanceof`

This is used to check whether an object is an instance of a certain class.

```php
class Student {}
$student = new Student();

$student instanceof Student; // true
gettype($student); // 'object'
```