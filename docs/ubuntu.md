---
tags:
  - linux
---
# :fontawesome-brands-ubuntu: Ubuntu

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

## [Remove Snap][1]

```shell
(
  sudo umount /var/snap
  sudo apt purge snapd
  sudo rm -rf ~/snap /snap /var/snap /var/lib/snapd
)
```

## [An upgrade from 'hirsute' to 'jammy' is not supported with this tool][2]

```shell
Reading cache

Checking package manager

Can not upgrade 

An upgrade from 'hirsute' to 'jammy' is not supported with this tool.
```

```bash title="script.sh"
#!/bin/bash
echo "Updating"
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get dist-upgrade -y
echo "Bypass check"
sudo sed -i 's/continue/pass/g' /usr/lib/python3/dist-packages/UpdateManager/Core/MetaRelease.py
echo "Upgrade distro"
sudo do-release-upgrade
```

```shell
chmod +x script.sh && ./script.sh
```

## [Ubuntu – apt-get update fails “The repository no longer has a Release file”][3]

```shell
sudo apt update
Err:6 http://archive.ubuntu.com/ubuntu eoan Release
404 Not Found [IP: 91.189.88.142 80]
```

```shell
# backup your sources file
cp /etc/apt/sources.list /etc/apt/sources.list.bak 

# replace the links with the archive address
sudo sed -i -re 's/([a-z]{2}.)?archive.ubuntu.com|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list

# run update again
sudo apt update && sudo apt dist-upgrade
```

## [Auto Retart Daemons during Update][4]

```shell
sudo sed -i 's/#$nrconf{restart} = '"'"'i'"'"';/$nrconf{restart} = '"'"'a'"'"';/g' /etc/needrestart/needrestart.conf
```

## [User Groups][5]

```shell
usermod -a -G adm,cdrom,lpadmin,sudo,sambashare,dip,plugdev nicholas
```

## [Autocomplete Directories][6]

`export CDPATH=foo`

## [Apt Cacher NG][7]

### Server

```
# /etc/apt-cacher-ng/acng.conf
PassThroughPattern: .*
CacheDir: /mnt/storage/apt-cacher-ng
```

```
systemctl restart apt-cacher-ng
```

### Client

```shell
echo "Acquire::http::Proxy \"http://aptcache.nicholaswilde.io:3142\";"| sudo tee /etc/apt/apt.conf.d/00aptproxy
```

[1]: <https://fedingo.com/how-to-remove-snap-in-ubuntu/>
[2]: <https://stackoverflow.com/questions/73034540>
[3]: <https://veducate.co.uk/ubuntu-apt-update-fails/>
[4]: <https://askubuntu.com/a/1421221/344358>
[5]: <https://askubuntu.com/a/1381087>
[6]: <https://superuser.com/a/571778>
[7]: <https://www.atlantic.net/vps-hosting/how-to-set-up-apt-caching-server-using-apt-cacher-ng-on-ubuntu/>
