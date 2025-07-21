# :simple-platformio: PlatformIO

## :hammer_and_wrench: [Installation][1]

```shell
curl -fsSL https://raw.githubusercontent.com/platformio/platformio-core-installer/master/get-platformio.py | python3
```

```shell title="Shell Commands"
(
  [ -d ~/.local/bin/ ] || mkdir ~/.local/bin/ &&
  ln -s ~/.platformio/penv/bin/platformio ~/.local/bin/platformio &&
  ln -s ~/.platformio/penv/bin/pio ~/.local/bin/pio &&
  ln -s ~/.platformio/penv/bin/piodebuggdb ~/.local/bin/piodebuggdb &&
)
```

## :gear: Config

??? abstract "paltformio.ini"

    ```ini
    ; PlatformIO Project Configuration File
    ;
    ;   Build options: build flags, source filter
    ;   Upload options: custom upload port, speed and extra flags
    ;   Library options: dependencies, extra library storages
    ;   Advanced options: extra scripting
    ;
    ; Please visit documentation for the other options and examples
    ; https://docs.platformio.org/page/projectconf.html

    [platformio]
    src_dir = ./src
    default_envs = msc_external_flash_sdcard

    [env]
    platform = espressif32
    framework = arduino
    monitor_speed = 115200

    [env:LILYGO-T-Dongle-S3]
    board = esp32-s3-devkitc-1
    build_src_filter = +<digital-picture-frame/>
    upload_resetmethod = nodemcu
    monitor_rts = 0
    monitor_dtr = 0
    build_flags = 
            -DARDUINO_USB_MODE=1
            -DARDUINO_USB_CDC_ON_BOOT=1
            -D DISPLAY_RST=1
            -D DISPLAY_DC=2
            -D DISPLAY_MOSI=3
            -D DISPLAY_CS=4
            -D DISPLAY_SCLK=5
            -D DISPLAY_LEDA=38
            -D DISPLAY_MISO=-1
            -D DISPLAY_BUSY=-1
            -D DISPLAY_WIDTH=160
            -D DISPLAY_HEIGHT=80
            -D TFT_WIDTH=80
            -D TFT_HEIGHT=160
            -D SD_MMC_D0_PIN=14
            -D SD_MMC_D1_PIN=17
            -D SD_MMC_D2_PIN=21
            -D SD_MMC_D3_PIN=18
            -D SD_MMC_CLK_PIN=12
            -D SD_MMC_CMD_PIN=16
            -D BTN_PIN=0
            -D NUM_LEDS=1
            -D LED_DI_PIN=40
            -D LED_CI_PIN=39
    lib_deps = fastled/FastLED@^3.10.1

    [env:blink]
    extends = env:LILYGO-T-Dongle-S3
    build_src_filter = +<blink/>
    lib_deps =
        fastled/FastLED@^3.10.1

    [env:sd2usbmsc]
    extends = env:LILYGO-T-Dongle-S3
    build_src_filter = +<sd2usbmsc/>

    [env:msc_external_flash_sdcard]
    extends = env:LILYGO-T-Dongle-S3
    build_src_filter = +<msc_external_flash_sdcard/>
    ```

## :link: References

[1]: <https://docs.platformio.org/core/installation/methods/installer-script.html>
