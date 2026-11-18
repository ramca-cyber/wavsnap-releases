# WavSnap Releases

This repository is WavSnap's official distribution hub. It contains customer-facing installation instructions, release metadata, checksums, and downloadable installers. WavSnap application source remains in a separate private repository.

For a guided comparison of every edition, visit [wavsnap.com/download](https://wavsnap.com/download).

## Install WavSnap

| Edition | Best for | Install or open | Updates |
| --- | --- | --- | --- |
| Hosted Web | Editing and foreground exports in your browser | [Open the current hosted release](https://wavsnap.com/editor) | Updated centrally after release verification |
| Windows Desktop | Local projects, reusable pipelines, export queues and native rendering | [Download the latest Windows release](https://github.com/ramca-cyber/wavsnap-releases/releases/latest) | Install the newer release over the existing application |

All editions use the portable `.wavsnap` project format. Each environment keeps projects and rendered outputs in storage appropriate to that environment.

### Hosted Web

No installation is required. Keep the editor tab open during exports. Windows provides the persistent export queue; the browser has no queue or CLI. See [the Hosted Web guide](docs/hosted-web.md) for browser storage and project portability details.

### Windows Desktop

The latest release page provides the supported Windows x86_64 installers:

- `WavSnap-<version>-x64-setup.exe` — normal interactive installer
- `WavSnap-<version>-x64.msi` — MSI installer for managed environments

Read the release's signing notice before installing. Unsigned releases are explicitly labeled; Windows or organization policies may warn or block installation. See [the Windows guide](docs/windows-desktop.md).

Docker distribution is retired. The supported editions are Hosted Web and Windows Desktop.

## One release record, multiple delivery channels

Every stable version has one canonical [GitHub release record](https://github.com/ramca-cyber/wavsnap-releases/releases). That record identifies the exact product version and source commit, then lists which editions were released:

- Hosted Web is delivered through WavSnap's production deployment.
- Windows installers are attached directly to the GitHub release.

An edition can be omitted from a particular coordinated release. New coordinated releases attach `RELEASE-METADATA.json` to record exactly what was published and where to find it. See [the release contract](docs/release-contract.md).

## Verify a download

Release assets include `SHA256SUMS.txt`. After downloading an installer, compare its SHA-256 digest before running it.

PowerShell:

```powershell
Get-FileHash .\WavSnap-<version>-x64-setup.exe -Algorithm SHA256
```

Linux or macOS:

```sh
sha256sum WavSnap-<version>-x64-setup.exe
```

Release-specific open-source notices are provided in `THIRD-PARTY-LICENSES.txt`.

## Supported release policy

- Stable versions use tags such as `v0.2.0`.
- Exact installer versions are immutable.
- `latest` means the newest stable release, not a development build.
- The release notes are the authority for edition availability, signing status, storage migrations, and rollback limitations.
- Development snapshots and source builds are not customer release channels.

## Support

For installation, release, or update help, contact `support@wavsnap.com`.
