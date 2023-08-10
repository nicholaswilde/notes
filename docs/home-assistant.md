# :house: Home Assistant

## :arrow_down: Install

``` shell
mkdir ~/ha
docker run -d \
  --name homeassistant \
  --privileged \
  --restart=unless-stopped \
  -e TZ=America/Los_Angeles \
  -v /home/nicholas/ha:/config \
  --network=host \
  ghcr.io/home-assistant/home-assistant:stable
```
