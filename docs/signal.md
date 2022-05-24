# Signal

## Installation

```shell
brew install signal-cli
```

## [Link Device from CLI][1]

```
signal-cli link -n "optional device name" | tee >(xargs -L 1 qrencode -t utf8)
# or
signal-cli link -n "optional device name" | xargs -L 1 qrencode -o /tmp/qrcode.png & while [ ! -f /tmp/qrcode.png ]; do sleep 1; done; xdg-open /tmp/qrcode.png
```

[1]: https://github-wiki-see.page/m/AsamK/signal-cli/wiki/Linking-other-devices-(Provisioning)
