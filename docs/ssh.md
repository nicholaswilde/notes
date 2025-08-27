---
tags:
  - linux
---
# :material-ssh: SSH

```shell
(
  [ -d ~/.ssh ] || mkdir ~/.ssh &&
  curl https://github.com/nicholaswilde.keys -o ~/.ssh/authorized_keys &&
  lpass show ssh --attach=att-4322045537695550419-20689 -q > ~/.ssh/id_ed25519 &&
  chmod 600 ~/.ssh/id_ed25519 &&
  ssh-keygen -y -f ~/.ssh/id_ed25519 > ~/.ssh/id_ed25519.pub &&
  chmod 644 ~/.ssh/id_ed25519.pub &&
  chmod 0700 ~/.ssh
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

## :material-check-bold: Verify that Keys Match

To verify if a public and private RSA SSH key pair match, you can compare their fingerprints using the `ssh-keygen` command. If the fingerprints generated from both the private and public keys are identical, then the keys are a matching pair.

1.  **Get the fingerprint of the private key:**
    ```shell
    ssh-keygen -lf /path/to/your/private_key
    ```
    Replace `/path/to/your/private_key` with the actual path to your private key file (e.g., `~/.ssh/id_rsa`).

2.  **Get the fingerprint of the public key:**
    ```shell
    ssh-keygen -lf /path/to/your/public_key.pub
    ```
    Replace `/path/to/your/public_key.pub` with the actual path to your public key file (e.g., `~/.ssh/id_rsa.pub`).

3.  **Compare the outputs:**
    The output for both commands will be a string containing the key size, the fingerprint (a series of hexadecimal numbers separated by colons), and a comment. If the SHA256 fingerprint values are exactly the same for both the private and public keys, then they are a matching pair.

