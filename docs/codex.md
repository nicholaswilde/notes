# ![codex](https://cdn.jsdelivr.net/gh/selfhst/icons/png/openai.png){width="36"}Codex

[Codex CLI][1] is a coding agent from OpenAI that runs locally on your computer.
If you are looking for the cloud-based agent from OpenAI, Codex Web

## :hammer_pick: Installation

=== "npm"

    ```bash
    npm install -g @openai/codex
    ```

=== "brew"

    ```bash
    brew install codex
    ```

## :gear: Config

```ini
export OPENAI_API_KEY="your-api-key-here"
```

```toml
# ~/.codex/config.toml
preferred_auth_method = "apikey"
```

Then simply run `codex` to get started:

```bash
codex
```

[1]: <https://github.com/openai/codex>
