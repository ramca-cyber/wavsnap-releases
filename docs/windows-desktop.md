# Windows Desktop

WavSnap Desktop currently supports Windows x86_64. Download installers only from the [latest official WavSnap release](https://github.com/ramca-cyber/wavsnap-releases/releases/latest).

## Choose an installer

- `WavSnap-<version>-x64-setup.exe` is the normal interactive installer.
- `WavSnap-<version>-x64.msi` is available for MSI-based deployment and administration.

Both packages are built from the same coordinated release commit. Their SHA-256 digests are recorded in `SHA256SUMS.txt` on the release page.

## Signing status

Read the release notes and attached signing notice before installation. Until Authenticode signing is configured, an explicitly authorized release may be labeled unsigned. Windows can display **Unknown publisher** or a Microsoft Defender SmartScreen warning for an unsigned build.

Verify the download source and SHA-256 checksum. Organization policy may block unsigned applications; do not change security policy to run WavSnap.

## Included workflows

The Windows app includes reusable export pipelines, a persistent export queue and the bundled `wavsnap.exe` command-line companion. Node and native rendering components are packaged with the app; no separate CLI or Node installation is required.

Keep WavSnap open while app-owned queued jobs run. Closing the app, sleep or shutdown interrupts rendering; unfinished queued outputs can be retried after reopening. A CLI-owned worker can run without an editor window while its process stays running. Schedules and watch folders are not included.

Help includes a two-track release-pack example. Save a pipeline, review audio bindings and source ranges, then reuse it with the next track. Back up portable projects, saved pipelines and source media separately.

## Update

Download the newer installer from the latest release and install it over the existing application. Project and workspace storage are separate from application installation files, but exporting important projects as `.wavsnap` archives before an upgrade remains good practice.

Automatic in-place updating will be documented here only after its signed updater channel is enabled. Until then, GitHub Releases is the update source of record.

## Project portability

Desktop workspaces keep local projects, imported media, and rendered outputs outside the application installation directory. Use portable `.wavsnap` archives to move a project to another WavSnap edition or to retain a separate project backup.
