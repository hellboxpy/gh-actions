# gh-actions

Shared GitHub Actions reusable workflows for the hellboxpy organization.

## Workflows

### `publish.yml`

Builds and publishes a Python package to PyPI using
[Trusted Publishing](https://docs.pypi.org/trusted-publishers/) (OIDC — no API
tokens required).

**Usage** — add `.github/workflows/publish.yml` to your package repo:

```yaml
name: Publish

on:
  release:
    types: [published]

permissions:
  id-token: write

jobs:
  publish:
    uses: hellboxpy/gh-actions/.github/workflows/publish.yml@main
```

**PyPI setup** — register each package on PyPI with a Trusted Publisher entry:
- Publisher: GitHub Actions
- Owner: `hellboxpy`
- Repository: `hellbox-{name}`
- Workflow: `.github/workflows/publish.yml`
