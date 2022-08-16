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

## [lpass login returns 'unknown'][2]

> $ lpass login username@email.com <br/>
> Please enter the LastPass master password for username@email.com.
> 
> unknown
> Master Password:

A workaround is to:

1. Open Account Settings in your browser (Open My Vault → Account Settings)
2. Press Show Advanced Settings
3. Set General → Security → Password Iterations to exactly 100100

LastPass will ask for your Master password and re-encrypt your vault. After that using lpass should work again.

## References

- <https://github.com/lastpass/lastpass-cli>

[1]: https://github.com/lastpass/lastpass-cli/issues/560#issuecomment-724266729
[2]: https://github.com/lastpass/lastpass-cli/issues/604#issue-894502620
