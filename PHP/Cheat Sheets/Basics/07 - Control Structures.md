# Control Structures

## Conditions

### If Statement
The `if` statement works as in Java.
```php
$x = 10;

if ($x > 0) {
    echo "x is positive";
} elseif ($x < 0) {
    echo "x is negative";
} else {
    echo "x is zero";
}
```

### Switch Statement
The `switch` statement works as in Java.
```php
$day = 2;

switch ($day) {
    case 6:
        echo "Saturday";
        break;
    case 7:
        echo "Sunday";
        break;
    default:
        echo "Weekday";
}
```

## Loops

### While Loop
The `while` loop works as in Java.
```php
$i = 1;

while ($i <= 5) {
  echo $i++;
}
```
You can also use an alternative syntax with the `endwhile` statement.
```php
$i = 1;

while ($i <= 5):
  echo $i++;
endwhile;
```

### Do-While Loop
The `do-while` loop works as in Java.
```php
$i = 1;

do {
  echo $i++;
} while ($i <= 5);
```

### For Loop
The `for` loop works as in Java.
```php
for ($i = 0; $i <= 5; $i++) {
  echo $i;
}
```

### Foreach Loop
The `foreach` loop can iterate over **arrays** and **objects**, accessing the values or key-value pairs.

Iterating over an **indexed array**:
```php
$primes = [2, 3, 5];

// Iterate over values only
foreach ($primes as $prime) {
    echo $prime . "\n";
}
// Output:
// 2
// 3
// 5

// Iterate over indexed values
foreach ($primes as $index => $prime) {
    echo "Index $index: $prime\n";
}
// Output:
// Index 0: 2
// Index 1: 3
// Index 2: 5
```

Iterating over an **associative array**:
```php
$prices = ['apple' => 1.29, 'watermelon' => 4.99, 'pineapple' => 2.99];

// Iterate over values only
foreach ($prices as $price) {
    echo $price . "\n";
}
// Output:
// 1.29
// 4.99
// 2.99

// Iterate over key-value pairs
foreach ($prices as $name => $price) {
    echo $name . ': ' . $price . "\n";
}
// Output:
// apple: 1.29
// watermelon: 4.99
// pineapple: 2.99
```

Iterating over an **object**:
```php
class Book {
    public $author;
    public $title;

    public function __construct(string $author, string $title) {
        $this->author = $author;
        $this->title = $title;
    }
}

$book = new Book("George Orwell", "1984");

// Iterate over property values only
foreach ($book as $propertyValue) {
    echo $propertyValue . "\n";
}
// Output:
// George Orwell
// 1984

// Iterate over key-value pairs
foreach ($book as $propertyName => $propertyValue) {
    echo $propertyName . ": " . $propertyValue . "\n";
}
// Output:
// author: George Orwell
// title: 1984
```

### Break and Continue
PHP supports `break` and `continue` operators in loops.