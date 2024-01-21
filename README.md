# create-release-action
Action to create tag and release

### example

```
name: create release

on:
  workflow_dispatch:
    inputs:
      tagname:
        description: "tag name"
        required: true
      releasename:
        description: "release name"
        required: false
      latest:
        description: "mark as latest"
        required: true
        type: boolean
        default: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v3
      - name: create release
        uses: oskarirauta/create-release-action@v1
        with:
          token: ${{ github.token }}
          tag: ${{ inputs.tagname }}
          release: ${{ inputs.releasename }}
          latest: ${{ inputs.latest }}
      - name: show results
        shell: bash
        run: |
          echo "release id: ${{ env.release_id }}"
          echo "assets url: ${{ env.assets_url }}"
          echo "upload url: ${{ env.upload_url }}"
          echo "asset_ids: ${{ env.asset_ids }}"
```
