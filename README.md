# Bytebase Login Action

Use this action to log in to your Bytebase server in the GitHub CI.

## Usage Example

```yml
on:
  push:
    branches:
      - main
  workflow_dispatch:
  pull_request:

jobs:
  bytebase-ci:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Login Bytebase
        id: bytebase-login
        uses: bytebase/login-action@main
        with:
          bytebase-url: ${{ secrets.BYTEBASE_URL }}
          service-key: ${{ secrets.BYTEBASE_SERVICE_KEY }}
          service-secret: ${{ secrets.BYTEBASE_SERVICE_SECRET }}
      - name: List projects
        run: |
          curl "${{ steps.bytebase-login.outputs.api_url }}/projects" \
            -H 'Authorization: Bearer ${{ steps.bytebase-login.outputs.token }}' \
            -H 'Content-Type: application/json; charset=utf-8'
```

## Outputs

- `token`: Login result, the service account token.
- `api_url`: Bytebase API URL with version.
