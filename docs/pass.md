# [pass](https://www.passwordstore.org/)

## Installation

```shell
# Ubuntu
brew install pass
```

Remove gpg-agent error

```shell
sudo apt remove gpg-agent
gpgconf --kill gpg-agent
```

## Usage

### [Import File](https://lists.zx2c4.com/pipermail/password-store/2014-August/001105.html)

```shell
pass insert -fm gpg/revoke < file.txt
```

### Git

```shell
# Push your local pass history
pass git push -u --all
```

## Reconnecting Existing Repo

```shell
git clone git@github.com:nicholaswilde/pass.git ~/.password-store
```

## [pass-import](https://github.com/roddhjav/pass-import)

```shell
wget -qO - https://pkg.pujol.io/debian/gpgkey | sudo apt-key add -
echo 'deb [arch=amd64] https://pkg.pujol.io/debian/repo all main' | sudo tee /etc/apt/sources.list.d/pkg.pujol.io.list
sudo apt-get update
sudo apt-get install pass-extension-import
```

## References

* https://wiki.archlinux.org/index.php/Pass
