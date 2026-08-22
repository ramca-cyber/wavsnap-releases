# WavSnap release contract

This repository is the canonical customer-facing release index even though each edition uses its natural delivery channel.

## Canonical record

Every stable product version receives one GitHub release tagged `v<version>`. The release record contains:

- customer-facing release notes;
- the exact source commit used by every selected edition;
- a human-readable `RELEASE-METADATA.txt` summary;
- a machine-readable `RELEASE-METADATA.json` manifest;
- `SHA256SUMS.txt` for attached assets;
- release-specific third-party notices;
- Windows installers and signing evidence when Windows Desktop is selected;
- pointers to the verified Hosted Web deployment and Docker image when those editions are selected.

The JSON manifest and versioned Docker deployment bundle are guaranteed for releases created after this multi-edition contract was adopted. Earlier release records may contain only the human-readable metadata available at their publication time.

## Delivery locations

| Edition | Canonical artifact location |
| --- | --- |
| Hosted Web | URL recorded in the release manifest |
| Windows Desktop | Assets attached to the GitHub release |
| Self-hosted Docker | `ghcr.io/ramca-cyber/wavsnap` tags recorded in the release manifest |
| Future editions | Location declared by a new manifest edition entry |

Keeping container layers and hosted deployments out of the Git repository avoids duplicating artifacts while this repository remains the place users discover, install, verify, and update every edition.

## Machine-readable metadata

`RELEASE-METADATA.json` has an integer `schemaVersion`, product version, source commit, release URL, and an `editions` object. Each edition entry declares whether it was released and includes edition-specific locations and platform information.

Consumers must:

- ignore unknown edition keys and unknown properties;
- treat a missing or `released: false` edition as unavailable for that version;
- use an exact versioned artifact or image when reproducibility matters;
- reject a breaking metadata schema they do not understand.

Adding an edition or an optional property is backward-compatible. A breaking shape change requires a new `schemaVersion`.

## Selective releases

Web, Windows Desktop, and Docker normally share one version, but the coordinated workflow can release only selected editions. The release manifest is authoritative: it prevents a version number alone from implying that every edition was republished.

Exact version tags are immutable. A correction requires a newer patch release rather than replacement of existing installers or container tags.

## Discover the latest stable release

Humans can use:

<https://github.com/ramca-cyber/wavsnap-releases/releases/latest>

Automation can query GitHub's latest-release API and locate `RELEASE-METADATA.json` in the returned assets:

<https://api.github.com/repos/ramca-cyber/wavsnap-releases/releases/latest>
