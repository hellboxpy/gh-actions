# gh-actions

Shared GitHub Actions reusable workflows for the hellboxpy organization.

## Workflows

### `test.yml`

Runs the test suite across Python 3.11–3.14 using uv.

```yaml
# .github/workflows/test.yml
name: Tests

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    uses: hellboxpy/gh-actions/.github/workflows/test.yml@main
```

### `release.yml`

Opens and maintains a release PR via
[release-please](https://github.com/googleapis/release-please) on every push to
`main`. When the PR is merged, a GitHub release and git tag are created
automatically.

```yaml
# .github/workflows/release.yml
name: Release Please

on:
  push:
    branches: [main]

permissions:
  contents: write
  pull-requests: write

jobs:
  release-please:
    uses: hellboxpy/gh-actions/.github/workflows/release.yml@main
```

### `publish.yml`

Builds and publishes a Python package to PyPI using
[Trusted Publishing](https://docs.pypi.org/trusted-publishers/) (OIDC — no API
tokens required). Triggered by the GitHub release that release-please creates.

```yaml
# .github/workflows/publish.yml
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
- Workflow filename: `publish.yml`
