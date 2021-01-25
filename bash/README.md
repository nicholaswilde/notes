# Bash

```
#/bin/bash

set -e

# https://stackoverflow.com/a/246128/1061279
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
```

# Checks
```bash
# Check if chart dir exists
if [ -d "${CHART_PATH}" ]; then
  echo "Chart path already exists, ${CHART_PATH}"
  exit 1
fi

# Check if i2c-tools is installed
if ! command -v git &> /dev/null; then
    echo "git is not installed"
    exit 1
fi

```

# String manipulation

Get variable from a command
```bas
VAR=$(basename "/tmp/file.txt")
```

Get last character

```bash
VAR="${VAR: -1}"
```

Remove last character

```bash
VAR="${VAR::-1}"
```

# Checksums

Get checksum of remote file

```
wget -qO- https://github.com/nicholaswilde/helm-template/archive/main.zip | sha256sum
```

```bash
echo "62df608caba8f2591755f99efac0097c3d7acf313e237e328aa2c046d500efd1  main.zip" | sha256sum -c
```

# Miscellaneous

Download and extract file in one line. Works with tar & zip files.

```
wget -qO- https://github.com/nicholaswilde/helm-template/archive/main.zip | bsdtar -xvf-
```

Make variable global from inside function

```bash
eval VAR="value"
```

Compare semver
```
# https://stackoverflow.com/a/4025065/1061279
function vercomp () {
  if [[ $1 == $2 ]]; then
    return 0
  fi
  local IFS=.
  local i ver1=($1) ver2=($2)
  # fill empty fields in ver1 with zeros
  for ((i=${#ver1[@]}; i<${#ver2[@]}; i++)); do
    ver1[i]=0
  done
  for ((i=0; i<${#ver1[@]}; i++)); do
    if [[ -z ${ver2[i]} ]]; then
      # fill empty fields in ver2 with zeros
      ver2[i]=0
    fi
    if ((10#${ver1[i]} > 10#${ver2[i]})); then
      return 1
    fi
    if ((10#${ver1[i]} < 10#${ver2[i]})); then
      return 2
    fi
  done
  return 0
}

function testvercomp () {
  vercomp $1 $2
  case $? in
    0) op='=';;
    1) op='>';;
    2) op='<';;
  esac
  if [[ $op != $3 ]]; then
    echo "The minimum required version of git is $2"
    exit 1
  fi
}

testvercomp ${GIT_VER} ${MIN_VER} '>'
```

Check empty variable
```
if [ -z "${REPOSITORY}" ]; then
  echo "Could not get the repository"
  exit 1
fi
```
