# Bash

```bash
#/bin/bash

set -e
set -o pipefail

# https://stackoverflow.com/a/246128/1061279
readonly DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
readonly SCRIPT_NAME=$(basename "${0}")
```
## Files

Delete all files matching a pattern in sub folders

```bash
find . -name "*.lock" -type f -delete
```

Clear an already existing file

```shell
>|file.txt
```

Search root for the name

```shell
sudo find / -name file.txt
```

Create a new blank file

```shell
touch file.txt
```

Get file size in bytes

```shell
wc -c file.txt
```

Get the size in bytes of a compressed file

```shell
gzip -c file.txt | wc -c
bzip2 -c file.txt | wc -c
tar -cf - file.txt | wc -c
```

### [Remove File Extension](https://stackoverflow.com/a/12152669/1061279)

```shell
name=$(echo "$filename" | cut -f 1 -d '.')
# or
echo "${filename%%.*}"
```

### [Full File Path](https://stackoverflow.com/a/5265775/1061279)

```shell
readlink -f file.txt
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

[Check if substring is in string](https://stackoverflow.com/a/229606/1061279)

```bash
string='My long string'
if [[ $string == *"My long"* ]]; then
  echo "It's there!"
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

Get domain without the `.com`

`http://user:pw@example.com:80/some/path/url?data&and#hash` -> `example`

```shell
# https://unix.stackexchange.com/a/428990/93726
echo "http://user:pw@example.com:80/some/path/url?data&and#hash" | sed -e "s/[^/]*\/\/\([^@]*@\)\?\([^:/]*\).*/\2/" | sed "s/^www\.//" | cut -f 1 -d '.'
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

### Generate Random String
```shell
cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 64 | head -n 1
```

### [Function Library](https://bash.cyberciti.biz/guide/Shell_functions_library)

```shell
#!/bin/bash
# Load the  myfunctions.sh 
# My local path is /home/vivek/lsst2/myfunctions.sh
. /home/vivek/lsst2/myfunctions.sh

# Define local variables
# var1 is not visitable or used by myfunctions.sh
var1="The Mahabharata is the longest and, arguably, one of the greatest epic poems in any language."

# Invoke the is_root()
is_root && echo "You are logged in as root." || echo "You are not logged in as root."

# Find out if user account vivek exits or not
is_user_exits "vivek" && echo "Account found." || echo "Account not found."

# Display $var1
echo -e "*** Orignal quote: \n${var1}"

# Invoke the to_lower()
# Pass $var1 as arg to to_lower()
# Use command substitution inside echo
echo -e "*** Lowercase version: \n$(to_lower ${var1})"
```

### Run As Different User

```shell
sudo -u "${TARGET_USER}" bash <<"EOF9"
  command
EOF9
```

### Return Value from Function

```shell
function myfunc(){
    local  myresult='some value'
    echo "$myresult"
}

result=$(myfunc)   # or result=`myfunc`
echo $result
```

### [Sort Semver Using Sort](https://stackoverflow.com/a/63027058/1061279)

```shell
printf "1.0\n2.0\n2.12\n2.10\n1.2\n1.10" | sort -t "." -k1,1n -k2,2n -k3,3n
1.0
1.2
1.10
2.0
2.10
2.12
```

### ID (Debian, Ubuntu)

```shell
echo $(. /etc/os-release && echo $ID)
```

### Arch

Subs `aarch64` with `arm64`, `x86_64` with `amd64`, and `armv7l` and `armv6l` with `arm`

```shell
ARCH=$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')
echo $ARCH
```

Subs `aarch64` with `arm64`, `x86_64` with `amd64`, and `armv7l` and `armv6l` with `armhf`

```shell
ARCH=$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2hf/' -e 's/aarch64$/arm64/')
echo $ARCH
```

### [Check if system needs to be restarted][2]

```shell
sudo needrestart
```

We use the systemctl command as follows to restart services one-by-one:

```bash
sudo systemctl restart nginx
sudo systemctl restart firewalld
```

We can use bash for loop as follows:

```bash
for s in systemd-udevd  firewalld  polkit  sshd nginx; do
  sudo systemctl restart "$s"
done
```

How to restart systemd with PID # 1 without rebooting Linux box

```shell
sudo systemctl daemon-reexec
```

And verify it again:

```shell
sudo lsof | grep 'DEL.*lib' | cut -f 1 -d ' ' | sort -u
```

## References

* [set -e, -u, -o pipefail explanation](https://gist.github.com/mohanpedala/1e2ff5661761d3abd0385e8223e16425)
* [pure bash bible](https://github.com/dylanaraps/pure-bash-bible)
* [bash-utility](https://github.com/labbots/bash-utility)

[2]: https://www.cyberciti.biz/faq/how-to-restart-systemd-without-rebooting-linux-when-critical-libraries-installed/
