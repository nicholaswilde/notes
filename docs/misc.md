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

## References

* https://www.computerhope.com/unix/shred.htm#examples

[1]: https://askubuntu.com/a/823630/344358
