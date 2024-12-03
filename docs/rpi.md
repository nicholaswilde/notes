# :simple-raspberrypi: RPi

## [Raspberry Pi 4 boot from usb][1]

```shell
# to get vendorId and deviceId
$ dmesg
$ sudo nano /boot/cmdline.txt
usb-storage.quirks=152d:1561:u console=serial0,115200 console=tty1 root=PARTUUID=fcf4cb94-02 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait
$ echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
```

```shell
vcgencmd otp_dump | grep 17
17:1020000a=USB boot disabled
17:3020000a=USB boot enabled
```

```shell
sudo raspi-config
sudo rpi-update
```

## [Generate User Before Boot][2]

```shell
echo 'mypassword' | openssl passwd -6 -stdin | sudo tee -a /boot/userconf.txt
# /boot/userconf.txt
user:password-hash
# Enable ssh
touch /boot/ssh
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
  sudo apt --purge remove -y "x11-*"
  sudo apt --purge -y autoremove
  sudo apt update
  sudo apt upgrade -y
)
```

## [Swap](https://nebl.io/neblio-university/enabling-increasing-raspberry-pi-swap/)

Temporarily Stop Swap

```shell
sudo dphys-swapfile swapoff
```

Modify the size of the swap

```shell
sudo nano /etc/dphys-swapfile
CONF_SWAPSIZE=1024
```

Initialize Swap File

```shell
sudo dphys-swapfile setup
```

Start Swap

```shell
sudo dphys-swapfile swapon
```

## References

[1]: <https://www.makeuseof.com/how-to-boot-raspberry-pi-ssd-permanent-storage/>
[2]: <https://www.raspberrypi.com/news/raspberry-pi-bullseye-update-april-2022/>
