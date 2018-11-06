## Purpose ##

This repo contains the Json-LD schemas served by bioterms.org. It also includes a Dockerfile to create a Docker image running Apache2 web server serving these schemas.


## Contents ##

If you decide to build the Docker image and serve the contents as a Docker container, please edit the httpd.conf file found in the docker/apache_conf sub directory - make sure that the port and DNS name are correct, as the Apache web server is set up to use virtual hosts to run the website and serve the schemas.

The actual Json-LD schemas are in the docker/schemas sub directory.

## How to run the image ##

```
cd docker
docker build -t bioterms-docker-image .
docker run -dit -p 8889:80 -v "$PWD":/usr/local/apache2/htdocs/ bioterms-docker-image:latest
```

The above will expose port 8889 (which is what we use to serve the contents on). In our setup we use Traefik (https://traefik.io/) to run multiple domains on the same machine (episb.org, bioterms.org etc.), all as Docker images. Traefik will take care of all the port/DNS forwarding in this scenario.

## How to serve the contents without a Docker image ##

If you have a dedicated machine to run Apache and want to serve the contents, make use to use the included httpd.conf file - copy it into the appropriate Apache conf directory (e.g. /etc/httpd/conf or /usr/local/apache2/conf) and make sure to edit the file to reflect the correct DocumentRoot and ServerRoot directories. The schemas/ sub directory and its contents should be copied into /var/www/html (or /usr/local/apache2/htdocs, or wherever DocumentRoot is set to point). After starting Apache, it should serve all the schemas properly. Do not forget to comment out the VirtualHost section or change it to make it appropriate for your situation.
