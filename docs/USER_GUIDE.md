# User guide: the ThoxKey Start release list

## What it is

`releases.json` is the list of published ThoxKey™ Start releases. ThoxKey Start is the app on a ThoxKey that inspects the key, asks for your approval, starts the key's model and opens ThoxOS. Each entry in the list names one release: the computer it runs on, its version and date, its release page, the SHA-256 checksum of the sealed ThoxKey package that carries it, and the SHA-256 checksum of every file on the release page.

It is for:

- **ThoxKey owners**, whose ThoxKey Start reads it when they choose **Check for updates**.
- **Anyone verifying a download**, who compares a file's checksum with the list before running it.
- **IT and support staff**, who need a stable place to see which ThoxKey Start version is newest.

The list holds data only. It contains no software and no release files.

## Checking for updates on a key

On ThoxKey Start 0.4.2 or later:

1. Plug in the ThoxKey and start it as usual.
2. In ThoxOS, open **Devices**, then **Updates & recovery**. The panel shows the ThoxKey Start version on the key.
3. Choose **Check for updates**. ThoxKey Start reads this list and compares its own version with the newest one listed for your computer.

| ThoxOS says | Meaning | What to do |
|---|---|---|
| "ThoxKey Start 0.4.3 is available. This key runs 0.4.2." (versions vary) | The list names a newer ThoxKey Start for this computer | Open its release page and follow [Updating a ThoxKey](#updating-a-thoxkey) |
| "This key runs the latest ThoxKey Start for windows (0.4.2)." | No newer version is listed for this computer | Nothing |
| "The release feed lists no ThoxKey Start for linux." | The list has no release for this computer type yet | Nothing yet; the entry appears when that release is published |
| "The release feed could not be read (...)" | No network, or GitHub did not answer | Check the network and try again after a minute |
| "This ThoxKey has no release feed set, ..." | The key's package names no release list | Update by hand once, as below |
| "This ThoxKey Start cannot check for updates; version 0.4.2 adds it." | The key runs ThoxKey Start 0.4.1 or older | Update by hand once, as below |

The check runs only when you choose the button, never on a timer; a second check within a minute shows the first answer again. It sends no key ID, computer ID, cookie or session; it downloads and installs nothing.

## Keys on ThoxKey Start 0.4.1 or older

ThoxKey Start 0.4.1 and older cannot check for updates. The first move to 0.4.2 is manual:

1. Open the [ThoxKey Start releases page](https://github.com/ttracx/thox-key/releases) and download the 0.4.2 release files for your computer.
2. Verify each file's SHA-256 against this list and against the release's `SHA256SUMS.txt` ([quick start](QUICKSTART.md)).
3. Install the sealed ThoxKey package with the THOX provisioner.
4. Plug the key back in and approve it in ThoxKey Start.

From 0.4.2 on, **Check for updates** tells you when the next release is out.

## Updating a ThoxKey

A release is installed on a key only through the sealed ThoxKey package and the THOX provisioner. Do not copy `Start-ThoxKey.exe` or any other file onto the key by hand: the key's package check refuses a ThoxKey Start that was not installed from a sealed package, and the key will not start.

1. Download the release files and verify every SHA-256 ([quick start](QUICKSTART.md)).
2. Install the sealed package with the THOX provisioner. Its checksum is the entry's `package_sha256`.
3. Plug the key back in, review the key ID and fingerprint in ThoxKey Start, and approve it.
4. In ThoxOS, **Updates & recovery** shows the new version.

## Configuration

There is nothing to configure in this repository. A ThoxKey learns the list's address from its sealed package, so the address changes only with a new package. The address is:

```
https://raw.githubusercontent.com/ttracx/thoxkey-releases/main/releases.json
```

## Troubleshooting

| Problem | Cause | Fix |
|---|---|---|
| The release page shows 404 | Release pages are in the private `ttracx/thox-key` repository | Sign in to GitHub with an account that has access, or ask THOX for the files |
| A checksum does not match | The file is damaged or not the published one | Do not run it. Delete it, download again; if it still differs, write to security@thox.ai |
| ThoxOS says the check is not configured | The key's ThoxKey Start is 0.4.1 or older, or its package names no list | Update by hand once, as above |
| ThoxOS says the list could not be read | No network, or GitHub did not answer | Check the network and try again after a minute |
| The key refuses to start after an update | A file was copied by hand | Reinstall the sealed package with the THOX provisioner |

## FAQ

**Why is the list public when the release pages are not?**
So any ThoxKey can check for updates without signing in to anything, and so anyone can verify a file they were given. The list holds versions, dates, links and checksums only.

**Is the list signed?**
No. Its integrity rests on HTTPS to GitHub and on write access to this repository, which only THOX.ai holds. Each entry must point at a release page in `ttracx/thox-key`, and ThoxKey Start opens only `https` links on `github.com`.

**Which computers are covered?**
Windows releases are listed today. Linux and macOS entries appear when those releases are published.

**When does a new release appear?**
After it is published and every checksum in its entry has been checked against the release's own files.
