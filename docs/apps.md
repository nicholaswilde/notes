# Apps

## Ubuntu

```shell
sudo apt-get install unzip build-essential
```

## [brew](https://brew.sh/)

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## [gh](https://github.com/cli/cli)

```shell
brew install gh
```

## [Snyk](https://snyk.io/)

```shell
sudo npm install -g snyk
snyk auth
```

## [nanorc](https://github.com/scopatz/nanorc)

```shell
wget https://raw.githubusercontent.com/scopatz/nanorc/master/install.sh -O- | sh
```

```shell
echo "set tabsize 2" >> ~/.nanorc
echo "set tabstospaces" >> ~/.nanorc
```

## [Chromebook](https://chromium.googlesource.com/apps/libapps/+/hterm-1.80/nassh/doc/FAQ.md#How-do-I-copy-text-from-the-terminal)

```shell
curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-notify.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/notify && sudo chmod +x /usr/bin/notify
curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-show-file.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/show-file && sudo chmod +x /usr/bin/show-file
curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/osc52.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/copy && sudo chmod +x /usr/bin/copy
```

## [semver](https://github.com/fsaintjacques/semver-tool)

```shell
sudo wget -O /usr/bin/semver https://github.com/fsaintjacques/semver-tool/raw/master/src/semver
sudo chmod +x /usr/bin/semver
```

## [pre-commit](https://pre-commit.com/#install)

```shell
brew install pre-commit
```
