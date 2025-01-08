# HeyPongo Reusable Workflows

This repository contains reusable GitHub Actions workflows for HeyPongo projects.

## Release Label Workflow

This workflow automatically manages a `release` branch based on labeled Pull Requests.

### Features

- Creates/updates a `release` branch based on `dev`
- Automatically cherry-picks commits from PRs with the "release" label
- Automatic conflict handling
- Automatic PR comments indicating success or failure

### Installation

1. In your project, create the file `.github/workflows/update-release.yml` with the following content:

```
name: Update Release Branch

on:
  pull_request_target:
    types: [labeled, unlabeled, synchronize, opened]

jobs:
  call-update-release:
    uses: heypongo/heypongo-workflow/.github/workflows/release-label.yml@main
    secrets:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Usage

1. Create your Pull Requests normally targeting the `dev` branch
2. Add the `release` label to PRs you want to include in the next release
3. The workflow will:
   - Trigger automatically when the label is added/removed
   - Recreate the `release` branch from `dev`
   - Add commits from labeled PRs
   - Comment on the PR to indicate success or failure

### Prerequisites

- A `dev` branch as the main development branch
- GitHub Actions enabled in your repository
- Write permissions for the GitHub token

### Troubleshooting

If the workflow fails:
1. Check the workflow logs in GitHub Actions
2. Verify that there are no merge conflicts
3. Ensure the PR is targeting the `dev` branch
4. Make sure the GitHub token has sufficient permissions

### Contributing

Feel free to open issues or submit pull requests if you find any bugs or have suggestions for improvements.

### License

MIT License - feel free to use this workflow in your own projects.