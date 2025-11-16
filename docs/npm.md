# :simple-npm: npm

## :hammer_and_wrench: Installation

!!! code ""

    ```shell
    (
      sudo apt install build-essential libssl-dev curl git-core
      curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/$(curl -s "https://api.github.com/repos/nvm-sh/nvm/releases/latest" | grep '"tag_name":' | cut -d'"' -f4)/install.sh | bash && \
      export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" && \
      [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm && \
      nvm install node
    )
    ```

## [Update](https://flaviocopes.com/update-npm-dependencies/) `packages.json`

```shell
sudo npm install -g npm-check-updates
ncu -u
```

## [Update Node][1]

```shell title="set latest Version as default with this command"
nvm alias default node
```

```shell title="now you can update npm with this command"
npm install -g npm
```

## Correct app version not running fix

```
hash -r
```

[1]: <https://stackoverflow.com/a/76934903/1061279>
