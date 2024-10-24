# Classes

## Define Classes

Classes in PHP are defined with the `class` keyword. In contrast to JavaScript, PHP classes are not functions under the hood, but real object-oriented constructs. A class can contain the following:
- Instance properties
- Static properties
- Constants (are automatically static)
- Magic Functions (e.g. the `__construct()` function)
- Instance methods
- Static methods
```php
class Book {
    // Properties
    public $author;
    public $title;
    public static $exampleAuthor = 'George Orwell';
    public static $exampleTitle = '1984';

    // Constants
    public const MAX_BOOK_COUNT = 1000;

    // Magic constructor function
    public function __construct($author, $title) {
        $this->author = $author;
        $this->title = $title;
    }

    // Methods
    public function print() {
        echo 'author: ' . $this->author . ', title: ' . $this->title . "\n";
    }

    public static function createExample(): Book {
        return new Book(self::$exampleAuthor , self::$exampleTitle);
    }
}
```

## Instantiate Classes

Classes are instantiated with the `new` keyword.
```php
$book = new Book("George Orwell", "1984");
```

## Access Class Members
Instance members can be accessed with the **object operator** `->`.
```php
$book->author = 'Other author';
$book->print();
```
Static members are called with the **scope resolution operator** `::`.
```php
Book::$exampleAuthor = 'Other example author';
$book = Book::createExample();
```

## Access Class Members within a Class

In Java, you can simply assign class members within the class by name. In PHP, on the other hand, you have to explicitly use certain keywords to access class members.

### `$this`
The `$this` variable refererences the current instance within a class context. It allows you to access the instance properties and methods of the current object. See this code snippet from the example above:
```php
public function __construct($author, $title) {
    $this->author = $author;
    $this->title = $title;
}
```

### `self`
The `self` keyword refers to the class in which it is used. It allows you to access static properties, constants and methods within the class. You can think of the `self` keyword as a placeholder for the name of the current class. See this code snippet from the example above:
```php
public static function createExample(): Book {
    return new Book(self::$exampleAuthor , self::$exampleTitle);
}
```
_Note: An alternative to the `self` keyword is the `static` keyword. `static` only makes a difference if it is used within a base class from which other classes inherit. More on this in the inheritance cheat sheet._

## Visibility Modifiers

Class members without modifiers are implicitly public. For instance properties, however, a modifier must be specified explicitly, unless the deprecated `var` keyword is used. Either way, it is recommended to explicitly specify the visibility modifiers for all members.

PHP offers similar visibility modifiers as Java:
- `public`: Class member can be accessed everywhere.
- `protected`: Class member can be accessed only within the class itself and by child and parent classes.
- `private`: Class member can only be accessed within the class.

There is no equivalent in PHP for the implicit `package-private` modifier in Java.

## Magic Methods

Magic methods are methods that override PHP's default behavior when certain actions are performed on an object.

Some important magic methods are:
- `__construct(…)`: Is called when an instance of the class is created.
- `__destruct()`: Is called when an instance of the class is destroyed.
- `__get($name)`: Is called when a non-existent or private property is accessed.
- `__set($name, $value)`: Is called when a non-existent or private property is set.
- `__call($name, $arguments)`: Is called when a non-existent method is called.
- `__callStatic($name, $arguments)`: Is called when a non-existent static method is called.
- `__toString()`: Is called when an object is converted to a string.
- `__invoke()`: Is called when an object is called like a function.
