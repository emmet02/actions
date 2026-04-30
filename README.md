# Antigravity Custom Actions

This repository is dedicated to storing **Custom GitHub Actions** used across the Antigravity ecosystem.

## 🏗 Workflow vs. Action: Where does it go?

### 📁 `emmet02/actions` (This Repo)
Use this repository for **Custom Actions** (building blocks).
- **Composite Actions**: Bundled steps (`action.yml`).
- **JavaScript Actions**: Logic written in Node.js.
- **Docker Actions**: Logic containerized for consistency.
- **Note**: This repository should **not** contain `.github/workflows/` meant for other repositories.

### 📁 `emmet02/.github`
Use the `.github` repository for **Reusable Workflows** (the blueprints).
- **CI/CD Pipelines**: (`ci.yml`, `release.yml`).
- **Scheduled Tasks**: (`cleanup.yml`).
- **Global Config**: (`CODEOWNERS`, default templates).

---

## 🚀 How to use an action from this repo
In your workflow, reference a custom action from this repo like this:

```yaml
steps:
  - name: Use My Custom Action
    uses: emmet02/actions/my-action-folder@main
    with:
      input-param: "value"
```

---

*Standardized and maintained by Antigravity AI.*
