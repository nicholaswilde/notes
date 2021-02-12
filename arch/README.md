# Arch

## Reference

* https://archlinuxarm.org/platforms/armv6/raspberry-pi
* http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html
* https://wiki.archlinux.org/index.php/Fstab

## As Root

### pacman

```shell
$ su
$ pacman-key --init && ls -R / && ls -R / && ls -R /
$ pacman-key --populate archlinuxarm

$ pacman -Su
$ pacman -Syu
$ pacman -S --needed archlinux-keyring sudo util-linux systemd-swap ntp raspberrypi-firmware base-devel nfs-utils wget python git go go-tools python-pip rpcbind docker screen github-cli lastpass-cli python-pygments ca-certificates ansible pkgfile
```

### Timezone

```shell
$ rm /etc/localtime
$ ln -s /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
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
$ echo "arch" | tee /etc/hostname
# /etc/hosts
127.0.0.1 localhost.localdomain localhost arch
```

### Swap
```shell
$ echo "swapfc_enabled=1" | tee /etc/systemd/swap.conf
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
$ sudo locale-gen
```

```shell
$ useradd -m -G wheel -s /bin/bash pi
$ passwd pi
```

### rpi-update
```shell
$ sudo wget https://raw.github.com/Hexxeh/rpi-update/master/rpi-update -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update
$ export PATH=$PATH:/opt/vc/bin/
$ sudo rpi-update
```

### SSH

## As pi

```shell
$ mkdir ~/.ssh
$ curl https://github.com/nicholaswilde.keys -o ~/.ssh/id_rsa.pub
$ cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
$ chmod 0700 ~/.ssh
```

## SSH Authentication

```bash
# /etc/ssh/sshd_config
...
RSAAuthentication yes
PubkeyAuthentication yes
...
```

## NAS
```shell
$ mkdir ~/nas
```

```shell
# /etc/fstab
UUID=1FDD-27B1  /boot   vfat    defaults        0       0
UUID=b264f4c6-8797-4ed5-99db-e85ceebc1db4  /   ext4    defaults        0       0
192.168.1.192:/home/pi/nas /home/pi/nas nfs rw,async,hard,intr 0 0
```

```shell
$ echo "192.168.1.192:/home/pi/nas /home/pi/nas nfs rw,async,hard,intr 0 0" | sudo tee -a /etc/fstab
```

## Chromebook

```shell
$ curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-notify.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/notify && sudo chmod +x /usr/bin/notify
$ curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-show-file.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/show-file && sudo chmod +x /usr/bin/show-file
$ curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/osc52.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/copy && sudo chmod +x /usr/bin/copy
```
