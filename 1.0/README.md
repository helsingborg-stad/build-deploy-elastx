# 1.0 deploy action

Build docker image and deploying to Elastx using GHCR

## Parameters

| Parameter name    | Description        | Default | Required | Notes |
| ----------------- | ------------------ | ------- | -------- | ----- |
| JELASTIC_API_KEY  | API key to Elastix |         | true     |       |
| JELASTIC_NODE_ID  | Elastx Node ID     |         | true     |       |
| JELASTIC_ENV_NAME |                    |         | true     |       |
| JELASTIC_TAG      |                    |         | true     |       |
| DOCKER_CONTEXT    |                    |         | true     |       |
| DOCKER_FILE_PATH  |                    |         | true     |       |

## Usage

Example

```yml
name: Build and deploy.

on:
  release:
    types:
      - released
    branches:
      - master

jobs:
  build:
    runs-on: codebuild-f-ai-builder-${{ github.run_id }}-${{ github.run_attempt }}-ubuntu-7.0-medium

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Build & Deploy Elastx
        uses: helsingborg-stad/build-deploy-elastx/1.0@main
        with:
          JELASTIC_API_KEY: ${{ secrets.JELASTIC_API_KEY }}
          JELASTIC_NODE_ID: ${{ vars.JELASTIC_NODE_ID }}
          JELASTIC_ENV_NAME: ${{ vars.JELASTIC_ENV_NAME }}
          JELASTIC_TAG: ${{ vars.JELASTIC_TAG }}
          DOCKER_CONTEXT: ${{ vars.DOCKER_CONTEXT }}
          DOCKER_FILE_PATH: ${{ vars.DOCKER_FILE_PATH }}
```
