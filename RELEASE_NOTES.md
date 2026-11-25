# Uptime Kuma 2.5.12 — ReadyStack release `2.5.12-CE-ubuntu24.04-r3`

Generated 2026-11-25 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3` (linux/amd64). Index digest `sha256:e061a2f4e947d1059dad92ba2581cd308078520c17da69ad1da6186d1b794d4b` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:5ed8ea83cd683f136df4e79cd6e062eebfc1f3b033a97aba145adf9a6845bb1a` [`TARGET_DIGEST.txt`].
- **Upstream:** Uptime Kuma 2.5.12 built from source at `2.5.12` of https://github.com/louislam/uptime-kuma — upstream notes: https://github.com/louislam/uptime-kuma/releases/tag/2.5.12 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** `ubuntu:24.04`; runtime user `uptimekuma`.
- **Build:** `source-rebuild-node`, built offline with `--network=none`.
- **Supersedes:** ReadyStack release `2.5.12-CE-ubuntu24.04-r2`.

## What changed in this release

- Upstream version unchanged (2.5.12); ReadyStack rebuild.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `@azure/msal-node` at least `7.1.0` (shipped: `7.1.0`)
  - `@grpc/grpc-js` at least `1.13.6` (shipped: `1.13.6`)
  - `glob` at least `11.1.0` (shipped: `11.1.0`)
  - `jsonata` at least `2.2.1` (shipped: `2.2.1`)
  - `lodash` at least `4.18.0` (shipped: `4.18.0`)
  - `minimatch` at least `10.2.3` (shipped: `10.2.3`)
  - `mysql2` at least `3.22.0` (shipped: `3.22.0`)
  - `nodemailer` at least `10.0.6` (shipped: `10.0.6`)
  - `protobufjs` at least `7.6.1` (shipped: `7.6.1`)
  - `tar` at least `7.5.21` (shipped: `7.5.21`)
- Uptime Kuma 2.5.12 is unchanged from the release this supersedes (2.5.12-CE-ubuntu24.04-r2); this release rebuilds it. Changes: libssh-4 moves from 0.10.6-2ubuntu0.5 to 0.10.6-2ubuntu0.6 (USN-9187-1). Settings, ports and data volumes are those of 2.5.12-CE-ubuntu24.04-r2: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-25)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `uptimekuma` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:5ed8ea83cd683f136df4e79cd6e062eebfc1f3b033a97aba145adf9a6845bb1a`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 2 of 2 use cases passed (5 authored, 2 kept in the suite; 3 not exercised, see below) against the running image [`docs/validation/test-results.json`].
- The cases are `GET /api/entry-page` (200), `GET /setup-database-info` (200); the suite checks nothing else.
- 3 further authored checks were not exercised and are not counted above: 3 (`GET /`, `GET /dashboard`, `GET /robots.txt`) were answered with the same page the build's test container served for a made-up path, so they could not show the path exists (listed under Not exercised in `docs/validation/FAILED_TESTS.md`).

## Known issues

- None found (reviewed by held semantic review (Claude) on 2026-11-25).

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

