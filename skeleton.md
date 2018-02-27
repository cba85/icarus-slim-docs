# Skeleton

The skeleton of the framework, located [here](https://github.com/cba85/icarus-slim), has an architecture that follows the rules of [pds/skeleton](https://github.com/php-pds/skeleton) the standard filesystem skeleton suitable for all PHP packages mixed with the ones of [Ruby on Rails](http://guides.rubyonrails.org/getting_started.html#creating-the-blog-application) for a web application.

## Architecture

```
bin/
config/
└── settings.php
db/
docs/
logs/
public/
├── assets/
├── .htaccess
├── favicon.ico
├── index.php
└── robots.txt
resources/
├── assets
└── views
src/
├── Controllers/
├── Helpers/
├── Middleware/
├── Models/
├── dependencies.php
├── middlewares.php
└── routes.php
tests/
tmp/
├── logs/
└── views/
.editorconfig
.env.example
.gitignore
.user.ini
composer.json
Makefile
Procfile
```

## .editorconfig

The framework has an [editorconfig](http://editorconfig.org) file to respect PHP standards coding style.

## .user.ini

The framework has an [.user.ini](http://php.net/manual/fr/configuration.file.per-user.php) file for changing `php.ini` settings on some servers. (e.g [Heroku](https://devcenter.heroku.com/articles/custom-php-settings#php-runtime-settings)).

## Procfile

A [Procfile](https://devcenter.heroku.com/articles/getting-started-with-php#define-a-procfile) is included in the framework to explicitly declare what command should be executed to start the app on [Heroku](https://www.heroku.com/home).

## Folders

| Description                | Folder name  |
| -------------------------- | -------------|
| Command-line executables   | `bin/`       |
| Configuration files        | `config/`    |
| Database schema/migrations | `db/`        |
| Documentation files        | `docs/`      |
| Log files                  | `logs/`      |
| Web server files           | `public/`    |
| Other resource files       | `resources/` |
| PHP source code            | `src/`       |
| Test code                  | `tests/`     |
| Temporary files            | `tmp/`       |

## Assets

| Path | Description|
|-|-|
| `resources/assets/` | Assets for development (unminified)  |
| `public/assets/` | Assets for production (minified) and libraries |

## Helpers

| Path | Description|
|-|-|
| `src/Helpers/` | Helpers folder |

The helper functions are autoloaded by Composer.

## Controllers

| Path | Description|
|-|-|
| `src/Controllers/` | Controllers folder |
| `src/Controllers/Controller.php` | Base Controller |

## Middlewares

| Path | Description|
|-|-|
| `src/Middlewares/` | Middlewares folder |
| `src/middlewares.php` | Register middlewares |

## Dependencies

| Path | Description|
|-|-|
| `src/dependencies.php` | DIC configuration |

## Views

| Path | Description|
|-|-|
| `resources/lang/` | Internationalisation files |
| `resources/views/` | Views (Twig) folder |

# Makefile

A Makefile is included with the project.

```bash
$ make [command]
```

Use `help` to list available commands.

Scripts are categorized:
- Serve the project
- Tests
- Sitemap
- Minify css and js
- Concat css and js

### Sources

- http://wonko.com/post/simple-makefile-to-minify-css-and-js
- https://gist.github.com/bpierre/1341808