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
- `is_scalar()` - whether it is a scalar type
- `is_numeric()` - whether it is a number or a numeric string
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

## Type Casting

### Explicit Casting
You can explicitly cast types by writing the desired type in round brackets in front of it.
```php
$oneString = '1';
$one = (int) $oneString;
$true = (bool) $one;
```
Supported types for explicit casting:
- `(int)` / `(integer)`
- `(float)` / `(double)` / `(real)`
- `(string)`
- `(bool)` / `(boolean)`
- `(array)`
- `(object)`
- `(unset)` - converts to data type `NULL`

### Explicit Casting with Functions
Alternatively, you can use functions for explicit casting.
```php
$oneString = '1';
$one = intval($oneString);
$true = boolval($one);
```
The following functions are available:
- `intval()`
- `floatval()` / `doubleval()`
- `strval()`
- `boolval()`

#### `settype()`
This function changes the type of the specified variable directly.
```php
$one = '1';
settype($one, 'int');
```
The following values for the type are possible:
- `'int'` / `'integer'`
- `'float'` / `'double'`
- `'string'`
- `'bool'` / `'boolean'`
- `'array'`
- `'object'`
- `'null'`

### Implicit Casting (Type Juggling)
Sometimes PHP can automatically convert the data type based on the context, e.g. for operations or function calls. This automatic adjustment of data types is called **type juggling**.
```php
function double(int $number) {
    return $number * 2;
}

// string '22' is automatically converted to int 22
double('22');
```
