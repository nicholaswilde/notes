# :simple-raspberrypi: RPi

## [Raspberry Pi 4 boot from usb][1]

```shell
sudo raspi-config
Advanced Options -> Boot Order -> B2 NVMe/USB
sudo reboot
```

```shell
# to get vendorId and deviceId
$ dmesg
$ sudo nano /boot/cmdline.txt
usb-storage.quirks=152d:1561:u console=serial0,115200 console=tty1 root=PARTUUID=fcf4cb94-02 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait
$ echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
# Check
$ mount | egrep "/([[:space:]]|boot)"
```

```shell
vcgencmd otp_dump | grep 17
17:1020000a=USB boot disabled
17:3020000a=USB boot enabled
```

```shell
sudo raspi-config
sudo rpi-update
sudo raspi-config --expand-rootfs
```

## [Trusted Key Problem][3]

```shell
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
8 packages can be upgraded. Run 'apt list --upgradable' to see them.
W: https://packages.microsoft.com/repos/edge/dists/stable/InRelease: Key is stored in legacy trusted.gpg keyring (/etc/apt/trusted.gpg), see the DEPRECATION section in apt-key(8) for details.
W: https://download.sublimetext.com/apt/stable/InRelease: Key is stored in legacy trusted.gpg keyring (/etc/apt/trusted.gpg), see the DEPRECATION section in apt-key(8) for details.
```

```shell
cd /etc/apt
sudo cp trusted.gpg trusted.gpg.d
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
[3]: <https://askubuntu.com/a/1408456>
