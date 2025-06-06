# :simple-docker: Docker

## Installation

```shell
(
  set -x; sudo apt-get update &&
  sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release &&
  DIST=$(lsb_release -is | tr '[:upper:]' '[:lower:]') &&
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(armhf\)\(64\)\?.*/\1\2hf/' -e 's/aarch64$/arm64/')" &&
  curl -fsSL "https://download.docker.com/linux/${DIST}/gpg" | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg &&
  echo "deb [arch=${ARCH} signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/${DIST} $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt update &&
  sudo apt install -y docker-ce docker-ce-cli containerd.io &&
  sudo usermod -aG docker $(whoami)
  newgrp docker
)
```

## Test that sudo is not needed

```shell
docker run --rm hello-world
```

## [qemu-user-static](https://github.com/multiarch/qemu-user-static)

```shell
uname -m
# x86_64
docker run --rm -t arm64v8/ubuntu uname -m
# standard_init_linux.go:211: exec user process caused "exec format error"
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
docker run --rm -t arm64v8/ubuntu uname -m
# aarch64
```

## [buildx](https://github.com/docker/buildx#binary-release)

```shell
mkdir ~/.docker/cli-plugins
wget https://github.com/docker/buildx/releases/download/v0.5.1/buildx-v0.5.1.linux-amd64 -O ~/.docker/cli-plugins/docker-buildx
chmod a+x ~/.docker/cli-plugins/docker-buildx
# Set buildx as default
docker buildx install
# Create builder
docker buildx create --name mybuilder
# Switch to the new builder
docker buildx use mybuilder
# Inspect it
docker buildx inspect --bootstrap
```

## Prune all

```shell
docker system prune --all
```


## [ssh certs](https://curl.se/docs/caextract.html)
```shell
curl --remote-name --time-cond cacert.pem https://curl.se/ca/cacert.pem
```

## Shell

```shell
# Debian
docker exec -it <container name> /bin/bash
docker run -it --rm <image name> /bin/bash
# alpine
docker exec -it <container name> /bin/ash
docker run -it --rm alpine:3.13.1 <container name> /bin/ash
```

## Stop all containers

```shell
docker container stop $(docker container ls -aq)
```

## Remove all stopped containers

```shell
docker container rm $(docker container ls -aq)
```

## To delete all containers including its volumes

```shell
docker rm -vf $(docker ps -a -q)
```

## To delete all the images,

```shell
docker rmi -f $(docker images -a -q)
```

Remember, you should remove all the containers before removing all the images from which those containers were created.

## Copy Multiple Files

```dockerfile
COPY ["__BUILD_NUMBER", "README.md", "gulpfile", "another_file", "./"]
```

## docker-compose

```script
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## [hadolint](https://github.com/hadolint/hadolint)

```shell
$ brew install hadolint
```
## Pull by Digest

```shell
docker run -it --rm python:3.7.10-slim-buster@sha256:482d4cc1ae3c95d0f4dd25005e22a17f22f693ca7fb07bb7870ff9354844f738 /bin/bash
```

## Run on Current Directory

```shell
docker run --rm -it -v $(pwd):/charts --entrypoint "/bin/bash" -w /charts k8s-at-home/charts-unit-test -l -c "bundle exec m -r ./test/charts"
```

## [Check if Image Exists](https://stackoverflow.com/a/33061675/1061279)

```shell
docker inspect --type=image treeder/hello.rb:nada
Error: No such image: treeder/hello.rb:nada
[]
```

## Insecure Registries

```shell
sudo nano /etc/docker/daemon.json
```

```json
{
  "insecure-registries" : ["registry.192.168.1.201.nip.io"]
  "insecure-registries" : ["registry.192.168.1.202.nip.io"]
  "insecure-registries" : ["registry.192.168.1.203.nip.io"]
  "insecure-registries" : ["registry.192.168.1.204.nip.io"]
  "insecure-registries" : ["registry.192.168.1.205.nip.io"]
  "insecure-registries" : ["registry.192.168.1.206.nip.io"]
  "insecure-registries" : ["registry.192.168.1.207.nip.io"]
}
```

## References

* [docker-template wiki](https://github.com/nicholaswilde/docker-template/wiki/)
* [https://docs.docker.com/docker-for-mac/multi-arch/](https://docs.docker.com/docker-for-mac/multi-arch/)
* [https://github.com/docker/buildx#binary-release](https://github.com/docker/buildx#binary-release)
* [https://docs.docker.com/buildx/working-with-buildx/](https://docs.docker.com/buildx/working-with-buildx/)
