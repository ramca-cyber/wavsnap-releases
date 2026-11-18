# Hosted Web

The Hosted Web edition runs in a browser and requires no installation. Open the URL listed under **Hosted Web** in the [latest WavSnap release](https://github.com/ramca-cyber/wavsnap-releases/releases/latest).

The current release endpoint is:

<https://wavsnap.com>

Keep the editor tab open during exports. Hosted Web supports foreground exports and has no persistent queue or CLI; use Windows for reusable export pipelines and queued runs.

## Updates

The release process publishes tested Windows downloads before promoting the matching website, then verifies the live version and source commit. Browser users receive the new release on their next load; no local updater is required.

If the editor was already open during a release, finish or save active work and reload before relying on newly announced behavior.

## Projects and media

Browser projects and media stay in browser-origin storage. Clearing site data or using browser cleanup tools can remove that local state. Export important work as a portable `.wavsnap` archive and retain your rendered media separately.

Portable `.wavsnap` archives can be moved between the Hosted Web and Windows Desktop editions when the receiving release supports the archive schema described in its release notes.

## Verify the running version

The deployed edition exposes a version record at:

<https://wavsnap.com/api/version>

The response identifies the edition, product version, and exact release commit.
