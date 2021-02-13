# [pass](https://www.passwordstore.org/)

## Reconnecting Existing Repo

```shell
$ git clone git@github.com:nicholaswilde/pass.git ~/.password-store
```

## [pass-git-helper](https://github.com/languitar/pass-git-helper)

```shell
$ sudo apt install pass-git-helper
$ git config --global credential.helper /usr/bin/pass-git-helper
$ git config --global credential.useHttpPath true
```

## [pass-import](https://github.com/roddhjav/pass-import)

```shell
$ wget -qO - https://pkg.pujol.io/debian/gpgkey | sudo apt-key add -
$ echo 'deb [arch=amd64] https://pkg.pujol.io/debian/repo all main' | sudo tee /etc/apt/sources.list.d/pkg.pujol.io.list
$ sudo apt-get update
$ sudo apt-get install pass-extension-import
```

## References

* https://wiki.archlinux.org/index.php/Pass
