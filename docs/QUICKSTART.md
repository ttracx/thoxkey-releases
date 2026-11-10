# Quick start: check a ThoxKey Start file against the list

Five minutes. You need a file from a ThoxKey Start release page (for example `Start-ThoxKey.exe` from [start-windows-v0.4.1](https://github.com/ttracx/thox-key/releases/tag/start-windows-v0.4.1); the release pages need a GitHub account with access to `ttracx/thox-key`).

## 1. Read the list

```sh
curl -fsSL https://raw.githubusercontent.com/ttracx/thoxkey-releases/main/releases.json -o releases.json
python3 -m json.tool releases.json | head -20
```

The file starts with `"schema": "thoxkey-update-feed/1"` and lists each release under `releases`.

## 2. Find the checksum the list gives

```sh
python3 -c "
import json
for r in json.load(open('releases.json'))['releases']:
    for a in r['assets']:
        print(r['host'], r['version'], a['name'], a['sha256'])
"
```

Example line for ThoxKey Start 0.4.1 on Windows:

```
windows 0.4.1 Start-ThoxKey.exe e1c95c40df0af7542d347b889846989e7010fb48d16456164c3980154b1e3ce6
```

## 3. Hash your file and compare

macOS:

```sh
shasum -a 256 Start-ThoxKey.exe
```

Linux:

```sh
sha256sum Start-ThoxKey.exe
```

Windows (PowerShell; this command was not run when this guide was checked): `Get-FileHash .\Start-ThoxKey.exe -Algorithm SHA256`. It prints the checksum in capitals; compare it letter for letter, ignoring case.

The checksum must equal the `sha256` the list gives for that file name under that version. If it differs, do not run or install the file: delete it, download it again from the release page, and if it still differs, write to security@thox.ai.

## 4. Check the release's own checksum file

Each release also carries `SHA256SUMS.txt`. In the folder holding the downloaded files:

```sh
sha256sum -c SHA256SUMS.txt
```

Every line must end in `OK`. The checksum of `SHA256SUMS.txt` itself is in the list too, so step 3 covers it.

## Next

Installing a release on a key: [User guide, updating a ThoxKey](USER_GUIDE.md#updating-a-thoxkey). Every field in the list: [FORMAT.md](FORMAT.md).
