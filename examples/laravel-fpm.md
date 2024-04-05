# A Laravel example using the FPM version.

1. Create a file named **docker-compose.yml** in the root directory.
```
version: '3'

services:
  php:
    image: digbang/php-dev:8.3-fpm
    volumes:
      - .:/var/www/html

  nginx:
    image: nginx:latest
    ports:
      - "8000:80"
    volumes:
      - .:/var/www/html
      - ./docker/nginx/conf.d/:/etc/nginx/conf.d/:ro
    depends_on:
      - php
```

2. Then, create a file named **docker/nginx/conf.d/default.conf**.
```
server {
    listen 80;
    server_name localhost;
    root /var/www/html/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass php:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }
}
```

3. Build the container using `docker-compose up -d --build`. The `-d` flag is to run it in detached mode.

4. You can now access the site hosted at http://localhost:8000.