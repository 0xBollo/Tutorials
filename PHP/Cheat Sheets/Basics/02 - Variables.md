# Variables

## Declaring Variables

Variables are declared with the dollar sign `$` followed by a name.
```php
$number = 44;
```

Constants are defined with the `const` keyword or the `define()` function
```php
const PI = 3.14;
define("PHI", 1.62);
```

## Scopes

### Global Scope
Global variables are defined outside of functions and classes. Within functions, you can access global variables using the keyword 'global'.
```php
$name = 'Eugene'; // global variable

function changeGlobalName() {
    global $name;
    $name = "Mara"; // reassign global variable
}

function changeLocalName() {
    $name = "Thomas"; // local variable (does not affect the global variable)
}

changeGlobalName();
changeLocalName();
echo $name; // output: Mara
```

### Local Scope
Local variables are defined within a function or method and are only available in this context.
```php
function defineLocalNumber() {
    $number = 99; // local variable
}

echo $number; // error: undefined variable '$number'
```

### Static Variables
Static variables only exist in the local function scope, but retain their value between function calls.
```php
function printIncrement() {
    static $i = 0; // static variable
    echo $i++;
}

printIncrement(); // output: 0
printIncrement(); // output: 1
printIncrement(); // output: 2
```
