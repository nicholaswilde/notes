# :simple-tmux: tmux

## Installation

!!! quote ""

    ```shell
    sudo apt install tmux
    ```

## [Allow Notify in tmux][1]

!!! quote ""

    ```shell
    set -g allow-passthrough on
    ```

## [TPM][2]

!!! quote "Install tpm"

    ```
    mkdir -p ~/.tmux/plugins
    git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
    # Ctrl + b
    # Shift + I
    ```

## [Autostart Session][3]

```shell title="~/.bashrc"
if [[ $- =~ i ]] && [[ -z "$TMUX" ]] && [[ -n "$SSH_TTY" ]]; then
  tmux attach-session -t ssh_tmux || tmux new-session -s ssh_tmux
fi
```

This command creates a tmux session called ssh_tmux if none exists, or reattaches to a already existing session with that name. In case your connection dropped or when you forgot a session weeks ago, every SSH login automatically brings you back to the tmux-ssh session you left behind.

### What if I mess up and lock myself out somehow?

```shell
ssh -t myname@myserver bash --norc
```

(You might also need --noprofile, depending on your setup)

```shell title="Or just connect with sh"
ssh -t myname@myserver sh
```

## :link: References

- <https://tmuxcheatsheet.com/>

[1]: <https://groups.google.com/a/chromium.org/g/chromium-hterm/c/davGyRBr3l8/m/7BPjaTwQAAAJ>
[2]: <https://github.com/tmux-plugins/tpm>
[3]: <https://stackoverflow.com/a/40192494/1061279>
