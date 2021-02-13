# apps

## Ubuntu

```shell
$ sudo apt-get install unzip build-essential
```

## [brew](https://brew.sh/)

```shell
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## [gh](https://github.com/cli/cli)

```shell
$ brew install gh
```

## [Snyk](https://snyk.io/)

```shell
$ sudo npm install -g snyk
$ snyk auth
```

## [nanorc](https://github.com/scopatz/nanorc)

```shell
$ wget https://raw.githubusercontent.com/scopatz/nanorc/master/install.sh -O- | sh
```

## [golang](https://golang.org/doc/install)

```shell
$ wget "https://dl.google.com/go/$(curl https://golang.org/VERSION?m=text).linux-amd64.tar.gz"
$ sudo tar -C /usr/local -xzf "go$(curl https://golang.org/VERSION?m=text).linux-amd64.tar.gz"
# ~/.bash_exports
$ export PATH=$PATH:/usr/local/go/bin
$ export GOROOT=/usr/local/go/
```

## Chromebook

```shell
$ curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-notify.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/notify && sudo chmod +x /usr/bin/notify
$ curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-show-file.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/show-file && sudo chmod +x /usr/bin/show-file
$ curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/osc52.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/copy && sudo chmod +x /usr/bin/copy
```
