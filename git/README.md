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
$ git config --global commit.gpgsign true
```

## Usage

### Switching Remote URLs

```shell
$ git remote -v
origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
origin  git@github.com:USERNAME/REPOSITORY.git (push)
$ git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

### [Syncing a Fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)

```shell
# Configuring a remote for a fork
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
$ git fetch upstream
$ git checkout main
$ git merge upstream/main
```

### [Different Path](https://git-scm.com/docs/git#Documentation/git.txt--Cltpathgt)

```shell
$ git -C <path>
```

### [Empty Message](https://stackoverflow.com/a/17365487/1061279)

```shell
$ git commit --allow-empty-message -m ''
```

## URLs

* Commit: https://github.com/python/cpython/archive/31af650.tar.gz
* Latest: https://github.com/USER/PROJECT/releases/latest/download/package.zip
* Release: https://github.com/$(IMAGE_NAME)/$(IMAGE_NAME)/releases/download/v${VERSION}/Leantime-v${VERSION}.tar.gz
* Release Source: https://github.com/nicholaswilde/helm-charts/archive/wikijs-0.1.6.tar.gz

## [gh](https://github.com/cli/cli)

```shell
$ brew install gh
$ gh auth login
```
