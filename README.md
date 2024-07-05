# YepCode Copy Team GitHub Action

This repo contains a GitHub Action that copies all the contents from the current git repository to one YepCode remote team.

This ensures seamless data transfer and synchronization between teams. Ideal for managing team migrations, duplicating environments, or maintaining consistent setups across multiple YepCode teams.

## Inputs

```yml
inputs:
  teamSlug:
    description: |
      Remote team slug to push contents. It may be a single string (for https://cloud.yepcode.io teams), or a full URL (for on-premise teams)
    required: true
  clientId:
    description: |
      Team auth Client ID (for oauth, to be used with Client Secret)
  clientSecret:
    description: |
      Team auth Client ID Client Secret (for oauth, to be used with Client ID)
  email:
    description: |
      team auth Email (to be used wi th password)
  password:
    description: |
      team auth Password (to be used with email)
  updateMetadataWithNewRemote:
    description: |
      It 'true', the action will perform a commit in the current repo with the changes in the .'yepcode.json' metadata file. This will allow then to check sync status agains this remote.
    required: false
    default: "false"
```

## Usage

```yml
name: Pull Request
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

jobs:
  linting:
    runs-on: ubuntu-latest
    permissions:
      # Needed if updateMetadataWithNewRemote is enabled
      contents: write
    steps:
      - name: YepCode Copy Team
        uses: yepcode/gha-copy-team@v1
        with:
          teamSlug: your-yepcode-team
          authEmail: yepcode-sync-user-email
          authPassword: yepcode-sync-user-password
```
