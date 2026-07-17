# validate-multiflexi-app

Reusable GitHub Action that validates `*.multiflexi.app.json` application
definition files against the MultiFlexi application schema, using
[`multiflexi-cli`](https://github.com/VitexSoftware/multiflexi-cli)
(`application:validate-json`) installed from `repo.multiflexi.eu`.

Validation runs against the schema bundled with `multiflexi-cli`
(`php-vitexsoftware-multiflexi-core`), not a URL fetch, so it isn't affected
by schema files moving or 404ing on GitHub raw content.

## Usage

```yaml
name: MultiFlexi JSON Validation

on:
  push:
    paths:
      - 'multiflexi/*.json'
  pull_request:
    paths:
      - 'multiflexi/*.json'

jobs:
  validate-multiflexi-json:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
      - uses: VitexSoftware/validate-multiflexi-app@v1
```

## Inputs

| Name             | Default             | Description                                                             |
|------------------|----------------------|---------------------------------------------------------------------------|
| `path-glob`      | `multiflexi/*.json`  | Glob (relative to repo root) matching app definition files to validate.   |
| `apt-repo-suite` | *(autodetected)*     | Debian/Ubuntu suite for the `repo.multiflexi.eu` apt line. Autodetects via `lsb_release -sc` when unset. |

## Requirements

Runs on Debian/Ubuntu-based runners (`ubuntu-latest` etc.) since it installs
`multiflexi-cli` via apt from `repo.multiflexi.eu`.
