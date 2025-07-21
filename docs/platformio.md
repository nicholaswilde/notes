# :simple-platformio: PlatformIO

## :hammer_and_wrench: Installation

```shell
(
  curl -fsSL -o get-platformio.py https://raw.githubusercontent.com/platformio/platformio-core-installer/master/get-platformio.py
  python3 get-platformio.py
)
```

```shell title="Shell Commands"
(
  [ -d ~/.local/bin/ ] || mkdir ~/.local/bin/ &&
  ln -s ~/.platformio/penv/bin/platformio ~/.local/bin/platformio &&
  ln -s ~/.platformio/penv/bin/pio ~/.local/bin/pio &&
  ln -s ~/.platformio/penv/bin/piodebuggdb ~/.local/bin/piodebuggdb &&
)
```
