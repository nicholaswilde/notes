```yaml
      - name: Dump github context
        run:   echo "$GITHUB_CONTEXT"
        shell: bash
        env:
          GITHUB_CONTEXT: ${{ toJson(github) }}
```
