# neogeek/unity-test-runner

> Test runner for Unity projects

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: neogeek/unity-test-runner@v0
        with:
          # The serial key found at https://id.unity.com/en/subscriptions.
          # Keys are only avalible with a Plus or Pro Subscription.
          #
          # Required
          UNITY_SERIAL: ${{ secrets.UNITY_SERIAL }}

          # Your email address used to log into https://unity.com/
          #
          # Required
          UNITY_USERNAME: ${{ secrets.UNITY_USERNAME }}

          # Your password used to log into https://unity.com/
          #
          # Required
          UNITY_PASSWORD: ${{ secrets.UNITY_PASSWORD }}

          # If the action should cache the installer files.
          #
          # Values: 'true' | 'false'
          # Optional
          CACHE_INSTALLERS: 'true'

          # The directory that contains the Unity project
          #
          # Optional
          WORKING_DIRECTORY: '.'

          # Unity installer hash. See editor installers URLs at
          # https://github.com/neogeek/get-unity/blob/main/data/editor-installers.json
          #
          # Optional
          UNITY_INSTALLER_HASH: '35713cd46cd7'

          # Unity installer version. See editor installers URLs at
          # https://github.com/neogeek/get-unity/blob/main/data/editor-installers.json
          #
          # Optional
          UNITY_INSTALLER_VERSION: '2022.3.4f1'

          # URL for the editor installer. See editor installers URLs at
          # https://github.com/neogeek/get-unity/blob/main/data/editor-installers.json
          #
          # Optional
          UNITY_INSTALLER_URL: 'https://download.unity3d.com/download_unity/35713cd46cd7/LinuxEditorInstaller/Unity.tar.xz'
```

## Scenarios

- [Simple Usage](#simple-usage)

### Simple Usage

**.github/workflows/test.workflow.yml**

```yaml
name: Test

on:
  workflow_dispatch:
  push:
    branches:
      - main

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 30
    if: github.event.pull_request.draft == false

    steps:
      - name: Check out repository
        uses: actions/checkout@v3

      - name: Run Unity tests
        uses: neogeek/unity-test-runner@v0
        with:
          UNITY_SERIAL: ${{ secrets.UNITY_SERIAL }}
          UNITY_USERNAME: ${{ secrets.UNITY_USERNAME }}
          UNITY_PASSWORD: ${{ secrets.UNITY_PASSWORD }}
```
