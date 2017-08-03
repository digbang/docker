# Digbang Docker
Docker images for Digbang PHP projects

## Usage
Images extend php-apache so that webserver is already embedded on the container.

### Dev environments
Use docker-compose in dev environments:

```
services:
  php:
    image: digbang/php-dev:7.1
    volumes:
      - .:/var/www/html
      - ./docker/apache:/etc/apache2/sites-enabled:ro
      - ./docker/php/custom.ini:/usr/local/etc/php/conf.d/custom.ini:ro
    ports:
      - "80:80"
```

Mounted volumes correspond to code, apache vitualhost configurations and custom php.ini configurations. Both apache and php configurations are optional.
Check provided extensions on the Dockerfile.

### Live environments
The digbang/php image does not include debugging tools or composer, which makes it more suitable for live environments.

> This image has not been used in live deployments yet! Use at your own risk.

## Contributing
This repository has 2 `Dockerfile.template` files, one for the `digbang/php` image and one for the `digbang/php-dev` image, that extends the former.
To edit this images, *always edit the template file* and run `./build` to generate a `Dockerfile` for each PHP version supported.

