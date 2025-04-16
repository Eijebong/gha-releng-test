# Mozilla RelEng github actions

This repository contains a few github actions used across repositories in the `mozilla-releng` organization.

## Actions

### pre-commit

This is a simple action to run pre-commit hooks

#### Example

```yaml
name: Pre-commit
on:
  - push
jobs:
  pre-commit:
    name: Run pre-commit hooks
    runs-on: ubuntu-latest
    steps:
      - uses: mozilla-releng/actions/pre-commit@main
```

### pre-commit-autoupdate

This is an action to run `pre-commit autoupdate`, push the result to a branch and open a PR for the changes if necessary

#### Inputs

- token: A token that has write access to the repository

#### Example

```yaml
name: Auto update pre-commit hooks every month
on:
  schedule:
    - cron: '0 0 1 * *'
jobs:
  pre-commit:
    name: Pre-commit
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
    steps:
      - uses: mozilla-releng/actions/pre-commit-autoupdate@main
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```
