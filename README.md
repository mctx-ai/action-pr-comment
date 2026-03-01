# action-pr-comment

Post a comment on a pull request using mctx-bot.

## What It Does

This composite action generates a GitHub App token for mctx-bot, then posts a Markdown comment on a pull request. It is designed to be called from `pull_request` workflows to deliver automated guidance at PR open time.

## Inputs

| Name | Required | Description |
|------|----------|-------------|
| `app-id` | Yes | GitHub App ID for mctx-bot |
| `private-key` | Yes | GitHub App private key for mctx-bot |
| `body` | Yes | Comment body (Markdown) |

## Usage

```yaml
name: PR Comment

on:
  pull_request:
    types: [opened]

permissions:
  pull-requests: write

jobs:
  comment:
    runs-on: ubuntu-latest
    steps:
      - uses: mctx-ai/action-pr-comment@v1
        with:
          app-id: ${{ secrets.MCTX_BOT_APP_ID }}
          private-key: ${{ secrets.MCTX_BOT_PRIVATE_KEY }}
          body: |
            ## Squash Merge Workflow

            This repo uses **squash merging**. Each PR becomes a single commit on `main`.

            **Your PR title becomes the commit subject line.** Keep it under 72 characters and follow [Conventional Commits](https://www.conventionalcommits.org) format:

            ```
            type: short description
            ```

            **Your PR description becomes the commit body.** Use it to explain the why.
```
