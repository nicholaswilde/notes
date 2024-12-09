---
tags:
  - homelab
  - linux
  - proxmox
---
# :house_with_garden: Homelab :test_tube:

## :simple-grafana: [Grafana][2]

### :floppy_disk: Install

```shell
# amd64
bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/grafana.sh)"
```

```shell
# arm64
bash -c "$(wget -qLO - https://github.com/asylumexp/Proxmox/raw/main/ct/grafana.sh)"
```

### :key: [Passwordless Login][1]

```shell
# /etc/grafana/grafana.ini
#################################### Anonymous Auth ##########################
[auth.anonymous]
# enable anonymous access
enabled = true

# specify organization name that should be used for unauthenticated users
org_name = ORGANIZATION
```

## Prometheus

### :floppy_disk: Install

```shell
# amd64
bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/prometheus.sh)"
```

```shell
# arm64
bash -c "$(wget -qLO - https://github.com/asylumexp/Proxmox/raw/main/ct/prometheus.sh)"
```

## Enable Lifecycle Reload

```shell
# /etc/systemd/system/prometheus.service
...
ExecStart= ... --web.enable-lifecycle
```

Restart service

```shell
curl -X POST http://127.0.0.1:9090/-/reload
```

Add node

```yaml
# /etc/prometheus/prometheus.yml
...
scrape_configs:
  - job_name: 'yourservername'
    static_configs:
      - targets:
        - yourserverip:9100
    metrics_path: /metrics
    scrape_interval: 60s
```

### [Node][4]

In repo

```shell
apt install prometheus-node-exporter -y
```

As root and prometheus-node-exporter is not in repo


```shell
wget https://github.com/prometheus/node_exporter/releases/latest/tar.gz
tar -xvf tar.gz
cd node_exporter
mv node_exporter /usr/local/bin/
```

```
# /etc/systemd/system/node_exporter.service 
[Unit]
Description=Prometheus exporter for machine metrics
Documentation=https://github.com/prometheus/node_exporter

[Service]
Restart=on-failure
User=root
EnvironmentFile=/etc/default/prometheus-node-exporter
ExecStart=/usr/local/bin/node_exporter $ARGS
ExecReload=/bin/kill -HUP $MAINPID
TimeoutStopSec=20s
SendSIGKILL=no

[Install]
WantedBy=multi-user.target
```

```shell
systemctl daemon-reload
systemctl enable node_exporter.service
systemctl start node_exporter.service
journalctl -xeu node_exporter.service
```

Test

```shell
curl "http://localhost:9100/metrics"
```

## :link: References

- [InfluxDB][3]

[1]: <https://stackoverflow.com/a/36014284>
[2]: <https://community-scripts.github.io/ProxmoxVE/scripts?id=grafana>
[3]: <https://www.derekseaman.com/2023/04/home-assistant-installing-influxdb-lxc.html>
[4]: <https://theawesomegarage.com/blog/monitor-your-raspberry-pi-with-prometheus-and-grafana>
