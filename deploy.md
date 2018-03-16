# Deploy

## VPS

On VPS like DigitalOcean, Linode... that uses Ubuntu.

### Install dependencies using Composer

```bash
composer install --no-dev
```

### Create vhost on Nginx

#### HTTP

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name example.com;

    root /var/www/example;

    index index.php index.html index.htm;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
            expires 14d;
    }

}
```

#### HTTPS

```nginx
server {
        listen 443 ssl http2;
        listen [::]:443 ssl http2;

        server_name example.com;

        root /var/www/example;

        index index.php index.html index.htm;

        ssl on;
        include snippets/ssl-example.com.conf;
        include snippets/ssl-params.conf;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }

        location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
                expires 14d;
        }

}
```

Add redirection for http:

```nginx
server {
        listen 80;
        server_name mondialrelay-woocommerce.com;
        return 301 https://www.$server_name$request_uri;
}
```

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

### Skeleton

Rename `public` folder to `htdocs`.

### Basic authentification

Add `environnement` in the basic auth middleware:

```php
$app->add(new \Slim\Middleware\HttpBasicAuthentication([
    ...
    "environment" => "REDIRECT_HTTP_AUTHORIZATION"
]));
```