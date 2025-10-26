---
tags:
  - linux
---
# :key: GPG

## :material-key-plus: Generate Key

```shell
gpg --full-generate-key
```

## :material-import: Import

```shell
lpass show gpg --attach=8017296795546256342-55097 -q | gpg --import
```

```shell
gpg --import secret.asc
```

## Trust Own Key

```shell
# https://unix.stackexchange.com/a/407070/93726
gpg --edit-key user@useremail.com

gpg> trust

Please decide how far you trust this user to correctly verify other users' keys
(by looking at passports, checking fingerprints from different sources, etc.)

  1 = I don't know or won't say
  2 = I do NOT trust
  3 = I trust marginally
  4 = I trust fully
  5 = I trust ultimately
  m = back to the main menu

Your decision? 5
gpg> save
```

## :pen_fountain: Sign Others' Keys

```shell
wget http://example.com/pgp-public-key -O- | gpg --import
gpg -k
gpg --sign-key theirs@email.com
```

## :fontawesome-solid-list: List

```shell
# Secret keys
gpg -K --keyid-format LONG
# All keys
gpg -k --keyid-format LONG
```

## Submit to Keyserver

```shell
gpg --keyid-format LONG --list-keys john@example.com
pub   rsa4096/ABCDEF0123456789 2018-01-01 [SCEA] [expires: 2021-01-01]
      ABCDEF0123456789ABCDEF0123456789
uid              [ ultimate ] John Doe
gpg --keyserver keyserver.ubuntu.com --send-keys ABCDEF0123456789
```

## Revokation Certificate

```shell
gpg --output revoke.asc --gen-revoke you@example.com
```

## Export

```shell
gpg --export-secret-keys --armor $EMAIL > /path/to/secret-key-backup.asc
gpg --export --armor $EMAIL > /path/to/public-key-backup.asc
```

## Keygrip to match `*.key` filenames in `~/.gnupg/private-keys-v1.d` directory

```shell
gpg -K --with-keygrip
gpg -k --with-keygrip
```

## Get Key ID

```shell
key=$(gpg -k --with-colons "noreply@email.com" | awk -F: '/^pub:/ { print $5 }') && echo "0x"${key:(-8)}
# 0x08B7D7A3
```

## [Restart Agent on Windows][1]

```PowerShell
gpg-connect-agent reloadagent /bye
```

## Refresh Keys

```shell
gpg --refresh-keys --keyserver keyserver.ubuntu.com
```

## Pinentry Mode

```shell
gpg --pinentry-mode loopback --import <file>.asc
```

## Validity Unknown

```shell
gpg --check-trustdb
gpg --update-trustdb
```

## Show Subkey Fingerprints

```shell
gpg -K --with-subkey-fingerprints
```

## Unlock Key

To manually force a passphrase prompt and "unlock" the key, you can run a simple GPG command that requires it, such as:

```shell
gpg -s
```

This command initiates a signature process on standard input. It will prompt you to type some text and then ask for your passphrase to sign it. Once you've entered the passphrase, you can press Ctrl+D twice to exit the command. Your key will then be unlocked and cached by gpg-agent.

Type something.

## References

- <https://ruimarinho.gitbooks.io/yubikey-handbook/content/openpgp/troubleshooting/gpg-failed-to-sign-the-data.html>
- <https://devhints.io/gnupg>

[1]: https://superuser.com/a/1663941/352242
