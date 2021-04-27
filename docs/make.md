# [make](https://www.gnu.org/software/make/manual/make.html)

## Help

Display the help

```Makefile
...
.PHONY: test
test: shellcheck yamllint ## Runs all the tests on the files in the repository.

.PHONY: help
help:
  @grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'
...
```

Output

```shell
shellcheck                     Runs the shellcheck tests on the scripts.
help
```

Alternative

```Makefile
...
## test   : Test the image with snyk
test:
  snyk container test $(NS)/$(IMAGE_NAME):$(VERSION)-ls$(LS) --file=Dockerfile

## help   : Show help
help: Makefile
  @sed -n 's/^##//p' $<
...
```

Output

```
test   : Test the image with snyk
help   : Show help
```
