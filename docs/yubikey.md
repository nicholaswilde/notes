# Yubikey

## [Installation][1]

```shell title="Ubuntu"
sudo apt install pcscd scdaemon
brew install ykman
```

```PowerShell title="Windows 11"
winget install Yubico.YubikeyManager
```

Add Yubico Manager program location to `PATH`.

`C:\Program Files\Yubico\YubiKey Manager`

## Card Status

```
gpg --card-status
```

## Metadata

```
gpg --card-edit
gpg/card> name
```

## References

- <https://ruimarinho.gitbooks.io/yubikey-handbook/content/>
- <https://github.com/drduh/YubiKey-Guide/blob/master/README.md>

[1]: https://docs.yubico.com/software/yubikey/tools/ykman/Install_ykman.html
