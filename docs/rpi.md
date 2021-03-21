# RPi

## Raspberry Pi 4 boot from usb

```shell
# to get vendorId and deviceId
$ dmesg
$ sudo nano /boot/cmdline.txt
usb-storage.quirks=152d:1561:u console=serial0,115200 console=tty1 root=PARTUUID=fcf4cb94-02 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait
```

## Ruby

```shell
$ sudo apt-get install rbenv
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> .bashrc
$ echo 'eval "$(rbenv init -)"' >> .bashrc
$ rbenv
$ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
$ rbenv install --list
$ rbenv install 2.3.1
$ rbenv global 2.3.1
```

## Server Images 64bit

- [https://downloads.raspberrypi.org/raspios_arm64/images/](https://downloads.raspberrypi.org/raspios_arm64/images/)

## Convert to server
```bash
(
  sudo apt --purge remove "x11-*"
  sudo apt --purge autoremove
  sudo apt update
  sudo apt upgrade
)
```
