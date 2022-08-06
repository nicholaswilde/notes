# Micro

## Install

```shell
brew install micro
```

## [Wakatime][1]

```shell
micro -plugin install wakatime
touch ~/.wakatime.cfg
# copy api_key to clipboard
lpass show 1247588986144505823 --password | copy
# from inside micro press ctrl+e
wakatime.apikey
```

## [Set Filetype][2]

```
Ctrl + e
set filetype yaml
```

```json title="~/.config/micro/settings.json"
{
    "/etc/default/grub": {
        "filetype": "bash"
    }
}
```

## References
- <https://github.com/zyedidia/micro/blob/master/runtime/help/options.md>
- <https://github.com/zyedidia/micro/blob/master/runtime/help/commands.md>
- <https://github.com/zyedidia/micro/blob/master/runtime/help/keybindings.md>

[1]: https://github.com/wakatime/micro-wakatime
[2]: https://github.com/zyedidia/micro/issues/2080
