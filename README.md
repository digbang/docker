# Digbang Docker
Docker images for Digbang PHP projects.

## Usage
We highly recommend reviewing the examples found in the **examples** directory of this repository to facilitate implementation. While specifically crafted for Laravel applications, these examples are easily adaptable.

## Building images based on PHP-Apache
As a reference, and using PHP 8.3 as an example, when mentioning:

`<container>` is equals to **83-apache-php-1**

`<version>` is equals to **8.3-apache**

### Instructions

1. Include the corresponding `<version>` in the **versions.txt** file.
2. the `./build` command.
3. `docker pull php:<version>` on each of the versions you want to rebuild.
4. `docker-compose up -d --build php`. First in the **php** directory, then in **php-dev** directory.
5. `docker commit <container> digbang/php:<version>`.
6. `docker push digbang/php:<version>`.
7. `docker commit <container> digbang/php-dev:<version>`.
8. `docker push digbang/php-dev:<version>`.

## Building images based on PHP-FPM
As a reference, and using PHP 8.3 as an example, when mentioning:

`<container>` is equals to **83-fpm-php-1**

`<version>` is equals to **8.3-fpm**

### Instructions

1. Include the corresponding `<version>` in the **versions.txt** file.
1. the `./build` command.
2. `docker pull php:<version>` on each of the versions you want to rebuild.
3. `docker-compose up -d --build php`. First in the **php** directory, then in **php-dev** directory.
4. `docker commit <container> digbang/php:<version>`.
5. `docker push digbang/php:<version>`.
6. `docker commit <container> digbang/php-dev:<version>`.
7. `docker push digbang/php-dev:<version>`.

## Disclaimer regarding production environments.
The **digbang/php** images do not include debugging tools or Composer, making them more suitable for production environments.

> Cautiously note that this image has not yet been utilized in live deployments. Proceed with caution and use at your own risk.