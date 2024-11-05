# Namespaces

Namespaces are very similar to packages in Java, but do not necessarily have to correspond to the directory structure in the file system.

## Declaring Namespaces

Namespaces are declared at the beginning of a file using the `namespace` keyword, followed by the namespace path. The path segments are separated by `\`, whereby the leading `\` (for the global namespace) is omitted, as namespace declarations are always fully qualified anyway.
```php
<?php
namespace App\Http\Controllers;
```
Compile-time constants, classes and functions declared in this file belong to the declared namespace. **Runtime constants and variables exist in global scope and are not bound to the namespace**.

## Using Namespaces

There are three ways to access constants, classes and functions in a namespace:
- Unqualified name: `someFunction()`
- Qualified name: `subnamespace\someFunction()`
- Fully qualified name: `\namespace\subnamespace\someFunction()`

### Unqualified Name
If a constant, class or function is located in the **same namespace** or in **global namespace**, or if an **alias** is used, it can be accessed via the unqualified name.
```php
namespace App;

use function App\Math\add;

function greet() {
    echo "Hello";
}

greet(); // from the same namespace
strlen('Hello'); // from global namespace
add(3, 4); // from the alias
```

### Qualified Name
If a constant, class or function is located in a **subnamespace**, it can be accessed via the qualified name. This is specified as a relative path.
```php
namespace App;

Math\add(3, 5); // Math is a subnamespace of the App namespace
```

### Fully Qualified Name
The fully qualified name can be used **anywhere**. It is specified as an absolute path, starting from the global namespace `\`.
```php
\App\Math\add(3, 5);
```

## Aliasing / Importing

To avoid illegible path specifications, you can define aliases for namespaces, classes, constants and functions. You can import a path with the `use` keyword and define an alias for this path with the `as` keyword. If the `as` keyword is omitted, the last segment of the path is implicitly used as alias.
```php
// Import namespace
use App\Math; // use App\Math as Math

// Import class
use App\Math\Calculator; // use App\Math\Calculator as Calculator

// Import constant
use const App\Math\PI; // use App\Math\PI as PI

// Import function with explicit alias
use function App\Math\add as sum;

// Use the aliases
Math\subtract(3, 2);
new Calculator();
echo PI;
sum(2, 4);
```
As import names are always fully qualified anyway, the leading `\` (for the global namespace) is omitted.

## References

PHP: Hypertext Preprocessor (no date) 'Using namespaces: Basics', available at: https://www.php.net/manual/en/language.namespaces.basics.php.

PHP: Hypertext Preprocessor (no date) 'Using namespaces: Aliasing/Importing', available at: https://www.php.net/manual/en/language.namespaces.importing.php.