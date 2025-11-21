---
tags:
  - linux
---
# :simple-git: Git

## :material-key: gpg

[Telling Git about your signing key](https://docs.github.com/en/github/authenticating-to-github/telling-git-about-your-signing-key)

## :material-cog: Configure

```shell
(
  git config --global user.email "ncwilde43@gmail.com"
  git config --global user.name "nιcнolaѕ wιlde"
  git config --global init.defaultBranch main
  git config --global user.signingkey 69FF3D02ABFCD01F328778D5374FA199233281E4
  git config --global commit.gpgsign true
  git config --global pull.rebase false
)
```

## :material-hammer-wrench: Usage

### :octicons-arrow-switch-24: Switching Remote URLs

```shell
git remote -v
origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
origin  git@github.com:USERNAME/REPOSITORY.git (push)
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

### :material-source-branch-sync: [Syncing a Fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)

```shell
# Configuring a remote for a fork if it doesn't already exist
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
git fetch upstream
git checkout main
git merge upstream/main
# Push the changes
git push origin main
```

### [Edit Remote Branch](https://stackoverflow.com/a/1783426/1061279)

In both cases, start by fetching from the remote repository to make sure you have all the latest changes downloaded.

```shell
git fetch origin branch-name
```

This will fetch all of the remote branches for you. You can see the branches available for checkout with:

```shell
git branch -v -a
...
remotes/origin/test
```

The branches that start with remotes/* can be thought of as read only copies of the remote branches. To work on a
branch you need to create a local branch from it. This is done with the Git command switch (since Git 2.23) by
giving it the name of the remote branch (minus the remote name):

```shell
git switch test
```

In this case Git is guessing (can be disabled with --no-guess) that you are trying to checkout and track the remote branch with the same name.

### [Different Path](https://git-scm.com/docs/git#Documentation/git.txt--Cltpathgt)

```shell
git -C <path>
```

### [Empty Message](https://stackoverflow.com/a/17365487/1061279)

```shell
git commit --allow-empty-message -m ''
```

### Change a Commit Message

```shell
git commit --amend
```

### List Commits

```shell
git log
```

### URLs

* Commit: https://github.com/python/cpython/archive/31af650.tar.gz

* Release Source: https://github.com/nicholaswilde/helm-charts/archive/wikijs-0.1.6.tar.gz

### [gh](https://github.com/cli/cli)

```shell
brew install gh
gh auth login
```

### No Message

```shell
git commit --allow-empty-message -a -m ""
```

### [Synchronizing a local Git repository with a remote one](https://stackoverflow.com/a/15124916/1061279)

```shell
git fetch --prune
# https://stackoverflow.com/a/17029936/1061279
git branch -r | awk '{print $1}' | egrep -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk '{print $1}' | xargs git branch -d
```

### [Deleting Remote Branch](https://www.git-tower.com/learn/git/faq/delete-remote-branch/)

```shell
git branch -d <branch name>
git push origin --delete <branch name>
```

### Rename Branch

```shell
git branch -m <new branch name>
```

### [Restore a File From Remote](https://stackoverflow.com/a/58019011/1061279)

```shell
git fetch
git restore -s origin/main -- path/to/file
```

### Reset last commit

```shell
git reset --hard HEAD^
```

### Reset last two commits

```shell
git reset --hard HEAD~2
```

### Delete Github Tag

```shell
git push --delete origin <tag name>
```

### Unstage file that has been added but not commited

```shell
git restore --staged <file name>
```

## Get Latest Version

Strips `v` and `release` prefixes

```shell
curl -sX GET "https://api.github.com/repos/Jackett/Jackett/releases/latest" | jq --raw-output '.tag_name'
version="${version#*v}"
version="${version#*release-}"
```

## Get Latest Commit

Get's the first 7 characters of commit.

```shell
curl -sX GET https://api.github.com/repos/seejohnrun/haste-server/commits/master | jq --raw-output '. | .sha'
version="${version#*v}"
version="${version#*release-}"
version="${version:0:7}"
```

## [Ignore Modified Files][2]

```shell
# dir
git update-index --assume-unchanged dir-im-removing/
# or a specific file
git update-index --assume-unchanged config/database.yml
# To get undo/show dir's/files that are set to assume-unchanged run this:
git update-index --no-assume-unchanged <file>
# To get a list of dir's/files that are assume-unchanged run this:
git ls-files -v|grep '^h'
```

## [Push Tags][1]

```shell
git tag
git tag v0.4.0
git push origin v0.4.0
```

## [Push commit and tags at the same time][4]

```shell
git push --atomic origin main v0.4.0
```

## [Compare Two Branches][3]

```shell
git diff branch1..branch2
```

![double-dot](https://devconnected.com/wp-content/uploads/2019/11/git-diff-double-dot.png)

```shell
git diff branch1...branch2
```

![triple-dot](https://devconnected.com/wp-content/uploads/2019/11/triple-dot.png)

## [Add File After Commit][5]

```
git add the_left_out_file
git commit --amend --no-edit
```

## Use a Specific SSH Key

### One Time Use

```
git -c "core.sshCommand=ssh -i ~/.ssh/id_ed25519" clone git@github.com:nicholaswilde/dotfiles.git
```

### Global Config

```
git config --global core.sshCommand "ssh -i ~/.ssh/id_ed25519"
```

## References

* [Cheat Sheet](https://github.com/tiimgreen/github-cheat-sheet)
* [GitHub Flavored Markdown](https://github.github.com/gfm/)
- [On undoing, fixing, or removing commits in git](https://sethrobertson.github.io/GitFixUm/fixup.html)
- [Convential Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [Amending a Commit Guide](https://github.com/RichardLitt/knowledge/blob/master/github/amending-a-commit-guide.md)

[1]: <https://stackoverflow.com/a/5195913>
[2]: <https://stackoverflow.com/a/761116>
[3]: <https://www.atlassian.com/git/tutorials/comparing-workflows/git-diff>
[4]: <https://stackoverflow.com/a/3745250/1061279>
[5]: <https://stackoverflow.com/a/40503483>
