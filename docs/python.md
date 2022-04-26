# Python

## Update All Installed Packages

```shell
pip3 list --outdated --format=freeze | grep -v '^\-e' | cut -d = -f 1 | xargs -n1 pip3 install -U
```

## Remap `python` to `python3`

```shell
# https://askubuntu.com/a/1234598/344358
sudo apt install python-is-python3
```
