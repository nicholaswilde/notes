# GPG

## Generate Key

```shell
gpg --full-generate-key
```

## Import

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

## Sign Others' Keys

```shell
wget http://example.com/pgp-public-key -O- | gpg --import
gpg --list-keys
gpg --sign-key theirs@email.com
```

## List

```shell
# Secret keys
gpg --list-secret-keys --keyid-format LONG
# All keys
gpg --list-keys --keyid-format LONG
```

## Submit to Keyserver

```shell
gpg --keyid-format LONG --list-keys john@example.com
pub   rsa4096/ABCDEF0123456789 2018-01-01 [SCEA] [expires: 2021-01-01]
      ABCDEF0123456789ABCDEF0123456789
uid              [ ultimate ] John Doe
gpg --keyserver pgp.mit.edu --send-keys ABCDEF0123456789
```

## Revokation Certificate

```shell
gpg --output revoke.asc --gen-revoke you@example.com
```

## Export

```shell
gpg --export-secret-keys --armor my@email.com > /path/to/secret-key-backup.asc
```

## Keygrip to match `*.key` filenames in `~/.gnupg/private-keys-v1.d` directory

```shell
gpg --list-secret-keys --with-keygrip
gpg --list-keys --with-keygrip
```
