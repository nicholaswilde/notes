# Docker

## Installation

```shell
wget -O - https://get.docker.com | sudo bash && sudo usermod -aG docker pi
```

## [qemu-user-static](https://github.com/multiarch/qemu-user-static)

```shell
$ uname -m
x86_64
$ docker run --rm -t arm64v8/ubuntu uname -m
standard_init_linux.go:211: exec user process caused "exec format error"
$ docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
$ docker run --rm -t arm64v8/ubuntu uname -m
aarch64
```

## Prune all

```shell
$ docker system prune --all
```

[ssh certs](https://curl.se/docs/caextract.html)
```shell
$ curl --remote-name --time-cond cacert.pem https://curl.se/ca/cacert.pem
```

## Shell

```shell
# Debian
$ docker exec -it <container name> /bin/bash
$ docker run -it --rm <image name> /bin/bash
# alpine
$ docker exec -it <container name> /bin/ash
$ docker run -it --rm alpine:3.13.1 <container name> /bin/ash
```

## Stop all containers

```shell
$ docker container stop $(docker container ls -aq)
```

## Remove all stopped containers

```shell
$ docker container rm $(docker container ls -aq)
```

## References

* [docker-template wiki](https://github.com/nicholaswilde/docker-template/wiki/)
