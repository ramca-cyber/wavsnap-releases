# Self-hosted Docker

The official Docker edition is a Linux AMD64 image published at `ghcr.io/ramca-cyber/wavsnap`. It provides the WavSnap editor plus a persistent server workspace for projects and rendered outputs. It does not require the private application source repository.

## Requirements

- Docker Engine with the Compose v2 plugin
- Linux AMD64 host, virtual machine, or compatible Docker environment
- persistent disk space for projects, media, and outputs
- a strong access token

The container image must be public before anonymous customers can pull it. Until package visibility is changed, authorized GitHub credentials with package-read access are required.

## Install

Download this [`docker/`](.) directory or clone the small release repository, then enter the directory:

```sh
git clone https://github.com/ramca-cyber/wavsnap-releases.git
cd wavsnap-releases/docker
cp .env.example .env
```

Generate a strong token:

```sh
openssl rand -hex 32
```

Put the generated value in `.env` as `WAVSNAP_SERVER_TOKEN`, then start WavSnap:

```sh
docker compose pull
docker compose up -d
docker compose ps
```

Open `http://localhost:3000/workspace` and enter the same token.

PowerShell users can create the configuration with:

```powershell
Copy-Item .env.example .env
$bytes = New-Object byte[] 32
[Security.Cryptography.RandomNumberGenerator]::Fill($bytes)
[Convert]::ToHexString($bytes).ToLowerInvariant()
```

## Choose a version

`.env.example` follows `latest`, which tracks the newest stable Docker release. For a reproducible deployment, set an exact image instead:

```dotenv
WAVSNAP_IMAGE=ghcr.io/ramca-cyber/wavsnap:0.1.1
```

Release pages record every published Docker tag. Linux AMD64 is the only supported container platform until another platform is explicitly listed in release metadata.

## Storage

The application container is disposable. Durable state lives in the Compose-managed `wavsnap-data` volume mounted at `/data`:

- `/data/projects` contains managed projects;
- `/data/outputs` contains server-managed rendered outputs;
- other runtime-managed workspace data remains under `/data`.

Portable `.wavsnap` archives remain the recommended way to move individual projects between editions. Back up the Docker volume separately for full-workspace recovery.

## Update

Read the target release notes for storage migrations and rollback limitations, then run:

```sh
docker compose pull
docker compose up -d
docker compose ps
```

Compose replaces the application container and retains the data volume.

## Back up the workspace

Stop WavSnap before taking a consistent volume archive:

```sh
docker compose stop
docker run --rm -v wavsnap_wavsnap-data:/data:ro -v "$PWD:/backup" alpine \
  tar czf /backup/wavsnap-data-backup.tgz -C /data .
docker compose start
```

The default Compose project name is `wavsnap`, producing the volume `wavsnap_wavsnap-data`. Confirm the actual name with `docker volume ls` if Compose was launched with a different project name.

Keep backups outside the Docker volume and test restoration before relying on them.

## Roll back the application

Set `WAVSNAP_IMAGE` in `.env` to a preceding exact version and run:

```sh
docker compose pull
docker compose up -d
```

Rolling back the image does not roll back workspace data. Do not roll back across an incompatible storage migration unless the release notes explicitly permit it or you are restoring a compatible backup.

## Network exposure

The default Compose file publishes port 3000 on the Docker host. A token is mandatory, but an internet-facing installation should additionally use TLS through a trusted reverse proxy or private network and restrict inbound access with a firewall.

Change `WAVSNAP_PORT` in `.env` if port 3000 is already used. Never commit `.env`; it contains the workspace access token.

## Troubleshooting

```sh
docker compose ps
docker compose logs --tail=200 wavsnap
docker compose config
```

The image includes a health check. A container that repeatedly restarts commonly indicates a missing access token, inaccessible storage, or an incompatible host architecture.

For release-specific problems, contact `support@wavsnap.com` and include the exact image tag, host architecture, and relevant container logs. Do not send access tokens.
