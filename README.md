# save-secret-file

Save a secret to a file during CI. Supports both base64-encoded secrets (default) and raw plaintext secrets (e.g. JSON service account keys). Useful for placing sensitive files like `firebase_options.dart`, `google-services.json`, `service-account.json`, etc. during CI.

## Usage

### Base64-encoded secret (default)

```yaml
steps:
  - uses: openci-org/save-secret-file@v1
    with:
      secret: ${{ secrets.FIREBASE_OPTIONS }}
      path: "lib/firebase_options.dart"
```

### Raw content (e.g. JSON stored directly in the secret)

```yaml
steps:
  - uses: openci-org/save-secret-file@v1
    with:
      secret: ${{ secrets.FIREBASE_SERVICE_ACCOUNT }}
      path: "firebase/service-account.json"
      encoding: raw
```

## Inputs

| Input | Description | Required | Default |
|---|---|---|---|
| `secret` | Secret content (base64-encoded by default, or raw when `encoding` is `raw`) | Yes | – |
| `path` | File path to save the content to | Yes | – |
| `encoding` | `base64` (decode before writing) or `raw` (write as-is) | No | `base64` |

## How it works

1. Creates the parent directory if it doesn't exist.
2. Based on `encoding`:
   - `base64`: decodes the secret and writes the decoded bytes to `path`.
   - `raw`: writes the secret content as-is to `path` (no trailing newline is added).

## License

MIT
