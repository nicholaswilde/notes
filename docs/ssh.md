# SSH

```shell
mkdir ~/.ssh
curl https://github.com/nicholaswilde.keys -o ~/.ssh/id_rsa.pub
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/id_rsa
cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
chmod 0700 ~/.ssh
ssh-import-id-gh nicholaswilde
```
