# thoxkey-releases

[![License](https://img.shields.io/badge/license-THOX%20list%20license-171719)](LICENSE)
[![Last commit](https://img.shields.io/github/last-commit/ttracx/thoxkey-releases?color=171719)](https://github.com/ttracx/thoxkey-releases/commits/main)
[![THOX.ai](https://img.shields.io/badge/THOX.ai-05A451)](https://thox.ai)
![Schema](https://img.shields.io/badge/schema-thoxkey--update--feed%2F1-171719)

**THOX.ai LLC. Your AI. Your Data. Your Rules.™**

The public release list for ThoxKey™ Start, the app on a ThoxKey that starts its model and opens ThoxOS. One file, [`releases.json`](releases.json), names every published ThoxKey Start release: its version, date, release page and the SHA-256 checksum of each file. ThoxKey Start 0.4.2 and later read it when you choose **Check for updates** in ThoxOS, under Devices, **Updates & recovery**. This repository holds the list and its documentation only: no source code and no release files.

## The list

```
https://raw.githubusercontent.com/ttracx/thoxkey-releases/main/releases.json
```

| Version | Computer | Published (UTC) | Release page |
|---|---|---|---|
| 0.4.1 | Windows | 2026-11-10 | [start-windows-v0.4.1](https://github.com/ttracx/thox-key/releases/tag/start-windows-v0.4.1) |
| 0.4.0 | Windows | 2026-11-09 | [start-windows-v0.4.0](https://github.com/ttracx/thox-key/releases/tag/start-windows-v0.4.0) |
| 0.3.1 | Windows | 2026-11-08 | [start-windows-v0.3.1](https://github.com/ttracx/thox-key/releases/tag/start-windows-v0.3.1) |

The release pages and their files live in the private `ttracx/thox-key` repository and open with a GitHub account that has access to it. The list itself opens for anyone.

## Quick start

Read the list and check a downloaded file against it:

```sh
curl -fsSL https://raw.githubusercontent.com/ttracx/thoxkey-releases/main/releases.json -o releases.json
python3 -c "import json; print([(r['host'], r['version']) for r in json.load(open('releases.json'))['releases']])"
shasum -a 256 Start-ThoxKey.exe
```

The last line must print the `sha256` listed for that file under its version. Step by step, including Windows: [docs/QUICKSTART.md](docs/QUICKSTART.md).

## Repository layout

| Path | What it is |
|---|---|
| `releases.json` | The release list (schema `thoxkey-update-feed/1`) |
| `docs/USER_GUIDE.md` | What the list is for, verifying a download, updating a key, questions |
| `docs/QUICKSTART.md` | Check a file against the list in five minutes |
| `docs/FORMAT.md` | Every field and rule of `releases.json` |
| `docs/DEVELOPMENT.md` | How entries are added and checked, known limits |
| `LICENSE`, `NOTICE.md` | Terms of use and the THOX.ai LLC notice |

## Documentation

- [User guide](docs/USER_GUIDE.md)
- [Quick start](docs/QUICKSTART.md)
- [List format](docs/FORMAT.md)
- [Development](docs/DEVELOPMENT.md)

## Releases

This repository has no releases of its own. ThoxKey Start releases are published at [ttracx/thox-key releases](https://github.com/ttracx/thox-key/releases) and listed in `releases.json` only after they are published.

## Maintainers

THOX.ai adds an entry when a ThoxKey Start release is published, after checking every listed checksum against the release's own files. See [docs/DEVELOPMENT.md](docs/DEVELOPMENT.md).

## License and notice

Use of the list is governed by [LICENSE](LICENSE). Copyright, trademarks and the THOX.ai LLC intellectual property notice: [NOTICE.md](NOTICE.md). Report a security issue to security@thox.ai, not in a public issue.
