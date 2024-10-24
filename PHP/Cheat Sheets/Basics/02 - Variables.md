# Variables

## Variables

Variables are declared with the dollar sign `$` followed by a name.
```php
$number = 44;
```

## Compile-Time Constants
In PHP there are only compile-time constants, whose value is already determined at compile time. It is not possible to initialize constants at runtime, as is the case in JavaScript, for example. Constants can only be defined at top level or in classes.

Constants are defined with the `const` keyword or the `define()` function and must be initialized immediately upon declaration.. Constants are automatically global and can be used across the entire script without the `global` keyword. 
```php
const PI = 3.14;
define("PHI", 1.62);

function echoPI() {
    echo PI; // output: 3.14
}
```

## Scopes

### Global Scope
Global variables are defined outside of functions and classes. Within functions, you can access global variables using the `global` keyword.
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
All global variables are stored in the superglobal array `$GLOBALS`. The index holds the name of the variable.
```php
$greeting = 'Hello World';

function echoGreeting() {
    $greeting = 'Hello PHP';

    // output global variable
    echo $GLOBALS["greeting"]; // output: Hello World

    // output local variable
    echo $greeting; // output: Hello PHP
}
```

### Superglobals
Several predefined variables are available in all scopes throughout a script without the need to use the `global` keyword. These superglobal variables are:
- `$GLOBALS`
- `$_SERVER`
- `$_GET`
- `$_POST`
- `$_FILES`
- `$_COOKIE`
- `$_SESSION`
- `$_REQUEST`
- `$_ENV`

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
