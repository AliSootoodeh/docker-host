# docker-host
Docker image to forward all traffic to the docker host

[![Build Status](https://travis-ci.org/qoomon/docker-host.svg?branch=master)](https://travis-ci.org/qoomon/docker-host)
[![Docker Stars](https://img.shields.io/docker/pulls/qoomon/docker-host.svg)](https://hub.docker.com/r/qoomon/docker-host/)

## Enironment Variables
`PORTS` a comma seperated list of ports and port ranges, **default**: 0:65535 

# Docker Run Example
```docker run -it --rm --name dockerhost --cap-add=NET_ADMIN --cap-add=NET_RAW -e PORTS=0:1024,9000 qoomon/docker-host```

```docker run --rm -it --link dockerhost bash ping dockerhost```

# Docker Compose Example
```yaml
version: '2'

services:
    dockerhost:
        image: qoomon/docker-host
        cap_add: [ 'NET_ADMIN', 'NET_RAW' ]
        mem_limit: 4M
        restart: on-failure
        environment:
          - PORTS=0:1024,9000

    dummy:
        image: bash
        command: ["ping" , "dockerhost"]
```
