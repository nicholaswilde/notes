# Apt

## The following signatures were invalid: BADSIG 54404762BBB6E853

https://security.debian.org/debian-security/README.security

https://www.reddit.com/r/Proxmox/comments/1hiamg8/apt_wont_update_keys_missing_or_invalid/

```ini
If you are using apt you can use this entry in /etc/apt/sources.list:

deb http://security.debian.org/debian-security stable-security main
```

```shell
(
  sudo rm -r /var/lib/apt/lists
  sudo mkdir -p /var/lib/apt/lists/partial
  sudo apt clean
  sudo apt update
)
```
