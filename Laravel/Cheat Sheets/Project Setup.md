# Project Setup

## Prerequisites

Make sure you have installed:
- Node.js
- PHP
- Composer
- Laravel Installer

Check whether you have installed the `unzip` command.
```bash
which unzip
```
If the command is installed, its path is displayed. If the output is empty, you must install the command.
```bash
sudo apt install unzip
```

Check whether you have installed the following PHP extensions:
- ZIP
- XML
- MySQL (or the PDO extension of a different database)
```bash
php --ini
```
The following lines should be displayed, among others:
```
/etc/php/<version>/cli/conf.d/15-xml.ini
/etc/php/<version>/cli/conf.d/20-mysqli.ini
/etc/php/<version>/cli/conf.d/20-zip.ini
```
If this is not the case, then install the corresponding extensions.
```bash
sudo apt install php-zip
sudo apt install php-xml
sudo apt install php-mysql
```

## Creating an Application

Create a new application using the Laravel Installer.
```bash
laravel new my-project
``` 

## Starting the Development Server

Once the application has been created, you can start Laravel's local development server, queue worker, and Vite development server using the `dev` Composer script.
```bash
npm install && npm run build
composer run dev
```
The application should now be accessible at http://localhost:8000. However, an internal server error is probably displayed because the database connection has not yet been configured.

## Configuring Database Connection

The database connection is configured in the `.env`.
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=basic_laravel_setup
DB_USERNAME=maria
DB_PASSWORD=maria
```

To perform the initial migrations, use the Artisan Console.
```php
php artisan migrate
```
