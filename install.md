# Getting started

## Installation

```bash
$ composer install
```

### .env

The framework use a `.env` file for environment variables thanks to [phpdotenv](https://github.com/vlucas/phpdotenv) package.

This file must be created based on the `.env.example` file.

Create a `.env` file by copying the `.env-example` file and modify the values with your environment:

```bash
$ make env
```

### Load environment variables in Makefile

Uncomment at the beginning of the `Makefile`:

```bash
include .env
```

## Servers

### Apache

The framework comes with an `/public/.htaccess` file.

### Nginx

In `nginx.conf` file of the server:

```nginx
try_files $uri /index.php;
```

## Usage

```bash
$ php -S 0.0.0.0:8080 -t public public/index.php
# or using Makefile
$ make serve
```

## Example

The framework comes with an example page `/` using [Bootstrap 4](https://getbootstrap.com).

## Clean

To clean (delete) the example files of the skeleton, just run:

```bash
$ make clean
```