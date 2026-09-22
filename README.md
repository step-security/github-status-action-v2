[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# GitHub Status Action V2

Adds a status update to a commit. GitHub will always show the latest state of a context.

## Usage

### Inputs

- `authToken` (required)  
  Use secrets.GITHUB_TOKEN or your own token if you need to trigger other workflows that use "on: status"
- `state` (required)  
  The status of the check should only be `success`, `error`, `failure` or `pending`
- `context`  
  The context, is displayed as the name of the check
- `description`  
  Short text explaining the status of the check
- `owner`  
  The repository owner defaults to context github.repository_owner if omitted
- `repository`  
  Repository, default to context github.repository if omitted
- `sha`  
  SHA of commit to update status on, defaults to context github.sha  
  \*If using `on: pull_request` use `github.event.pull_request.head.sha`
- `target_url`  
  Url to use for the details link. If omitted no link is shown.

## Example

```yml
name: "test"

on: # run on any PRs and main branch changes
  pull_request:
  push:
    branches:
      - main

permissions:
  statuses: write

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7

      - name: Run the action
        uses: step-security/github-status-action-v2@v1
        with:
          authToken: ${{secrets.GITHUB_TOKEN}}
          context: "Test run"
          description: "Passed"
          state: "success"
          sha: ${{github.event.pull_request.head.sha || github.sha}}
```

## Permissions Settings for GitHub Actions

With the introduction of the `permissions` block in GitHub Actions, it is crucial to configure the necessary permissions for your workflows to function correctly. Below is a guide to help you set up the permissions securely and effectively.

### Required Permissions

Refer to the [GitHub documentation](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/controlling-permissions-for-github_token) for a detailed list of available permissions.
