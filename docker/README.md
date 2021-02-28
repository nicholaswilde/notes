# Docker

## Installation

```shell
$ wget -O - https://get.docker.com | sudo bash && sudo usermod -aG docker pi
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

## [buildx](https://github.com/docker/buildx#binary-release)

```shell
$ mkdir ~/.docker/cli-plugins
$ wget https://github.com/docker/buildx/releases/download/v0.5.1/buildx-v0.5.1.linux-amd64 -O ~/.docker/cli-plugins/docker-buildx
$ chmod a+x ~/.docker/cli-plugins/docker-buildx
# Set buildx as default
$ docker buildx install
# Create builder
$ docker buildx create --name mybuilder
# Switch to the new builder
$ docker buildx use mybuilder
# Inspect it
$ docker buildx inspect --bootstrap
```

## Prune all

```shell
$ docker system prune --all
```


## [ssh certs](https://curl.se/docs/caextract.html)
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

## Copy Multiple Files

```dockerfile
COPY ["__BUILD_NUMBER", "README.md", "gulpfile", "another_file", "./"]
```

## docker-compose

```script
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

## [hadolint](https://github.com/hadolint/hadolint)

```shell
$ brew install hadolint
```
## Pull by Digest

```shell
$ docker run -it --rm python:3.7.10-slim-buster@sha256:482d4cc1ae3c95d0f4dd25005e22a17f22f693ca7fb07bb7870ff9354844f738 /bin/bash
```

## Run on Current Directory

```shell
$ docker run --rm -it -v $(pwd):/charts --entrypoint "/bin/bash" -w /charts k8s-at-home/charts-unit-test -l -c "bundle exec m -r ./test/charts"
```

## References

* [docker-template wiki](https://github.com/nicholaswilde/docker-template/wiki/)
* https://docs.docker.com/docker-for-mac/multi-arch/
* https://github.com/docker/buildx#binary-release
* https://docs.docker.com/buildx/working-with-buildx/
