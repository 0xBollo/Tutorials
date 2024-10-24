# Functions

## Define Functions

Functions are defined with the `function` keyword.
```php
function greet($name, $greeting) {
    echo $greeting . ' ' . $name . "\n";
}
```

## Call Functions

Functions are called using the standard approach.
```php
greet('Gundula', 'Hello');
```

## Default Arguments

Function parameters can have default values.
```php
function greet($name, $greeting = 'Hello') {
    echo $greeting . ' ' . $name . "\n";
}
```

## Variable Number of Arguments

PHP also supports a variable number of arguments. The variable-length argument must be the last one.
```php
function greetAll(...$names) {
    foreach ($names as $name) {
        echo $name . "\n";
    }
}
```
