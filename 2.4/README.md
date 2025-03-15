# Alpine Apache HTTPd 2.4

[![Build Status][ico-ghactions]][link-ghactions]
[![Docker Pull][ico-docker]][link-docker]
[![Latest Version][ico-version]][link-docker]
[![Software License][ico-license]](LICENSE)

An Apache HTTPd 2.4 image forked from the official [repository](https://store.docker.com/images/httpd).

With configuration:

* [Deflate](https://github.com/llaumgui/docker-images-httpd/tree/master/2.4/conf.d/deflate.conf).
* [ETags](https://github.com/llaumgui/docker-images-httpd/tree/master/2.4/conf.d/etags.conf).
* [Expires](https://github.com/llaumgui/docker-images-httpd/tree/master/2.4/conf.d/expires.conf).
* [Security](https://github.com/llaumgui/docker-images-httpd/tree/master/2.4/conf.d/security.conf).
* SSL support.
* You can put your vhost in _/usr/local/apache2/conf/vhost.d_ (This directory can be shared with the Docker host).

Works also with:

* [PHP-FPM](https://github.com/llaumgui/docker-images-httpd/tree/master/2.4/conf.d/php.conf) handler toward the _php_ hostname.

**Allow environment variables `PUID` and `PGID` to change the user which executes the HTTP process.**

## Usage

### With Docker client

You can run this container with the Docker client:

~~~bash
docker run -d \
  --volume /docker/volumes/www:/var/www \
  --volume /docker/volumes/httpd24/conf/vhost.d:/usr/local/apache2/conf/vhost.d:ro \
  --volume /docker/volumes/httpd24/conf/ssl:/usr/local/apache2/conf/ssl:ro \
  -p 80:80 \
  -p 443:443 \
  llaumgui/httpd24
~~~

### With Compose

You can use this container in a docker-compose.yml file:

~~~yaml
  httpd:
    container_name: httpd
    image: llaumgui/httpd24
    restart: always
    environment:
      TZ: 'Europe/Paris'
      PUID: 82
      PGID: 82
    volumes:
     - /docker/volumes/www:/var/www/
     - /docker/volumes/httpd24/conf/vhost.d:/usr/local/apache2/conf/vhost.d:ro
     - /docker/volumes/httpd24/conf/ssl:/usr/local/apache2/conf/ssl:ro
    ports:
     - "80:80"
     - "443:443"
~~~

### Environment Variables

| Variable | Description                                | Default Value |
|----------|--------------------------------------------|---------------|
| `TZ`     | Timezone configuration.                    | N/A           |
| `PUID`   | User ID for the httpd process (www-data).  | `82`          |
| `PGID`   | Group ID for the httpd process (www-data). | `82`          |

[ico-docker]: https://img.shields.io/docker/pulls/llaumgui/httpd?color=%2496ed&logo=docker&style=flat-square
[link-docker]: https://hub.docker.com/r/llaumgui/httpd
[ico-ghactions]: https://img.shields.io/github/actions/workflow/status/llaumgui/docker-images-httpd/devops.yml?style=flat-square&logo=github&label=CI/CD
[link-ghactions]: https://github.com/llaumgui/docker-images-httpd/actions
[ico-version]: https://img.shields.io/docker/v/llaumgui/httpd?sort=semver&color=%2496ed&logo=docker&style=flat-square
[ico-license]: https://img.shields.io/github/license/llaumgui/docker-images-httpd?style=flat-square
