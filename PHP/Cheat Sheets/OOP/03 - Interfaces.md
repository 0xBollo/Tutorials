# Interfaces

## Define Interfaces
Interfaces are defined with the `interface` keyword. Interfaces can contain the following:
- Abstract methods
- Magic functions
- Constants
```php
interface MyInterface {
    function abstractMethod();
    function __invoke();
    const CONSTANT = 'interface constant';
}
```

## Implement Interfaces

Classes can implement interfaces with the `implements` keyword.
```php
class MyClass implements MyInterface {
    function abstractMethod() {
        // TODO: Implement abstractMethod() method.
    }

    function __invoke() {
        // TODO: Implement __invoke() method.
    }
}
```