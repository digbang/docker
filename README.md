# Digbang Docker
Docker images for Digbang PHP projects

## Usage
Images extend php-apache so that webserver is already embedded on the container.

## Updates

1. Change the `.template` files.
2. Run the `build` command.
3. Run `docker pull php:<version>-apache` (example: `docker pull php:7.4-apache`) on each of the versions you want to rebuild.
4. Run `docker-compose up -d --build php` on each modified directory (First `php`, then `php-dev`).
5. Run `docker commit <container> digbang/php:<version>` (example: `docker commit 74_php_1 digbang/php:7.4`).
6. Run `docker commit <container> digbang/php-dev:<version>` (example: `docker commit 74_php_1 digbang/php-dev:7.4`).
7. Run `docker push digbang/php:<version>` and/or `docker push digbang/php-dev:<version>` for each of the commits.


### Dev environments
Use docker-compose in dev environments:

```
services:
  php:
    image: digbang/php-dev:7.4
    volumes:
      - .:/var/www/html
      - ./docker/apache:/etc/apache2/sites-enabled:ro
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
> Remember to add the new version to the build command.
