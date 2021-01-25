# Bash

```
#/bin/bash

set -e

# https://stackoverflow.com/a/246128/1061279
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"

# Check if i2c-tools is installed
if ! command -v git &> /dev/null; then
    echo "git is not installed"
    exit 1
fi
```
