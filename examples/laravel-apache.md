# A Laravel example using the Apache version.

1. Create a file named **docker-compose.yml** in the root directory.
```
version: '3'

services:
  php:
    image: digbang/php-dev:8.3-apache
    ports:
      - "8000:80"
    volumes:
      - .:/var/www/html
      - ./docker/apache:/etc/apache2/sites-enabled:ro
```

2. Then, create a file named **docker/apache/default.conf**.
```
<VirtualHost *:80>
    ServerName _
    DocumentRoot /var/www/html/public

    <Directory "/var/www/html/public">
        Options Indexes FollowSymlinks MultiViews
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>

    <IfModule mod_rewrite.c>
        RewriteEngine On

        RewriteRule ^(.+[^/])/$ $1 [R=301,L]

        RewriteCond %{DOCUMENT_ROOT}%{REQUEST_URI} !-d
        RewriteCond %{DOCUMENT_ROOT}%{REQUEST_URI} !-f
        RewriteRule . /index.php [L]
    </IfModule>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    ServerSignature Off

    SetEnv APP_ENV local
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

3. Build the container using `docker-compose up -d --build`. The `-d` flag is to run it in detached mode.

4. You can now access the site hosted at http://localhost:8000.