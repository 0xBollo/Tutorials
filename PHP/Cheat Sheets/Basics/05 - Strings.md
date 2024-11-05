# Strings

Strings are surrounded by single quotes or double quotes. Double quotes support the interpolation of variables and the interpretation of special escape sequences, single quotes does not.
```php
$name = 'Joe';
echo 'Hello $name\n'; // output: Hello $name\n
echo "Hello $name\n"; // output: Hello Joe
```
