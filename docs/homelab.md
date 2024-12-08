---
tags:
  - homelab
  - linux
---
# :house_with_garden: Homelab :test_tube:

## :simple-grafana: [Grafana][2]

### :floppy_disk: Install

```shell
# amd64
bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/grafana.sh)"
```

```shell
# arm64
bash -c "$(wget -qLO - https://github.com/asylumexp/Proxmox/raw/main/ct/grafana.sh)"
```

### :key: [Passwordless Login][1]

```shell
# /etc/grafana/grafana.ini
#################################### Anonymous Auth ##########################
[auth.anonymous]
# enable anonymous access
enabled = true

# specify organization name that should be used for unauthenticated users
org_name = ORGANIZATION
```

## :link: References

[1]: <https://stackoverflow.com/a/36014284>
[2]: <https://community-scripts.github.io/ProxmoxVE/scripts?id=grafana>
