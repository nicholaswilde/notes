# uv

## :hammer_and_wrench: Installation

=== "curl"

    ```
    curl -LsSf https://astral.sh/uv/install.sh | less
    ```

=== "apt"

    ```
    (
      sudo mkdir -p /etc/apt/keyrings
      curl -LsSf https://astral.sh/uv/packaging/key.asc | sudo gpg --dearmor -o /etc/apt/keyrings/astral.gpg
      echo "deb [signed-by=/etc/apt/keyrings/astral.gpg] https://astral.sh/uv/packaging/debian stable main" | sudo tee /etc/apt/sources.list.d/astral.list
      sudo apt-get update
      sudo apt-get install uv
    )
    ```
## :link: References

- <https://docs.astral.sh/uv/getting-started/installation/>
