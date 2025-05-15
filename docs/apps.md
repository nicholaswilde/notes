# Apps

## [Chrony][1]

### Server

```shell
(
  sudo apt install chrony
  sudo service chrony restart
)
```

!!! abstract "/etc/chrony/chrony.conf"

    ```apacheconf
    confdir /etc/chrony/conf.d
    pool 2.debian.pool.ntp.org iburst
    sourcedir /run/chrony-dhcp
    sourcedir /etc/chrony/sources.d
    keyfile /etc/chrony/chrony.keys
    driftfile /var/lib/chrony/chrony.drift
    ntsdumpdir /var/lib/chrony
    logdir /var/log/chrony
    maxupdateskew 100.0
    rtcsync
    makestep 1 3
    leapsectz right/UTC
    allow 192.168.1.0/24
    authselectmode ignore
    manual
    ```

### Client

```shell
(
  sudo apt install chrony
  sudo service chrony restart
  # Check that server is running
  sudo chronyc sources -v -a
  sudo chronyc clients
  sudo chronyc ntpdata <Server IP>
  # Check that port 123 is running
  nc -zvu <Server IP> 123
  chronyc activity
  chronyc tracking
)
```

```apacheconf
# /etc/chrony/chrony.conf
server 192.168.1.198 iburst trust
authselectmode ignore
confdir /etc/chrony/conf.d
pool ntp.ubuntu.com        iburst maxsources 4
pool 0.ubuntu.pool.ntp.org iburst maxsources 1
pool 1.ubuntu.pool.ntp.org iburst maxsources 1
pool 2.ubuntu.pool.ntp.org iburst maxsources 2
sourcedir /run/chrony-dhcp
sourcedir /etc/chrony/sources.d
keyfile /etc/chrony/chrony.keys
driftfile /var/lib/chrony/chrony.drift
ntsdumpdir /var/lib/chrony
logdir /var/log/chrony
maxupdateskew 100.0
rtcsync
makestep 1 3
leapsectz right/UTC
```

## Ubuntu

```shell
sudo apt install unzip build-essential
```

## [brew](https://brew.sh/)

```shell
(
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" && \
  echo >> /home/nicholas/.bashrc && \
  echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/nicholas/.bashrc && \
  eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
  brew install gcc
)
```

```bash
# should add this to dotfiles
brew leaves > my_brew.txt
xargs brew install < my_brew.txt
```

### [Chrome OS][2]

```shell
export CI=1
sudo chmod -R nicholas:nicholas /home/linuxbrew
```

## [gh](https://github.com/cli/cli)

```shell
brew install gh
```

## [nanorc](https://github.com/scopatz/nanorc)

```shell
wget https://raw.githubusercontent.com/scopatz/nanorc/master/install.sh -O- | sh
```

```shell
echo "set tabsize 2" >> ~/.nanorc
echo "set tabstospaces" >> ~/.nanorc
```

## [semver](https://github.com/fsaintjacques/semver-tool)

```shell
sudo wget -O /usr/bin/semver https://github.com/fsaintjacques/semver-tool/raw/master/src/semver
sudo chmod +x /usr/bin/semver
```

## [pre-commit](https://pre-commit.com/#install)

```shell
brew install pre-commit
```

## [PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/install/install-ubuntu?view=powershell-7.2#installation-via-package-repository)

```shell
# Update the list of packages
sudo apt-get update
# Install pre-requisite packages.
sudo apt-get install -y wget apt-transport-https software-properties-common
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb
# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb
# Update the list of packages after we added packages.microsoft.com
sudo apt-get update
# Install PowerShell
sudo apt-get install -y powershell
# Start PowerShell
pwsh
```

## mkdocs

```shell
(
  wget https://bootstrap.pypa.io/get-pip.py
  python get-pip.py
  pip install mkdocs
)
```

## mkdocs-material

```shell
pip install mkdocs-material mkdocs-minify-plugin
```

[1]: <https://ubuntu.com/server/docs/how-to-serve-the-network-time-protocol-with-chrony>
[2]: <https://github.com/Homebrew/install/issues/369>
[2]
