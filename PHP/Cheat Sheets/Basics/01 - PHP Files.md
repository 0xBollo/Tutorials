# PHP Files

## PHP File Structure

PHP files can contain: 
- **HTML, CSS, JavaScript**: Static content sent directly to the browser.
- **PHP**: Dynamic code that is executed on the server. The result is sent to the browser as plain HTML.

PHP code is embedded within `<?php ?>` tags.
```php
<!DOCTYPE html>
<html>
<head>
    <title>PHP Tutorial</title>
</head>
<body>
    <?php
        echo 'Hello PHP';
    ?>
</body>
</html>
```

If the file only contains PHP code, `?>` can be omitted.
```php
<?php
echo 'Hello PHP';
```