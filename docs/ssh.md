---
tags:
  - linux
---
# :material-ssh: SSH

```shell
(
  sudo apt install ssh-import-id &&
  [ -d ~/.ssh ] || mkdir ~/.ssh &&
  curl https://github.com/nicholaswilde.keys -o ~/.ssh/id_rsa.pub &&
  chmod 644 ~/.ssh/id_rsa.pub &&
  lpass show ssh --attach=att-4322045537695550419-20689 -q > ~/.ssh/id_rsa &&
  chmod 600 ~/.ssh/id_rsa &&
  cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys &&
  chmod 0700 ~/.ssh &&
  ssh-import-id-gh nicholaswilde
)
```

## :key: Authentication

```shell
(
  sudo sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/g' /etc/ssh/sshd_config && \
  echo "RSAAuthentication yes" | sudo tee -a /etc/ssh/sshd_config
)
```

```bash
# /etc/ssh/sshd_config
...
RSAAuthentication yes
PubkeyAuthentication yes
...
```

```shell
# Restart ssh
sudo systemctl restart sshd
```

## :material-check-bold: [Verify that Keys Match][1]

Use the following command, to test both files. The output of the command will show the 'signature' of both files. When
the 'signature' matches, they show the public key and private key are both valid and match.

```shell
# ssh-keygen -l -f ~/.ssh/id_rsa
2048 SHA256:REDACTED cptest@domain.tld (RSA)

# ssh-keygen -l -f ~/.ssh/id_rsa.pub
2048 SHA256:REDACTED cptest@domain.tld (RSA)
```

[1]: https://support.cpanel.net/hc/en-us/articles/360056952833-How-to-verify-if-a-public-and-private-RSA-SSH-key-match-
