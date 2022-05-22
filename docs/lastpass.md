# LastPass

## Installation

```bash
brew install lastpass-cli
```

## Show Attachment

```shell
lpass show ssh --attach=<attachment id>
```

## Rename Item

```shell
echo "${new_name}" | lpass edit --non-interactive --name "${id}"
```

## [Export as JSON][1]

```shell
lpass show --expand-multi --basic-regexp '.*' --json
```

## References

- <https://github.com/lastpass/lastpass-cli>

[1]: https://github.com/lastpass/lastpass-cli/issues/560#issuecomment-724266729
