# Google Cloud Firestore and Datastore Documentation Mirror

This repository provides a local Markdown mirror of official Google Cloud documentation for **Cloud Firestore (Native and Datastore mode)**. It is designed to be automatically updated via GitHub Actions.

## API Key Setup

This tool requires a Google Cloud API Key with access to the **Developer Knowledge API**.

### 1. Create the API Key

You can create a restricted API key using the `gcloud` CLI:

```bash
gcloud services api-keys create \
    --project=your-project-id \
    --display-name="Developer Knowledge API Key" \
    --api-target=service=developerknowledge.googleapis.com
```

### 2. Configure GitHub Secrets

#### Via Web Interface
1.  Copy the generated API key.
2.  In your GitHub repository, go to **Settings** -> **Secrets and variables** -> **Actions**.
3.  Add a **New repository secret**:
    *   Name: `DEVELOPERKNOWLEDGE_API_KEY`
    *   Value: (Your API key)

#### Via GitHub CLI (`gh`)
If you have the `gh` CLI installed, you can set the secret directly:

```bash
gh secret set DEVELOPERKNOWLEDGE_API_KEY --body "YOUR_API_KEY"
```

## Manual Run

If you have Go installed locally, you can run the mirror script manually:

```bash
export DEVELOPERKNOWLEDGE_API_KEY=your_api_key
./mirror.sh
```

## Credits

This mirror system is powered by [gcp-docs-mirror-tools](https://github.com/apstndb/gcp-docs-mirror-tools).

## License

The documentation content collected in this repository is mirrored from Google Cloud Documentation according to the [Google Developers Site Policies](https://developers.google.com/terms/site-policies).
- Documentation content is licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- Code samples are licensed under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0).
