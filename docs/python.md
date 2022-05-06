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

## [Install GitHub Tarball][1]

```
pip install --upgrade https://github.com/<username>/<repo>/<tarball>/<branch>
pip install --upgrade https://github.com/nicholaswilde/parse-ingredients/tarball/nlp-proof-of-concept
pip install git+https://github.com/jkbr/httpie.git#egg=httpie
```

## Create Tarball of package in `./dist` folder

```shell
python setup.py sdist
```

[1]: https://stackoverflow.com/a/15268990/1061279
