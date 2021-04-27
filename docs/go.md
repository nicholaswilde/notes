# go

## [Install](https://golang.org/doc/install)

Figure out how to deal with `armv6l` and `armv7l`.

```shell
(
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(armhf\)\(64\)\?.*/\1\2hf/' -e 's/aarch64$/arm64/')" && \
  VERSION="$(curl https://golang.org/VERSION?m=text)" && \
  wget "https://dl.google.com/go/${VERSION}.linux-${ARCH}.tar.gz" -O- | sudo tar -C /usr/local -xzf -
)
```

```shell
# ~/.bash_exports
export PATH=$PATH:/usr/local/go/bin
export GOROOT=/usr/local/go/
```

Clear the build cache

```shell
$ go clean -cache -modcache -i -r
```

Get go version

```shell
$ GO_VERSION=$(curl -sSL "https://golang.org/VERSION?m=text")
```
