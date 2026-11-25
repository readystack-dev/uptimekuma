# Uptime Kuma: ReadyStack build kit

The offline build kit for the Docker image `readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [2.5.12-CE-ubuntu24.04-r3](https://github.com/readystack-dev/uptimekuma/releases/tag/2.5.12-CE-ubuntu24.04-r3)
- Image: [`docker.io/readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3`](https://hub.docker.com/r/readystack/uptimekuma/tags), manifest digest `sha256:5ed8ea83cd683f136df4e79cd6e062eebfc1f3b033a97aba145adf9a6845bb1a`
- Product page: https://readystack.dev/products/uptimekuma
- Source and build recipe: https://readystack.dev/products/uptimekuma/recipe
- Build trail: https://readystack.dev/products/uptimekuma/trail/2.5.12-CE-ubuntu24.04-r3
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=uptimekuma

## The image

Single container. A Node.js (Express + socket.io) self-hosted uptime/status monitor with an embedded SQLite database under /app/data by default. The image IS the complete running instance for that default (no external DB, no sidecar needed). An external MariaDB is technically reachable through environment variables (tested — see Database in the handbooks), but it is not the tested/supported deployment for this release.

## Who uses Uptime Kuma and why

Individuals, small teams and IT administrators who want to know when their websites and services go down.

Uptime Kuma is an easy-to-use, self-hosted monitoring tool. It checks websites, ports, DNS records and containers at short intervals, sends notifications when something fails, and publishes status pages.

A typical use: A small agency hosts websites for its clients. Uptime Kuma checks each site and its certificate, notifies the team by email or chat when one stops responding, and gives each client a status page for their own site.

From the upstream project's own description: https://github.com/louislam/uptime-kuma.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-25 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 99 packages with copyleft licences (GPL, LGPL, MPL), 98 of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`uptimekuma`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-25; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/uptimekuma.

Uptime Kuma is distributed under its upstream licence (MIT); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [2.5.12-CE-ubuntu24.04-r3 release](https://github.com/readystack-dev/uptimekuma/releases/tag/2.5.12-CE-ubuntu24.04-r3): `ReadyStack-uptimekuma-2.5.12-CE-ubuntu24.04-r3.tar.gz` (251.2 MB), SHA-256 `ee2f98c5ddcb25aa092bdacaa83f043c3831c93fe90d31ce2acf6523e5b15d1a`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-uptimekuma-2.5.12-CE-ubuntu24.04-r3.rebuild.json.sigstore ReadyStack-uptimekuma-2.5.12-CE-ubuntu24.04-r3.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-uptimekuma-2.5.12-CE-ubuntu24.04-r3.tar.gz
cd 2.5.12-CE-ubuntu24.04-r3
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-uptimekuma-2.5.12-CE-ubuntu24.04-r3.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/uptimekuma/recipe. The complete kit is the release download. Each release is a tag here.

— ReadyStack · https://readystack.dev
