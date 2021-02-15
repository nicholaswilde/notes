# Bash

```bash
#/bin/bash

set -e

# https://stackoverflow.com/a/246128/1061279
readonly DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
readonly SCRIPT_NAME=$(basename "${0}")
```
## Files

Delete all files matching a pattern in sub folders

```bash
$ find . -name "*.lock" -type f -delete
```

Clear an already existing file

```shell
$ >|file.txt
```

Create a new blank file

```shell
$ touch file.txt
```

## Checks
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

Check empty variable

```bash
if [ -z "${REPOSITORY}" ]; then
  echo "Could not get the repository"
  exit 1
fi
```

Single line checks

```bash

# Check is variable is null
function is_null {
  [ -z "$1" ]
}

# Check if directory exists
function dir_exists(){
  [ -d "${1}" ]
}

# Check if command exists
function command_exists(){
  command -v "${1}" &> /dev/null
}

is_null "$left" && echo "is null"

```

## String manipulation

Get variable from a command

```bash
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

## Checksums

Get checksum of remote file

```bash
wget -qO- https://github.com/nicholaswilde/helm-template/archive/main.zip | sha256sum
```

```bash
echo "62df608caba8f2591755f99efac0097c3d7acf313e237e328aa2c046d500efd1  main.zip" | sha256sum -c
```

## Scripts

Get single options, -v, -h, etc.

```bash
# https://www.jamescoyle.net/how-to/1774-bash-getops-example
# https://opensource.com/article/19/12/help-bash-program
# Get the options
while getopts ":hv" o; do
  case "${o}" in
    h) # display Help
      help
      exit 0;;
    v)
      printf "${SCRIPT_NAME} version ${APP_VERSION}\n"
      exit 0;;
    \?) # incorrect option
      usageerror;;
  esac
done

# https://unix.stackexchange.com/a/214151/93726
shift "$((OPTIND-1))"
```

## Miscellaneous

printf

```bash
printf "%s is the value" "${var}"

# Expand the tab, \t or new line \n
var="value\t"
printf "%b is the value" "${var}"
```

Insert first line of file
```bash
sed  -i '1i text' filename
```

Delete a tmp dir on exit
```bash
# https://stackoverflow.com/a/687052/1061279
trap 'rm -rf -- "$TMP_DIR"' EXIT
```

Download and extract file in one line. Works with tar & zip files.

```bash
wget -qO- https://github.com/nicholaswilde/helm-template/archive/main.zip | bsdtar -xvf-
```

Make variable global from inside function

```bash
eval VAR="value"
```

Compare semver

```bash
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

