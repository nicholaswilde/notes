# RPi

## [nanorc](https://github.com/scopatz/nanorc)

```shell
$ wget https://raw.githubusercontent.com/scopatz/nanorc/master/install.sh -O- | sh
```

## Raspberry Pi 4 boot from usb

```shell
# to get vendorId and deviceId
$ dmesg
$ sudo nano /boot/cmdline.txt
usb-storage.quirks=152d:1561:u console=serial0,115200 console=tty1 root=PARTUUID=fcf4cb94-02 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait
```
