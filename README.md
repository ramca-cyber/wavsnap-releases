# WavSnap Releases

Official public distribution channel for WavSnap downloadable release artifacts.

WavSnap application and platform development happens in a separate private source repository. This repository intentionally contains no product source code; it exists only to publish official binaries and release metadata.

## Current release target

The first supported desktop target is **Windows x86_64**.

A normal desktop release may include:

- `WavSnap-<version>-x64-setup.exe` — primary Windows installer (NSIS)
- `WavSnap-<version>-x64.msi` — optional MSI installer
- `SHA256SUMS.txt` — release artifact checksums
- `THIRD-PARTY-LICENSES.txt` — bundled third-party notices
- updater metadata and signatures when automatic updates are enabled

## Future artifacts

This repository may also publish other standalone WavSnap binaries in the future, such as:

- macOS desktop installers
- Linux desktop packages
- standalone WavSnap CLI binaries
- updater artifacts, signatures, checksums, and SBOMs

Node packages are published through npm, container images through GHCR, and the hosted web application through its deployment platform; those artifacts do not belong in this repository.

## Versioning

Release tags follow semantic-style product versions such as:

- `v0.1.0`
- `v0.1.1`
- `v0.2.0`

Pre-release builds may use tags such as `v0.1.0-rc.1`.

## Integrity

Official release assets should be downloaded only from this repository's **Releases** section or from WavSnap-owned download pages that point to these assets.

Published release assets include checksums so downloaded binaries can be verified independently.

## Open-source components

WavSnap includes third-party open-source components such as FFmpeg and whisper.cpp. Release-specific third-party notices are shipped with the application and/or attached to the corresponding release. Exact component versions and source references are maintained as part of WavSnap's release process.

## Support

For WavSnap support or release issues, contact `hello@wavsnap.com`.
