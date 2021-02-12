# GPG

## Import
```bash
$ gpg --import secret.asc
```

## Trust
```bash
# https://unix.stackexchange.com/a/407070/93726
$ gpg --edit-key user@useremail.com

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
