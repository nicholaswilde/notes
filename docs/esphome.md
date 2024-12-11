---
tags:
  - homelab
  - linux
  - esp32
---
# :simple-esphome: [ESPHome][1]

## :material-wifi: Similink XY-WFUSB

### :simple-wire: Wiring

#### :material-serial-port: USB to TTL Serial Adapter

```
( )          <- vcc - empty
( )          <- gnd - empty
( )          <- txd - device rx       usb male port - plugged into computer port
( )          <- rxd - device tx
( )          <- rts - empty
( )          <- cts - empty
```

#### :material-wifi: XY-WFUSB Device

```
usb female port
push button is on the other side of the board 
( )          <- 3v3   - empty
( )          <- rst   - empty
( )          <- gpio0 - empty
( )          <- rx    - adapter txd
( )          <- tx    - adapter rxd
( )          <- gnd   - empty
usb male port         - plugged into power supply/computer port
```

| Pin |	Function | Note |
|-----|----------|------|
| GPIO00 | User (Pad GPIO-0) |	Pulled-up to HIGH, boot fails if pulled LOW  |
| GPIO01 | User (Pad TX) |	HIGH at boot, spits debug output at boot, boot fails if pulled LOW  |
| GPIO02 | None	 | |
| GPIO03 | User (Pad RX) |	HIGH at boot  |
| GPIO04 | Button 1	| Pin input LOW when button is pressed  |
| GPIO05 | Relay 1 |	USB socket power with LED is ON when pin output HIGH  |
| GPIO09 | None	 | |
| GPIO10 | None	 | |
| GPIO12 | None	 | |
| GPIO13 | None	 | |
| GPIO14 | Led_i 1 |	Green LED, LED is ON when pin output HIGH  |
| GPIO15 | None	 | |
| GPIO16 | LedLink |	Blue LED, LED is ON when pin output HIGH. This is the device status LED. |
| GPIO17 | None	| |

### :pencil: Instructions

- Wire USB TTL serial adapter to device.
- Plug in USB TTL serial adapter to computer.
- Plug in device to power supply/other computer port.
- Use esphome command line to flash

```shell
esphome wizard switch.yaml
esphome run switch.yaml
```

### :material-checkbox-multiple-blank-outline: Template

Configure reset pin if it doesn't work.

```yaml
...
uart:
  id: uart_bus
  tx_pin: GPIO1
  rx_pin: GPIO3
  rts_pin: GPIO14
  cts_pin: GPIO15
  baud_rate: 115200 <- need to verify when looking at output of esphome run switch.yaml
```

```yaml
substitutions:
  name: "ipad-charge-controller"
  name_underscored: ipad_charge_controller
  friendly_name: iPad charge controller

esphome:
  name: ${name}
  name_add_mac_suffix: false
  friendly_name: ${friendly_name}
  platform: ESP8266
  board: esp01_1m

api:
  encryption:
    key: !secret encryption_key

logger:
  level: debug

ota:
  password: !secret ota_password

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  manual_ip:
    # I am using static IPs here.  You may want to
    # omit this section altogether.
    static_ip: 10.250.1.18
    gateway: 10.250.1.1
    subnet: 255.255.255.0

button:
- platform: restart
  name: Restart
  entity_category: diagnostic
  icon: mdi:restart
- platform: safe_mode
  name: Safe mode restart
  entity_category: diagnostic
  icon: mdi:restart-alert

# Blue LED
status_led:
  pin:
    number: GPIO16

switch:
  # Relay
  - platform: gpio
    id: relay
    pin: GPIO5

  # Green LED
  - platform: gpio
    pin: GPIO14
    id: green_led
    inverted: true # start on

  # Switch template to link relay and green LED states
  # LED is on when relay is off
  - platform: template
    id: ${name_underscored}_switch
    name: Switch
    lambda: |-
      if (id(relay).state) {
        return true;
      } else {
        return false;
      }
    turn_on_action:
        - switch.turn_on:
            id: green_led
        - switch.turn_on:
            id: relay
    turn_off_action:
        - switch.turn_off:
            id: green_led
        - switch.turn_off:
            id: relay

# Button
binary_sensor:
  - platform: gpio
    id: ${name_underscored}_button
    pin:
      number: GPIO04
      mode: INPUT_PULLUP
      inverted: True
    on_press:
      - switch.toggle: "${name_underscored}_switch"
```

## :link: References

- <https://esphome.io/guides/getting_started_command_line.html>
- <https://community.home-assistant.io/t/sinilink-wifi-usb-controller-xy-wfusb-turns-usb-port-power-on-off-esphome-yaml/574532/2>
- <https://tech.scargill.net/aliexpress-sinilink-wifi-usb-controller/>
- <https://rudd-o.com/linux-and-free-software/switching-an-usb-load-on-or-off-using-the-sinilink-xy-wfusb-and-esphome>
- <https://esphome.io/components/uart.html>

[1]: <https://esphome.io/>
