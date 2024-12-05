# :simple-proxmox: Proxmox

## [Proxmox VE Helper-Scripts][1]

```shell
(
  bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/misc/update-repo.sh)" &&
  bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/misc/post-pve-install.sh)"
)
```

```shell
sudo apt install ca-certificates curl gnupg lsb-release ntp htop zip unzip gnupg apt-transport-https ca-certificates net-tools ncdu apache2-utils ssh-import-id git build-essential
```

```shell
(
  adduser nicholas &&
  usermod -G adm,cdrom,lpadmin,sudo,sambashare,dip,plugdev user123 &&
  su nicholas
)
```

## [Raspberry Pi 4][2]

[1]: <https://community-scripts.github.io/ProxmoxVE/>
[2]: <https://github.com/jiangcuo/Proxmox-Port/wiki/Install-Proxmox-VE-on-Debian-bookworm>
