---
tags:
  - linux
---
# :simple-task: [Task](https://taskfile.dev/#/)

## Installation

```shell
brew install go-task/tap/go-task
```

```shell
# For Default Installion to ./bin with debug logging
sh -c "$(curl --location https://taskfile.dev/install.sh)" -- -d

# For Installation To /usr/local/bin for userwide access with debug logging
# May require sudo sh
sh -c "$(curl --location https://taskfile.dev/install.sh)" -- -d -b /usr/local/bin
```

## Checks

```yaml
  _check-chart:
    cmds:
      # Check if variable exists
      - test -n "{{ .CHART }}" || (echo "Please define CHART parameter"; exit 1)
      # Check if directory exists
      - test -d {{.GIT_ROOT}}/charts/{{.CHART}} || (echo "Chart {{ .CHART }} doesn't exist"; exit 1) 
      # Check if a file exists
      - test -f {{.GIT_ROOT}}/charts/{{.CHART}} || (echo "Chart {{ .CHART }} doesn't exist"; exit 1) 
    silent: true
```

!!!NOTE
    If you want to call a task declared in the root Taskfile from within an included Taskfile, add a leading `:`
    like this: `task: :task-name`.

## [Escape Braces][1]

```shell
{{"{{"}}
{{"}}"}}
```

produces

```shell
{{
}}
```

```shell
cmds:
  - sed -i 's/{{"{{"}} LIB {{"}}"}}/{{ .EXAMPLE }}/g' ./examples/{{ .EXAMPLE }}.sh
```

[1]: <https://github.com/go-task/task/issues/179#issuecomment-466780873>
