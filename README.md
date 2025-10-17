<div style="display: flex; align-items: center; justify-content: left; gap: 1rem;">
  <img src="./assets/hmcts-logo.png" alt="HM Courts & Tribunals Service logo" width="120" />
  <h1 style="margin: 0;">🔐 Publish Openapi Spec GitHub Action</h1>
</div>

## 🚀 Usage

```yaml
- uses: hmcts/publish-openapi-spec-to-apihub@main
```
Or the following example will pin to a specific major version:
```yaml
- uses: hmcts/publish-openapi-spec-to-apihub@v1
```

## 📂 Example Workflow

```yaml
on:
  workflow_call:
    secrets:
      SWAGGERHUB_API_KEY:
        required: true
    inputs:
      upload_artifact_name:
        required: true
        type: string
      apihub_owner:
        required: true
        type: string
      api_name:
        required: true
        type: string
      api_version:
        required: true
        type: string
      is_release:
        required: false
        type: boolean
        default: false

jobs:
  Push-API-to-APIHub:
    runs-on: ubuntu-latest
    steps:
      - uses: hmcts/publish-openapi-spec-to-apihub@main
        with:
          swaggerhub_api_key: ${{ secrets.SWAGGERHUB_API_KEY }}
          upload_artifact_name: ${{ inputs.upload_artifact_name }}
          apihub_owner: ${{ inputs.apihub_owner}}
          api_name: ${{ inputs.api_name}}
          api_version: ${{ inputs.api_version}}
          is_release: ${{ inputs.is_release}}
```

### How to Tag
Tag and push the new version via the command line or GitHub UI:
Tag and force push ( override if ex)

```bash
    export VERSION="v1.0.0"
    export VERSIONMAJOR=$(echo $VERSION | cut -f1 -d.)
    git tag $VERSION HEAD
    git push origin $VERSION

    git tag -f $VERSIONMAJOR $VERSION
    git push origin $VERSIONMAJOR --force
```

### Verify

You can verify that `v1` now points to the latest version by visiting:

[https://github.com/hmcts/publish-openapi-spec-to-apihub/tags](https://github.com/hmcts/publish-openapi-spec-to-apihub/tags)

Make sure both the full version tag (e.g., `v1.0.0`) and the floating `v1` tag appear, and that `v1` points to the latest commit.


## License

This project is licensed under the [MIT License](LICENSE).
