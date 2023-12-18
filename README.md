# Grit GitHub Action

This action runs the Grit CLI to report any violations of your configured [Grit patterns](https://docs.grit.io/guides/config).

This action will add annotations to the GitHub commit or pull request with any `warning` or `error` patterns that are matched. If any `error` patterns are matched, the action will fail the workflow (exit code 1).

## Usage

You can add it as a step in your GitHub Actions workflow to automatically check for violations on every push:

```
  - name: Grit
    uses: getgrit/github-action-check@v0
    with:
      # Optional additional arguments to pass to the `grit check` command
      args: ''
```

## Inputs

### `args`
Specify [additional arguments](https://docs.grit.io/cli/reference#grit-check) to pass to the `grit check` command.

By default, only warning and error patterns are reported. To include info patterns, use `--level`.

```
  - name: Grit
    uses: getgrit/github-action-check@v0
    with:
      args: '--level info'
```

## Example workflow

```
name: grit-check

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - '*'

jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v4
      - name: grit-check
        uses: getgrit/github-action-check@v0
```

## License
This action code is released under the [MIT License](LICENSE).

The Grit CLI is not included in this repository and is licensed separately.
