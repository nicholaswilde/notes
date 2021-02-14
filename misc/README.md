# Misc

## Paperkey

Export gpg key to a printable version

https://wiki.archlinux.org/index.php/Paperkey

## Public Keys

* [GPG](https://github.com/nicholaswilde.gpg)
* [SSH](https://github.com/nicholaswilde.keys)

## Timezone

```shell
$ sudo timedatectl set-timezone America/Los_Angeles
```

## Images

### Imagemagick

```shell
# Ubuntu
$ sudo apt-get install sudo apt install imagemagick-6.q16hdri
# Convert image from ico to png
$ convert "favicon.ico" -thumbnail 16x16 -alpha on -background none -flatten "favicon.png"
```
