# Git

## gpg

[Telling Git about your signing key](https://docs.github.com/en/github/authenticating-to-github/telling-git-about-your-signing-key)

## Configure

```shell
$ git config --global user.email "ncwilde43@gmail.com"
$ git config --global user.name "Nicholas Wilde"
$ git config credential.helper store
$ git config --global init.defaultBranch main
$ git config --global user.signingkey <gpg key fingerprint>
```

## Switching Remote URLs

```shell
$ git remote -v
origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
origin  git@github.com:USERNAME/REPOSITORY.git (push)
$ git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```
