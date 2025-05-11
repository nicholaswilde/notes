# :snowflake: NixOS

## Managed Node

```shell
TEMPLATE_STORAGE='pve-shared'
# Name of the template file downloaded from Hydra.
TEMPLATE_FILE='nixos-system-x86_64-linux.tar.xz'
# Name to assign to new NixOS container.
CONTAINER_HOSTNAME='nixos'
# Which storage location to place the new NixOS container.
CONTAINER_STORAGE='local-lvm'
# How much RAM to assign the new container.
CONTAINER_RAM_IN_MB='8192'
# How much disk space to assign the new container.
CONTAINER_DISK_SIZE_IN_GB='80'
```

```shell
pct create "$(pvesh get /cluster/nextid)" \
  --arch amd64 \
  "${TEMPLATE_STORAGE}:vztmpl/${TEMPLATE_FILE}" \
  --ostype unmanaged \
  --description nixos \
  --hostname "${CONTAINER_HOSTNAME}" \
  --net0 name=eth0,bridge=vmbr0,ip=dhcp,firewall=1 \
  --storage "${CONTAINER_STORAGE}" \
  --memory "${CONTAINER_RAM_IN_MB}" \
  --rootfs ${CONTAINER_STORAGE}:${CONTAINER_DISK_SIZE_IN_GB} \
  --unprivileged 1 \
  --features nesting=1 \
  --cmode console \
  --onboot 1 \
  --start 1
```

## :package: LXC

```shell
(
  GITHUB_USERNAME='nicholaswilde'
  mkdir -p ~/.ssh && \
    curl "https://github.com/${GITHUB_USERNAME}.keys" > ~/.ssh/authorized_keys
)
```

```shell
(
  curl \
    --show-error \
    --fail \
    https://mtlynch.io/notes/nixos-proxmox/configuration.nix \
    > /etc/nixos/configuration.nix

  nix-channel --update && \
    nixos-rebuild switch --upgrade && \
    echo "install complete, rebooting..." && \
    poweroff --reboot
)
```

```
nano /etc/nixos/configuration.nix
```

```shell
(
  nix-channel --update
  nixos-rebuild switch --upgrade
)
```

## :link: References

- <https://mtlynch.io/notes/nixos-proxmox/>
- <https://hydra.nixos.org/project/nixos>
- <https://search.nixos.org/>
