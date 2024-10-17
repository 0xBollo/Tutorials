# Arrays

## Create Arrays
To create an array, you can use either an **array literal** or the `array()` function.
```php
// Array literal
$primes = [2, 3, 5, 7, 11];

// array() function
$names = array('Erwin', 'Thomas', 'Stefan');
```

## Manipulate Arrays
Arrays in PHP have a dynamic size, so you can add and delete elements even after they have been created.

### Add Elements

#### `[]` Operator
The `[]` operator can be used to add an element to the end of an array.
```php
$primes = [2, 3, 5, 7];
$primes[] = 11;
// $primes is now [2, 3, 5, 7, 11]
```

#### `array_push()`
The `array_push()` function adds one or more elements to the end of an array.
```php
$primes = [2, 3, 5];
array_push($primes, 7, 11);
// $primes is now [2, 3, 5, 7, 11]
```

#### `array_unshift()`
The `array_unshift()` function adds one or more elements to the beginning of an array.
```php
$numbers = [2, 3];
array_unshift($numbers, 0, 1);
// $numbers is now [0, 1, 2, 3]
```

### Remove Elements

#### `array_pop()`
The `array_pop()` function removes the last element from an array and returns it.
```php
$numbers = [0, 1, 2, 3];
array_pop($numbers);
// $numbers is now [0, 1, 2]
```

#### `array_shift()`
The `array_shift()` function removes the first element from an array and returns it.
```php
$numbers = [0, 1, 2, 3];
array_shift($numbers);
// $numbers is now [1, 2, 3]
```

#### `unset()`
The `unset()` function can be used to completely delete a key-value pair. This can create gaps in the array.
```php
$names = ['Eugene', 'Mara', 'Thomas', 'Bertha'];
unset($names[1]);
// $names is now [0 => 'Eugene', 2 => 'Thomas', 3 => 'Bertha']
```

### `array_splice()`
The `array_splice()` function can be used to remove, replace or insert parts of an array.

**Parameters:**
1. `$array`: The array that is modified.
2. `$offset`: The position in the array at which the removal/replacement begins. Positive values count from the beginning, negative values count from the end of the array.
3. `$length` (optional): The number of elements to be removed. If this parameter is omitted, all elements from `$offset` onwards are removed. A negative value indicates how many elements from the end are not deleted. For example, a value of `-2` means that the last two elements are not deleted.
4. `$replacement` (optional): An array or value that replaces the removed elements. If you do not want a replacement, leave this parameter empty.
```php
// Add two elements starting from index 1
$names = ['Marie', 'Daniel'];
array_splice($names, 1, 0, ['Henri', 'Wolfgang']);
// $names is now ['Marie', 'Henri', 'Wolfgang', 'Daniel']

// Remove two elements from index 1 and replace them with two new elements
$fruits = ['Apple', 'Strawberry', 'Pineapple', 'Blueberry'];
array_splice($fruits, 1, 2, ['Banana', 'Kiwi']);
// $fruits is now ['Apple', 'Banana', 'Kiwi', 'Blueberry']

// Remove two elements from index 1
$numbers = [1, 2, 3, 4, 5];
array_splice($array, 1, 2);
// $numbers is now [1, 4, 5]

// Remove the second last element
$primes = [2, 3, 5, 7, 11];
array_splice($primes, -2, 1);
// $primes is now [2, 3, 5, 11]
```