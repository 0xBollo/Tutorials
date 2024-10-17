# Classes

## Classes and Objects

Classes in PHP are defined in a similar way to Java.
```php
class Book {
    // Properties
    public $author;
    public $title;
    public static $exampleAuthor = 'George Orwell';
    public static $exampleTitle = '1984';

    // Constructor
    public function __construct(string $author, string $title) {
        $this->author = $author;
        $this->title = $title;
    }

    // Methods
    public function print() {
        echo 'author: ' . $this->author . ', title: ' . $this->title . "\n";
    }

    public static function createExample(): Book {
        return new Book(Book::$exampleAuthor , Book::$exampleTitle);
    }
}
```
Classes are instantiated with the `new` keyword, as in Java.
```php
$book = new Book("George Orwell", "1984");
```
Instance members can be accessed with the **object operator** `->`.
```php
$book->author = "Other author";
$book->print();
```
Static methods are called with the **scope resolution operator** `::`.
```php
Book::$exampleAuthor = 'Other author';
$book = Book::createExample();
```

## Visibility Modifiers

Class members without modifiers are implicitly public. For properties, however, a modifier must be specified explicitly, unless the deprecated `var` keyword is used. Either way, it is recommended to explicitly specify the visibility modifiers for all members.

PHP offers similar visibility modifiers as Java:
- `public`: Class member can be accessed everywhere.
- `protected`: Class member can be accessed only within the class itself and by inheriting and parent classes.
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
