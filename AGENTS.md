# Project Overview

This directory serves as a personal knowledge base or notes repository, primarily focused on
technical topics. It's built using [MkDocs](https://www.mkdocs.org/) with the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
theme, allowing the notes to be hosted online and accessed from various devices. The notes cover a wide range of subjects,
with a particular emphasis on Debian-based distributions.

## Key Files

* `mkdocs.yml`: The main configuration file for MkDocs, defining the site's name, description, author,
    navigation structure, theme, plugins, and markdown extensions.
* `Taskfile.yml`: Defines various automation tasks using [Task](https://taskfile.dev/#/), including building,
    serving, updating the Docker image, linting (YAML and Markdown), and checking links.
* `.pre-commit-config.yaml`: Configures [pre-commit](https://pre-commit.com/) hooks for linting YAML files
    (`yamllint`), Markdown files (`markdownlint`), and checking links in Markdown files (`markdown-link-check`).
* `.markdownlint.yaml`: Specifies the rules and configurations for `markdownlint`, ensuring consistent Markdown formatting.
* `docs/`: This directory contains all the Markdown files that constitute the actual notes and documentation.
* `.github/workflows/ci.yaml`: Defines the GitHub Actions workflow for continuous integration, specifically for
    deploying the documentation to GitHub Pages on pushes to the `main` branch.

## Usage

* **Serving Locally:** To run a local development server for the documentation, use the command defined in `Taskfile.yml`:

    ```bash
    task serve
    ```

    This will typically make the documentation available at `http://0.0.0.0:8000`.
* **Building Documentation:** To build the static HTML documentation, use:

    ```bash
    task build
    ```

* **Linting:** To lint the project (YAML, Markdown, and link checking), use:

    ```bash
    task lint
    ```

    Individual linting tasks are also available: `task yamllint`, `task markdownlint`, `task linkcheck`.
* **Pre-commit Hooks:** The project uses pre-commit hooks to automatically run linters and link checks before
    commits. These are configured in `.pre-commit-config.yaml`.
