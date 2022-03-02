# Ubuntu

## [Change Hostname 20.04](https://linuxize.com/post/how-to-change-hostname-on-ubuntu-20-04/)

```shell
sudo hostnamectl set-hostname <hostname>
```

## [Perform a Distrubution Upgrade](https://help.ubuntu.com/community/HirsuteUpgrades)

```shell
sudo do-release-upgrade -d
```

## [Screen on WSL](https://superuser.com/a/1284329/352242)

```shell
mkdir ~/.screen && chmod 700 ~/.screen
```

```shell title="~/.bashrc"
export SCREENDIR=$HOME/.screen
```
