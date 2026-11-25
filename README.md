# Uptime Kuma: ReadyStack build kit

The offline build kit for the Docker image `readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [2.5.12-CE-ubuntu24.04-r3](https://github.com/readystack-dev/uptimekuma/releases/tag/2.5.12-CE-ubuntu24.04-r3)
- Image: [`docker.io/readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3`](https://hub.docker.com/r/readystack/uptimekuma/tags), manifest digest `sha256:5ed8ea83cd683f136df4e79cd6e062eebfc1f3b033a97aba145adf9a6845bb1a`
- Product page: https://readystack.dev/products/uptimekuma
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=uptimekuma

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
