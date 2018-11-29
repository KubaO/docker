# Centos 7 Foreman Container

This image deploys the Centos-7-based, systemd-enabled current version of
Foreman. It breaks the composition model of docker, unfortunately. You'd
want to use [foreman-docker-compose](https://github.com/shlomizadok/foreman-docker-compose)
instead.

## Compose Quickstart

    $ docker-compose build foreman
    $ docker-compose run foreman

## Direct Quickstart

    $ docker build .
    $ docker run --rm -it --hostname c7-foreman.local --tmpfs /run --cap-add SYS_ADMIN .

## Notes

This will run the docker installer first :/.