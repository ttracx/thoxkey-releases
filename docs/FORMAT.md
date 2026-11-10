# List format: `thoxkey-update-feed/1`

`releases.json` is one JSON object, UTF-8, at most 64 KiB. ThoxKey Start reads it with strict JSON rules: no duplicate keys, no comments, no trailing commas, no `NaN` or `Infinity`. One malformed entry makes ThoxKey Start reject the whole list, so every change is checked before it is pushed.

## Top level

| Field | Type | Rule |
|---|---|---|
| `schema` | string | Exactly `thoxkey-update-feed/1` |
| `channel` | string | `stable` |
| `releases` | array | One object per published release, oldest first, at most 200 |

Unknown fields are ignored by ThoxKey Start.

## Release entry

| Field | Type | Rule |
|---|---|---|
| `host` | string | Computer the release runs on: `windows`, `macos` or `linux` |
| `version` | string | `major.minor.patch`, optionally `-pre`; unique per `host` |
| `tag` | string | `start-<host>-v<version>`, for example `start-windows-v0.4.1` |
| `published` | string | Date the release was published on GitHub, `YYYY-MM-DD`, in UTC |
| `release_url` | string | Exactly `https://github.com/ttracx/thox-key/releases/tag/<tag>` |
| `package_sha256` | string | SHA-256 of the sealed ThoxKey package that carries this release, 64 lowercase hex characters |
| `assets` | array | 1 to 20 objects, one per file on the release page |

Not used: `notes_url`. Release notes stay on the release page.

## Asset

| Field | Type | Rule |
|---|---|---|
| `name` | string | The file name exactly as on the release page: 1 to 120 letters, digits, spaces, `.`, `_` or `-`, no folders; unique within the entry |
| `sha256` | string | SHA-256 of that file, 64 lowercase hex characters |

## How ThoxKey Start uses it

ThoxKey Start keeps the entries for its own `host` and takes the highest `version`. Versions compare as numbers, part by part, and a prerelease (`0.5.0-rc1`) comes before its release (`0.5.0`). If that version is higher than its own, ThoxOS shows it as available and offers its `release_url`. ThoxKey Start downloads and installs nothing.

## Example entry

The real entry for ThoxKey Start 0.4.1 on Windows:

```json
{
  "host": "windows",
  "version": "0.4.1",
  "tag": "start-windows-v0.4.1",
  "published": "2026-11-10",
  "release_url": "https://github.com/ttracx/thox-key/releases/tag/start-windows-v0.4.1",
  "package_sha256": "f9b3e0c57625e3d7d49e5a467ceb809c826eba18dff340a89b1a228f69abde97",
  "assets": [
    {"name": "Start-ThoxKey.exe", "sha256": "e1c95c40df0af7542d347b889846989e7010fb48d16456164c3980154b1e3ce6"},
    {"name": "SHA256SUMS.txt", "sha256": "e286de809733da4e7f76b9f8c6871d6ed70241bc76623a6009331ee65bfd15e4"}
  ]
}
```

## Compatibility

A field may be added without changing `schema`; older ThoxKey Start versions ignore it. Removing or redefining a field needs a new schema name, and a new list file next to this one, so keys already in use keep reading `releases.json`.
