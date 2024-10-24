# Inheritance

## Extend Classes
Inheriting classes are defined with the `extends` keyword. When extending a class, the subclass inherits all of the public and protected properties, constants and methods from the parent class. 

```php
class Person {
    public $firstName;
    public $lastName;

    public function __construct($firstName, $lastName) {
        $this->firstName = $firstName;
        $this->lastName = $lastName;
    }
}

class Student extends Person {
    public $matrNr;

    public function __construct($matrNr, $firstName, $lastName) {
        parent::__construct($firstName, $lastName); // parent constructor call
        $this->matrNr = $matrNr;
    }
}
```

## Override Methods

Inherited methods can be overridden by redefining the methods (use the same name) in the child class.

## Keyword `final`

The `final` keyword can be used to prevent class inheritance or method overriding. The `final` keyword is not applicable to properties in PHP.

## Access Class Members in Inheritance Hierarchy

### `parent`
The `parent` keyword refers to the direct parent class of the class in which it is used. It allows you to explicitly access members of the parent class, even if they have been overridden in the child class.

In contrast to the `super` keyword in Java, which is only available for instance methods and attributes, the `parent` keyword in PHP can be used for both static and non-static members.

The `parent` keyword is always used in a static context syntax `parent::member`, even if it is an instance method.

```php
class Student extends Person {
    public $matrNr;

    public function __construct($matrNr, $firstName, $lastName) {
        parent::__construct($firstName, $lastName);
        $this->matrNr = $matrNr;
    }

    public function __toString() {
        return parent::__toString() . ', ' . $this->matrNr;
    }
}
```

### `static`
The `static` keyword refers to the calling class at runtime (**late static binding**), i.e. either the class in which it is used or a subclass. It allows you to access static properties, constants and methods of the calling class from the base class. The `self` keyword, on the other hand, always refers to the class in which it is used.
```php
class ClassA {
    protected static $name = 'ClassA';

    public static function getSelfName() {
        return self::$name;
    }

    public static function getStaticName() {
        return static::$name;
    }
}

class ClassB extends ClassA {
    protected static $name = 'ClassB';
}

ClassA::getSelfName(); // ClassA
ClassA::getStaticName(); // ClassA

ClassB::getSelfName(); // ClassA
ClassB::getStaticName(); // ClassB
```
_Note: Java has no such mechanism for late static binding._

## Abstract Classes

Abstract classes are defined with the `abstract` keyword, as in Java.
```php
abstract class ParentClass {
    abstract public function someMethod();
}
```
