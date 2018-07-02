# noVNC IPMI Container

This image deploys the bmc-support-old branch of a noVNC fork that supports
SuperMicro motherboard IPMI implementation.

## Image Contents

* [noVNC](https://github.com/kelleyk/noVNC) - a SuperMicro IPMI-compatible
  HTML5 VNC viewer

## Quickstart

    $ docker run --rm -it -p 8080:8080 kubao/novnc-ipmi --listen 8080 --vnc host:5600

Open a browser and navigate to `http://<CONTAINER_ADDRESS>:8080/vnc.html`. The
host you are connecting to is *not* the VNC host, but the websocket host. By
default, this won't be useful to connect to non-websocket VNC host: the
websockify running in the container only allows connections to localhost by
default. See the following section for how to set VNC hosts to connect to.

## Accessing the Web Server

On Mac, the container's IP addresses are not routed by default. Instead, Docker
exposes the ports passed to `-p` as ports on localhost. Thus,
`CONTAINER_ADDRESS` is simply `localhost`.

 See also https://docs.docker.com/docker-for-mac/networking/#there-is-no-docker0-bridge-on-macos

On Linux, the container has an individual IP address, available via:

    $ docker ps      # To get a list of running containers 
    $ docker inspect <CONTAINER_ID>
    ...
        "NetworkSettings": {
            "Bridge": "",
           [...
            "Ports": {
                "8080/tcp": [
                    ...
                ]
            },
            "Gateway": "172.17.0.1",
            "IPAddress": "172.17.0.2",
    ...

## Target Hosts

The arguments passed to the `docker run` command after the image name are
passed to the launch script (`noVNC/utils/launch.sh`). Thus, `--vnc host:port`
connects to the given SuperMicro host and port. At the moment, only one host is
supported. To connect to more hosts, start multiple instances of the container.
