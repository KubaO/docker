# Centos 7 Foreman Container

This image deploys the Centos-7-based, systemd-enabled current version of
Foreman. It breaks the composition model of docker, unfortunately. You'd
want to use [foreman-docker-compose](https://github.com/shlomizadok/foreman-docker-compose)
instead.

## Compose Quickstart

    $ docker-compose build foreman
    $ docker-compose run --service-ports foreman

## Direct Quickstart

    $ docker build .
    $ docker run --rm -Pit --hostname c7-foreman.local --tmpfs /run --cap-add SYS_ADMIN .

## Notes

Connect to https://localhost:9443 to access the web ui.

This will run the docker installer first, but all the packages should be already downloaded - so
it will be quick-ish.