---
tags:
  - linux
---
# :simple-ansible: Ansible

## :hammer_pick: [Installation][1]

```shell
(
  UBUNTU_CODENAME=$(source /etc/os-release && echo $VERSION_CODENAME | sed -e 's/bookworm/jammy/' -e 's/bullseye/focal/' -e 's/buster/bionic/')
  wget -O- "https://keyserver.ubuntu.com/pks/lookup?fingerprint=on&op=get&search=0x6125E2A8C77F2818FB7BD15B93C4A3FD7BB9C367" | sudo gpg --dearmour -o /usr/share/keyrings/ansible-archive-keyring.gpg
  echo "deb [signed-by=/usr/share/keyrings/ansible-archive-keyring.gpg] http://ppa.launchpad.net/ansible/ansible/ubuntu $UBUNTU_CODENAME main" | sudo tee /etc/apt/sources.list.d/ansible.list
  sudo apt update && sudo apt install ansible
)
```

## :octicons-versions-24: [standard-version](https://github.com/conventional-changelog/standard-version)

```shell
# Install
sudo npm i -g standard-version
```

[1]: <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html>
