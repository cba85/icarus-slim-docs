# Features

This framework comes with all the basic features to create a website/web application.

To remove one of them, simply remove its dependency in the `src/lib.php` file of the skeleton.

## Index

- [.env](#dotenv)
- [Config files](#config-files)
- [Templating](#templating)
- [Logging](#logging)
- [Database](#database)
- [Flash messages](#flash-messages)
- [Basic authentification](#basic-authentification)
- [CSRF protection](#csrf-protection)
- [Validation](#validation)
- [Sitemap](#sitemap)
- [Tests](#tests)

## dotenv

The framework use a `.env` file for environment variables thanks to [phpdotenv](https://github.com/vlucas/phpdotenv) package.

📖 [Documentation](https://github.com/vlucas/phpdotenv)

## Config files

The framework use config files located in `config/` folder thanks to [hassankhan/config](https://github.com/hassankhan/config) to load the files.

📖 [Documentation](https://github.com/hassankhan/config)

### Dependency

This feature has a dependency in Slim container in `src/lib.php` file.

```php
$container['config'];
```

### List

| File | Description |
|-|-|
| `app.php` | Application settings |
| `database.php` | Database settings |
| `logger.php` | Monolog settings |
| `slim.php` | Slim framework settings |
| `view.php` | Twig settings |

### Usage

Controller helper:

```php
// One setting
$this->config('app.url');
// All settings
$this->config();
```

Using the package natively:

```php
// One setting
$this->config->get('app.url');
// All settings
$this->config->all();
```

## Templating

For templating, the framework uses [Twig](https://twig.symfony.com) library.

📖 [Documentation](https://twig.symfony.com/doc/2.x/)

The framework uses 2 add-ons for Twig:

| Library | Description |
| ------- | ----------- |
| [Slim Twig view](https://github.com/slimphp/Twig-View) | Slim Framework view layer built on top of Twig |
| [Slim Twig Flash](https://github.com/kanellov/slim-twig-flash) | Twig extension for rendering slim flash messages |

### Dependency

This feature has a dependency in Slim container in `src/lib.php` file.

```php
$container['view'];
```

### Usage

```php
// Display a view
return $this->view($response, 'index.html');
```

## Logging

For logging, the framework uses [Monolog](https://github.com/Seldaek/monolog) library.

📖 [Documentation](https://github.com/Seldaek/monolog/tree/master/doc)

### Dependency

This feature has a dependency in Slim container in `src/lib.php` file.

```php
$container['logger'];
```

### Usage

Controller helper:

```php
$this->log($text, $type);
```

Using the package natively:

```php
    $this->container->logger->debug($text);
    $this->container->logger->info($text);
    // ...
```

## Database

For database connection, the framework uses [aura/sql](https://github.com/auraphp/Aura.Sql).

📖 [Documentation](https://github.com/auraphp/Aura.Sql/blob/3.x/docs/index.md)

### Dependency

This feature has a dependency in Slim container in `src/lib.php` file.

```php
$container['db'];
```

## Flash messages

For flash messages, this framework uses [Slim Flash](https://github.com/slimphp/Slim-Flash).

📖 [Documentation](https://github.com/slimphp/Slim-Flash)

The framework uses [Slim Twig Flash](https://github.com/kanellov/slim-twig-flash) for rendering slim flash messages in Twig.

### Dependency

This feature has a dependency in Slim container in `src/lib.php` file.

```php
$container['flash'];
```

## Usage

Using controller helper:

```php
 $this->flash($message, $type);
```

Using the package natively:

```php
$this->flash->addMessage($type, $message);
```

In a Twig file:

```html
<!-- Flash message -->
{% if flash.success %}
    <div>{{ flash.success[0] }}</div>
{% elseif flash.error %}
    <div>{{ flash.error[0] }}</div>
{% endif %}
```

## Basic authentification

For basic authentification, this framework uses [Slim Basic Auth](https://github.com/tuupola/slim-basic-auth).

📖 [Documentation](https://appelsiini.net/projects/slim-basic-auth/)

ℹ️ Basic authentification is not activated by default.

### Dependency

This feature has a dependency in Slim container in `src/lib.php` file.

To activate the basic authentification, just uncomment the dedicated code to add the middleware:

```php
// Http authentification
$app->add(new \Slim\Middleware\HttpBasicAuthentication([
    "users" => [
        "root" => "t00r",
    ]
]));
```

## CSRF protection

For flash messages, this framework uses [Slim CSRF](https://github.com/slimphp/Slim-Csrf).

📖 [Documentation](https://github.com/slimphp/Slim-Csrf)

### Dependency

This feature has a dependency in Slim container in `src/lib.php` file.

```php
$container['csrf'];

// Middleware
$app->add(new \Slim\Csrf\Guard);
```

## Validation

For validation, this framework uses [Slim Validation](https://github.com/DavidePastore/Slim-Validation), that internally uses [Respect/Validation](https://github.com/Respect/Validation).

📖 [Slim Validation documentation](https://github.com/DavidePastore/Slim-Validation)<br>
📖 [Respect Validation documentation](https://github.com/Respect/Validation)

## Sitemap

To create a sitemap of the website, this framework uses [samdark/sitemap](https://github.com/samdark/sitemap).

📖 [Documentation](https://github.com/samdark/sitemap)

By default, a route is created in `src/routes.php` and a controller `SitemapController.php` is included in `src/Controllers`.

### Usage

1. Edit the `create()` method in `src/Controllers/SitemapController` to add pages in the sitemap.

2. To create a sitemap, launch the Makefile command:

    ```bash
    make sitemap
    ```

The sitemap file `sitemap.xml` is created in `public/` folder.

## Tests

To execute the test suite, you'll need [phpunit](https://phpunit.de).

Phpunit is installed using Composer on your local/dev environment.

```bash
$ phpunit
```