# Arch

## As Root

### pacman

```shell
su
pacman-key --init && ls -R / && ls -R / && ls -R /
pacman-key --populate archlinuxarm

pacman -Su
pacman -Syu
pacman -S --needed archlinux-keyring sudo util-linux systemd-swap ntp raspberrypi-firmware base-devel nfs-utils wget python git go go-tools python-pip rpcbind docker screen github-cli lastpass-cli python-pygments ca-certificates ansible pkgfile
```

### Timezone

```shell
rm /etc/localtime
ln -s /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
```

### Sudo

```bash
# /etc/sudoers
root ALL=(ALL) ALL

## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL) ALL

## Same thing without a password
%wheel ALL=(ALL) NOPASSWD: ALL

## Uncomment to allow members of group sudo to execute any command
%sudo   ALL=(ALL) ALL
```

### Hostname
```shell
echo "arch" | tee /etc/hostname
# /etc/hosts
127.0.0.1 localhost.localdomain localhost arch
```

### Swap
```shell
echo "swapfc_enabled=1" | tee /etc/systemd/swap.conf
```

### Locale
```shell
$ locale -a
```
```shell
# /etc/locale.gen
...
en_US.UTF-8 UTF-8
..
```
```shell
sudo locale-gen
```

```shell
useradd -m -G wheel -s /bin/bash pi
passwd pi
```

### rpi-update
```shell
sudo wget https://raw.github.com/Hexxeh/rpi-update/master/rpi-update -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update
export PATH=$PATH:/opt/vc/bin/
sudo rpi-update
```

## As pi

### SSH

```shell
mkdir ~/.ssh
curl https://github.com/nicholaswilde.keys -o ~/.ssh/id_rsa.pub
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/id_rsa
cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
chmod 0700 ~/.ssh
ssh-import-id-gh nicholaswilde
```

## SSH Authentication

```bash
# /etc/ssh/sshd_config
...
RSAAuthentication yes
PubkeyAuthentication yes
...
```

## Reference

- <https://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2>
- <http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html>
- <https://wiki.archlinux.org/index.php/Fstab>
