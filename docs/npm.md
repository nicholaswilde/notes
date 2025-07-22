# :simple-npm: npm

## :hammer_and_wrench: Installation

```shell
sudo apt install build-essential libssl-dev curl git-core
```

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/$(curl -s "https://api.github.com/repos/nvm-sh/nvm/releases/latest" | grep '"tag_name":' | cut -d'"' -f4)/install.sh | bash
```

```shell
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

```shell title="Install node"
nvm install node
```

## [Update](https://flaviocopes.com/update-npm-dependencies/) `packages.json`

```shell
sudo npm install -g npm-check-updates
ncu -u
```
