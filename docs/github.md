# GitHub

## Find latest released version without using API and jq

```shell
curl -s https://github.com/neovim/neovim/releases | \
  grep -oP '/neovim/neovim/releases/tag/\K[^"]*' | \
  grep -E '^v?[0-9]+\.[0-9]+\.[0-9]+$'
```
