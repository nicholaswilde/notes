# Github Actions

```yaml
      - name: Dump github context
        run:   echo "$GITHUB_CONTEXT"
        shell: bash
        env:
          GITHUB_CONTEXT: ${{ toJson(github) }}
```

```yaml
      - name: Get tag
        run: echo "tag=${{ github.event.inputs.version }}-${{ github.event.inputs.ls }}" >> $GITHUB_ENV

      - name: Remove docker from the repo name
        run: echo "repo_name=$(echo "${{ github.event.repository.name }}" | sed 's/[^-]*-//')" >> $GITHUB_ENV

      - name: Get current date
        run: echo "date=$(date -u +%Y-%m-%dT%H%M%SZ)" >> $GITHUB_ENV
        
        build-args: |
            BUILD_DATE=${{ env.date }}
            REPO_NAME=${{ env.repo_name }}:
```

## Setup Task

```yaml
---
name: ci
on:  # yamllint disable-line rule:truthy
  workflow_dispatch:

jobs:
  test_code:
    name: Test code
    runs-on: ubuntu-latest
    steps:
      - name: Checkout main
        uses: actions/checkout@v3
      - name: Setup Task
        run: |
          /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" && \
          brew install go-task/tap/go-task
```
