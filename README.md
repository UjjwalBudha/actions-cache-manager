# GitHub Actions Cache Manager

Selectively cleans old GitHub Actions caches while preserving recent ones. This action helps you stay within the 10GB cache limit by removing outdated caches based on count or age.

## Usage

### Example Workflow

```yaml
name: Clear all Github actions caches on sundays
on:
  schedule:
    - cron: "0 0 * * 0"
  workflow_dispatch:

jobs:
  my-job:
    name: Delete all caches
    runs-on: ubuntu-20.04

    steps:
      - name: Clear caches
        uses: UjjwalBudha/actions-cache-manager@main
        with:
          dry-run: 'true'

### Permissions

If your workflow explicitly defines `permissions`, you must include `actions: write`:

```yaml
permissions:
  actions: write
  contents: read # Required for actions/checkout
```
```

### Inputs

```yaml
  github-token:
    description: 'Your GITHUB_TOKEN.'
    required: false
    default: ${{ github.token }}
  dry-run:
    description: 'List caches only, do not clear them.'
    required: false
    default: 'false'
  keep-recent:
    description: 'Number of recent caches to keep (sorted by creation date).'
    required: false
    default: '5'
  older-than-days:
    description: 'Delete caches older than this many days.'
    required: false
    default: ''
  page-size:
    description: 'Page size for cache listing.'
    required: false
    default: '100'
```
