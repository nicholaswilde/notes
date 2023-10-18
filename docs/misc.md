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

## Shred

Overwrite the data of file1.txt, file2.jpg, and file3.doc using the default shredding methods.

```shell
$ shred -u file1.txt file2.jpg file3.doc
```

## [Combine PDFs](https://stackoverflow.com/a/53754681/1061279)

```shell
$ qpdf --empty --pages *.pdf -- out.pdf
```

## [List if a Package is Installed][1]

```shell
apt -qq list <package name>
```

## Disk Free Space

```shell
df -h
```

## List Hardware

```shell
sudo lshw -short
```

## UID

```shell
id -u $(whoami)
```

## GID

```shell
id -g $(whoami)
```

## [Screen][2]


```shell title="Quit a session"
screen -XS <session-id> quit
```

```shell title="Check current session"
echo $STY
```

```shell title="Detached the previous screen and allowed me to reattach."
screen -d -r
```

```shell title="Scroll upward in the terminal"
C-a [
```

## [Replace Entire Line in File][3]

```shell
sed -i "s|^type     =.*$|type     = mysql|g" config.ini
```

## [keepachangelog](https://keepachangelog.com/en/1.0.0/)

## Quit Screen Sessions

```shell title="List screen ids"
screen -list
```

```shell title="Quit the session"
screen -XS <session-id> quit
```

## References

* https://www.computerhope.com/unix/shred.htm#examples

[1]: https://askubuntu.com/a/823630/344358
[2]: https://askubuntu.com/a/855919
[3]: https://stackoverflow.com/a/11660023/1061279
