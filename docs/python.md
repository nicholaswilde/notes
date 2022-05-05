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

## Pip

```bash
sudo apt install python3-pip
```

## Install GitHub Tarball

```
pip install --upgrade https://github.com/<username>/<repo>/<tarball>/<branch>
pip install --upgrade https://github.com/nicholaswilde/parse-ingredients/tarball/nlp-proof-of-concept
```
