# Type Declarations

Type declarations can be added to:
- Function arguments
- Return values
- Class properties
- Class constants

```php
function add(int $a, int $b): int {
    return $a + $b;
}

class ClassA {
    public string $property;
    public const int CONSTANT = 99;
}
```

## Type Errors

PHP checks type declarations at runtime. If a value does not satisfy the declared type, a `TypeError` is usually raised.

## Strict Mode

By default, if an argument does not satisfy the declared type, PHP attempts to implicitly cast it to the expected type. This can lead to unexpected behavior. To enforce exact type matching, you can activate strict mode at the beginning of the file.

```php
<?php
declare(strict_types=1);
```
