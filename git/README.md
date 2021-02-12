# Git

## gpg

[Telling Git about your signing key](https://docs.github.com/en/github/authenticating-to-github/telling-git-about-your-signing-key)

## Configure

```bash
git config --global user.email "ncwilde43@gmail.com"
git config --global user.name "Nicholas Wilde"
git config credential.helper store
git config --global init.defaultBranch main
git config --global user.signingkey <gpg key fingerprint>
```

