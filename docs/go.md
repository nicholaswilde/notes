# go

## [Install](https://golang.org/doc/install)

Figure out how to deal with `armv6l` and `armv7l`.

```shell
(
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(armhf\)\(64\)\?.*/\1\2hf/' -e 's/aarch64$/arm64/')" && \
  VERSION="$(curl https://go.dev/VERSION?m=text)" && \
  wget "https://dl.google.com/go/${VERSION}.linux-${ARCH}.tar.gz" -O- | sudo tar -C /usr/local -xzf -
)
```

```shell
# ~/.bash_exports
export PATH=$PATH:/usr/local/go/bin
export GOROOT=/usr/local/go/
```

## Clear the build cache

```shell
$ go clean -cache -modcache -i -r
```

## Get go version

```shell
$ GO_VERSION=$(curl -sSL "https://go.dev/VERSION?m=text")
```

## [Init][1]

```shell
go mod init project-name
go mod tidy
go run ./...
```

## Templates

- <https://docs.gomplate.ca/>

[1]: <https://stackoverflow.com/a/73966761>
