# Features

This framework comes with all the basic features to create a website/web application.

To remove one of them, simply remove its dependency in the `src/dependencies.php` file of the skeleton.

## Index

- [.env](#dotenv)
- [Config files](#config-files)
- [Templating](#templating)
- [Logging](#logging)
- [Database](#database)
- [Flash messages](#flash-messages)
- [Basic authentification](#basic-authentification)
- [Authentification](#authentification)
- [CSRF protection](#csrf-protection)
- [Validation](#validation)
- [Datetime](#datetime)
- [Sitemap](#sitemap)
- [Mail](#mail)
- [Localization](#localization)
- [IP address](#ip-address)
- [Tests](#tests)

## dotenv

The framework use a `.env` file for environment variables thanks to [phpdotenv](https://github.com/vlucas/phpdotenv) package.

📖 [Documentation](https://github.com/vlucas/phpdotenv)

## Config files

The framework use config files located in `config/` folder thanks to [hassankhan/config](https://github.com/hassankhan/config) to load the files.

📖 [Documentation](https://github.com/hassankhan/config)

### Dependency

This feature has a dependency in Slim container in `src/dependencies.php` file.

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

For templating, the framework uses [Twig](https://twig.symfony.com) dependenciesrary.

📖 [Documentation](https://twig.symfony.com/doc/2.x/)

The framework uses 2 add-ons for Twig:

| dependenciesrary | Description |
| ------- | ----------- |
| [Slim Twig view](https://github.com/slimphp/Twig-View) | Slim Framework view layer built on top of Twig |
| [Slim Twig Flash](https://github.com/kanellov/slim-twig-flash) | Twig extension for rendering slim flash messages |

### Dependency

This feature has a dependency in Slim container in `src/dependencies.php` file.

```php
$container['view'];
```

### Usage

```php
// Display a view
return $this->renderView($response, 'index.html');
// Fetch a view file
return $this->fetchView($filename, $params);
```

## Logging

For logging, the framework uses [Monolog](https://github.com/Seldaek/monolog) dependenciesrary.

📖 [Documentation](https://github.com/Seldaek/monolog/tree/master/doc)

### Dependency

This feature has a dependency in Slim container in `src/dependencies.php` file.

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

For database connection, the framework uses his own package.

### Dependency

This feature has a dependency in Slim container in `src/dependencies.php` file.

```php
$container['db'];
```

### Usage

```php
$posts = $this->db->fetchAll('SELECT * FROM posts');
```

## Flash messages

For flash messages, this framework uses [Slim Flash](https://github.com/slimphp/Slim-Flash).

📖 [Documentation](https://github.com/slimphp/Slim-Flash)

The framework uses [Slim Twig Flash](https://github.com/kanellov/slim-twig-flash) for rendering slim flash messages in Twig.

### Dependency

This feature has a dependency in Slim container in `src/dependencies.php` file.

```php
$container['flash'];
```

### Usage

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

This feature has a dependency in Slim container in `src/dependencies.php` file.

To activate the basic authentification, just uncomment the dedicated code to add the middleware:

```php
// Http authentification
$app->add(new \Slim\Middleware\HttpBasicAuthentication([
    "users" => [
        "root" => "t00r",
    ]
]));
```

## Authentification

For authentification, this framework uses his own package.

## CSRF protection

For flash messages, this framework uses [Slim CSRF](https://github.com/slimphp/Slim-Csrf).

📖 [Documentation](https://github.com/slimphp/Slim-Csrf)

### Dependency

This feature has a dependency in Slim container in `src/dependencies.php` file.

```php
$container['csrf'];

// Middleware
$app->add(new \Slim\Csrf\Guard);
```

## Validation

For validation, this framework uses [Respect/Validation](https://github.com/Respect/Validation).

📖 [Documentation](https://github.com/Respect/Validation)

### Usage

```php
use Respect\Validation\Validator;
```

## Datetime

This framework use [Carbon](https://github.com/briannesbitt/Carbon) to extend DateTime.

📖 [Documentation](https://github.com/briannesbitt/Carbon)

### Usage

```php
use Carbon\Carbon;

printf("Now: %s", Carbon::now());
```

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

## Mail

This framework send emails thanks to [Mailgun](https://www.mailgun.com) using the [official SDK for PHP](https://github.com/mailgun/mailgun-php).

- 📖 [Package documentation](https://github.com/mailgun/mailgun-php)
- 📖 [Documentation](https://documentation.mailgun.com)

### Usage

1. Set `.env` variables:

    ```bash
    MAILGUN_DOMAIN=
    MAILGUN_PRIVATE_KEY=
    ```

2. Add:

    ```php
    use Icarus\Mail as Mail;

    $mail = new Mail();
    $params = [
        'from' => 'john@appleseed.com',
        'to' => 'test@test.com',
        'subject' => 'Test',
        'text' => "If you received this email, it means emails work on your website!"
    ];
    $mail->send($params);
    ```

## Localization

This framework use [tboronczyk/localization-middleware](https://github.com/tboronczyk/localization-middleware) for localization.

📖 [Documentation](https://github.com/tboronczyk/localization-middleware)

ℹ️ Localization is not activated by default.

### Usage

1. Uncomment in `src/middlewares.php`:

    ```php
    use Boronczyk\LocalizationMiddleware;

    $availableLocales = ['en_US', 'fr_CA', 'es_MX', 'eo'];
    $defaultLocale = 'en_US';
    $app->add(new LocalizationMiddleware($availableLocales, $defaultLocale));
    ```

2. Add:

    ```php
    $app->get('/', function ($req, $resp, $args) {
        $attrs = $req->getAttributes();
        $locale = $attrs['locale'];
        return $resp->write("The locale is $locale.");
    });
    ```

## IP address

To determine the client IP address, this framework uses [akrabat/ip-address-middleware](https://github.com/akrabat/ip-address-middleware/).

📖 [Documentation](https://github.com/akrabat/ip-address-middleware/)

ℹ️ Client IP address determination is not activated by default.

### Usage

```php
$checkProxyHeaders = true; // Note: Never trust the IP address for security processes!
$trustedProxies = ['10.0.0.1', '10.0.0.2']; // Note: Never trust the IP address for security processes!
$app->add(new RKA\Middleware\IpAddress($checkProxyHeaders, $trustedProxies));

$app->get('/', function ($request, $response, $args) {
    $ipAddress = $request->getAttribute('ip_address');

    return $response;
});
```

## Tests

To execute the test suite, you'll need [phpunit](https://phpunit.de).

Phpunit is installed using Composer on your local/dev environment.

```bash
$ phpunit
```