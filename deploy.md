# Deploy

## VPS

On VPS like DigitalOcean, Linode... that uses Ubuntu

## Heroku

The framework includes a `Procfile` to initiate a php web server on an Heroku server.

To deploy on an Heroku server, you have to do some modification because the `dotenv` library is not compatible with the Heroku environment variables.

1. Remove `composer.lock` in `.gitignore` file.

2. Create an `HEROKU` variable on your Heroku application:

    ```
    HEROKU=true
    ```

3. In `index.php` file, add:

    ```php
    // Load secret parameters (.env)
    if (env('HEROKU') == null) {
        $dotenv = new Dotenv\Dotenv(__DIR__ . '/../');
        $dotenv->load();
    }
    ```

4. In `composer.json` file, move `vlucas/phpdotenv` from `require` to `require-dev` to continue using the `dotenv` package on your `local/dev` environment:

    ```php
    "require-dev": {
        "vlucas/phpdotenv": "^2.4",
    },
    ```

## Gandi