# GitHub Actions Library

This repository contains a collection of reusable GitHub Actions workflows designed to standardise CI/CD processes across projects, specifically tailored for the **Astral stack** (`uv`, `ruff`, `prek`).

## Workflows

### 1. Prek Autoupdate (`prek-autoupdate.yml`)
Automates the updating of pre-commit hooks using `prek`. If updates are found, it creates a new branch, commits the changes to `.pre-commit-config.yml`, and opens a Pull Request.

- **Trigger**: Intended to be called by a schedule or manual trigger in the target repo.
- **Key Feature**: Uses `uv run --with prek` to avoid polluting the project's permanent dependencies.

### 2. Standard CI (`reusable-ci.yml`)
A standard pipeline for Python projects that performs the following steps:
1. Environments setup via `uv`.
2. Dependency installation via `uv sync`.
3. Linting and hook verification via `prek-action`.
4. Test execution via `pytest`.

---

## Required Repository Settings

To use these workflows (particularly the `prek-autoupdate.yml`) in other repositories, you **must** configure the following settings in the target repository:

### GitHub Actions Permissions
1. Navigate to **Settings** > **Actions** > **General**.
2. Under **Workflow permissions**:
   - Select **Read and write permissions** (required for the bot to push branches and commit changes).
   - Check the box **"Allow GitHub Actions to create and approve pull requests"**.
3. Click **Save**.

### Repository Secrets
For workflows that interact with the GitHub API (like `gh pr create`), ensure the default `GITHUB_TOKEN` has sufficient scopes, or provide a Personal Access Token (PAT) if crossing repository boundaries or triggering further actions.

---

## Usage Example

To consume these workflows in your project, create a file in `.github/workflows/` (e.g., `ci.yml`):

```yaml
jobs:
  call-workflow:
    uses: emmet02/actions/.github/workflows/reusable-ci.yml@main
```

For scheduled updates:

```yaml
jobs:
  autoupdate:
    permissions:
      contents: write
      pull-requests: write
    uses: emmet02/actions/.github/workflows/prek-autoupdate.yml@main
    with:
      branch_name: "bot/prek-autoupdate"
```
