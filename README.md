# Typesake release records

Typesake is a PDF editor that runs in your browser: your documents are never uploaded. This repository
lets anyone check that the site keeps serving the code it says it serves.

Each file in `releases/` is named after a release (`<version>.json`) and lists every file that release
serves, with its SHA-256 fingerprint:

```json
{ "version": "fb05555a2da8", "build": "f3e2a29ad45d", "files": { "/assets/app-….js": "sha256-…", … } }
```

A record is added here every time the site is updated, and records are never edited afterwards; the git
history shows when each one was published. There is no source code here, only these lists.

## How to check the live site

1. See which release the site is serving now: open `https://typesake.com/release.json`. Its `version` should
   match a file in `releases/`, and its list should be identical to that file.
2. Download any file the list names and compare its fingerprint, for example:

   ```sh
   curl -s https://typesake.com/assets/app-DgRCvdqO.js | openssl dgst -sha256 -binary | base64
   ```

   The result, with `sha256-` in front, must equal the value in the record.

If the site serves a file that is not in the record, or a file whose fingerprint differs, the site is not
running the release it claims. Please tell us at hello@typesake.com.
