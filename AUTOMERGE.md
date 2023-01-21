# Merge pull requests from Renovate automatically under secure settings

In this document, we describe how to set up CI to merge pull requests from Renovate automatically under secure settings.

## Goals

- Merge pull requests from Renovate automatically
- Forbid users to merge changes without reviews

## Secure Settings

Set up branch protections.

- `main`
  - `Require a pull request before merging`
    - `Require approvals` (1 approval)
    - `Dismiss stale pull request approvals when new commits are pushed`
    - `Require review from Code Owners`
    - `Require approval of the most recent reviewable push`
  - `Require status checks to pass before merging`
    - `Status checks that are required.`: `status-check`
  - `Do not allow bypassing the above settings`
- `renovate/*` 
  - `Do not allow bypassing the above settings`
  - `Restrict who can push to matching branches`
    - `Restrict pushes that create matching branches`
      - `renovate`
      - `aqua-update-checksum-renovatepush` (GitHub App)
  - `Allow deletions`

## Repository Setting

- Allow auto-merge

## GitHub Apps

Create two GitHub Apps and install them to a repository.

- `aqua-update-checksum-push`
  - Use for pull requests from other than Renovate
  - Permissions
    - `contents: write`: Update `aqua-checksums.json` and push a commit to a pull request
- `aqua-update-checksum-renovatepush`
  - Use for pull requests from Renovate
  - Permissions
    - `contents: write`
      - Update `aqua-checksums.json` and push a commit to a pull request
      - Enable automerge
    - `pull-requests: write`: Enable Automerge

## fine-grained personal access token

Create a [fine-grained personal access token](https://github.blog/2022-10-18-introducing-fine-grained-personal-access-tokens-for-github/) to approve pull requests from Renovate automatically.

- permissions:
  - `pull-requests: write`

The owner of the access token must be a member of the organization, have a write permission, and a codeowner of the repository.

## Repository Secrets

Create Repository Secrets.

- `APP_ID`: GitHub App ID of `aqua-update-checksum-push`
- `APP_PRIVATE_KEY`: GitHub App Private Key of `aqua-update-checksum-push`

## GitHub Environment

Create a [GitHub Environment](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment).

- `renovate`
  - deployment branch rule: `renovate/*`
  - Secrets
    - `APP_ID`: GitHub App ID of `aqua-update-checksum-renovatepush`
    - `APP_PRIVATE_KEY`: GitHub App Private Key of `aqua-update-checksum-renovatepush`
    - `GH_TOKEN_APPROVE_RENOVATE_PR`: fine-grained personal access token

## GitHub Actions Workflow

Create two workflows.

- [test](.github/workflows/test.yaml)
- [renovate](.github/workflows/renovate.yaml)
