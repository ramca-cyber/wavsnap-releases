# WavSnap Releases

This repository is WavSnap's official distribution hub. It contains customer-facing installation instructions, deployment descriptors, release metadata, checksums, and downloadable installers. WavSnap application source remains in a separate private repository.

For a guided comparison of every edition, visit [wavsnap.com/download](https://wavsnap.com/download).

## Install WavSnap

| Edition | Best for | Install or open | Updates |
| --- | --- | --- | --- |
| Hosted Web | Using WavSnap without managing infrastructure | [Open the current hosted release](https://wavsnap.com/editor) | Updated centrally after release verification |
| Windows Desktop | Local projects, native rendering, and offline workflows on Windows x86_64 | [Download the latest Windows release](https://github.com/ramca-cyber/wavsnap-releases/releases/latest) | Install the newer release over the existing application |
| Self-hosted Docker | A persistent WavSnap workspace on your own Linux AMD64 server | [Follow the Docker guide](docker/README.md) | `docker compose pull` followed by `docker compose up -d` |

All editions use the portable `.wavsnap` project format. Each environment keeps projects and rendered outputs in storage appropriate to that environment.

### Hosted Web

No installation is required. The release workflow promotes and verifies the exact application version before the release record becomes final. See [the Hosted Web guide](docs/hosted-web.md) for browser storage and project portability details.

### Windows Desktop

The latest release page provides the supported Windows x86_64 installers:

- `WavSnap-<version>-x64-setup.exe` — normal interactive installer
- `WavSnap-<version>-x64.msi` — MSI installer for managed environments

Read the release's signing notice before installing. Preview releases may be intentionally unsigned until Authenticode signing is enabled. See [the Windows guide](docs/windows-desktop.md).

### Self-hosted Docker

The official image is `ghcr.io/ramca-cyber/wavsnap`. A ready-to-use Compose definition and environment template are maintained in [`docker/`](docker/README.md). Exact semantic-version tags are immutable; `latest` follows the newest stable Docker release.

## One release record, multiple delivery channels

Every stable version has one canonical [GitHub release record](https://github.com/ramca-cyber/wavsnap-releases/releases). That record identifies the exact product version and source commit, then lists which editions were released:

- Hosted Web is delivered through WavSnap's production deployment.
- Windows installers are attached directly to the GitHub release.
- Docker images are delivered through GitHub Container Registry.
- Future editions will be added to the same release record while retaining the delivery mechanism appropriate to that edition.

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

- Stable versions use tags such as `v0.1.1`.
- Exact installer versions and exact container tags are immutable.
- `latest` means the newest stable release, not a development build.
- The release notes are the authority for edition availability, signing status, storage migrations, and rollback limitations.
- Development snapshots and source builds are not customer release channels.

## Support

For installation, release, or update help, contact `support@wavsnap.com`.
