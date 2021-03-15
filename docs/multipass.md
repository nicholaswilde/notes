# [multipass](https://multipass.run/)

```
$ sudo snap install multipass
$ multipass launch --name foo
$ multipass exec foo -- lsb_release -a
# List your instances
$ multipass list
# Stop your instance
$ multipass stop foo bar
# Start your instance
$ multipass start foo
# Clean up what you don’t need
$ multipass delete bar
$ multipass purge
# Find alternate images to launch with multipass
$ multipass find
```

## References
* [https://multipass.run/](https://multipass.run/)
