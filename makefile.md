# Makefile

This frameworks includes a Makefile as a task runner and for automations instead webpack, gulp or grunt for example.

## Script

- [Install](#instal)
- [Serve](#serve)
- [Test](#test)
- [Sitemap](#sitemap)
- [Assets optimization](#assets-optimization)

### Install

#### Env

Crate a `.env` file based on `.env.example` file.

```bash
make env
```

#### Clean

Remove example files.

```bash
make clean
```

### Serve

```bash
make serve # Start a simple PHP server
make debug # Start a PHP server using xdebug
```

### Test

Launch tests using PHP Unit.

```bash
make tests
```

### Sitemap

Create a sitemap file.

```bash
make sitemap
```

### Assets optimization

Optimize assets files (css and js files) by concatening and minifying them.

#### Configuration

Change variables in Makefile.

```bash
# CSS
CSS_FOLDER = public/assets/css
CSS_FILES = $(CSS_FOLDER)/style.css
CSS_TEMP = $(CSS_FOLDER)/style.css
CSS_FINAL = $(CSS_FOLDER)/style.min.css
# JS
JS_FOLDER = resources/assets/js
JS_FOLDER_PUBLIC = public/assets/js
JS_FILES = $(JS_FOLDER)/scripts.js
JS_TEMP = $(JS_FOLDER_PUBLIC)/scripts.js
JS_FINAL = $(JS_FOLDER_PUBLIC)/scripts.min.js
```

#### Saas

Convert saas files to css files.

```bash
make saas
```

#### Concatenation

Concat assets files.

```bash
make concat-css # Concat css files
make concat-js # Concat js files
make concat # Concat all files
```

#### Minification

Minify assets files.

For minification, this framework uses :

- https://cssminifier.com
- https://javascript-minifier.com

```bash
make minify-css # Minify css files
make minify-js # Minify js files
make minify # Minify all files
```

#### Optimization

Optimize assets files by converting, moving, concatening and minifying them depending the type of files (css or js files).

```bash
make optimize-css # Optimize css files
make optimize-js # Optimize js files
make optimize # Optimize all files
```