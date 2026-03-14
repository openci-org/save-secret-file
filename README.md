# save-secret-file

Decode a base64-encoded secret and save it to a file. Useful for placing sensitive files like `firebase_options.dart`, `google-services.json`, etc. during CI.

## Usage

```yaml
steps:
  - uses: open-ci-io/save-secret-file@v1
    with:
      secret: ${{ secrets.FIREBASE_OPTIONS }}
      path: "lib/firebase_options.dart"
```

## Inputs

| Input | Description | Required |
|---|---|---|
| `secret` | Base64-encoded file content | Yes |
| `path` | File path to save the decoded content to | Yes |

## How it works

1. Creates the parent directory if it doesn't exist
2. Decodes the base64 content
3. Writes the decoded content to the specified path

## License

MIT
