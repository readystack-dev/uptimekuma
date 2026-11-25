# Provenance — Uptime Kuma (`2.5.12-CE-ubuntu24.04-r3`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/louislam/uptime-kuma
- Revision built: `2.5.12` (commit `5aa5dec425f8a955b54e150636979a6927745ec5`)
- Source tree: `73b080536f01c571cbf987245f40d95aa39befe01bdc293ed5e2ca45ad488107` over 804 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-node`; base image `ubuntu:24.04`
- Built with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795543201` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3` — index digest `sha256:e061a2f4e947d1059dad92ba2581cd308078520c17da69ad1da6186d1b794d4b` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:5ed8ea83cd683f136df4e79cd6e062eebfc1f3b033a97aba145adf9a6845bb1a` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/uptimekuma:2.5.12-CE-ubuntu24.04-r3`

## Pinned inputs, and why

- 24 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 2, image digests 1, language runtimes and toolchains 1, dependency versions readystack sets 12, pins in the kit's dockerfiles 3, readystack's build engine 1, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-uptimekuma-2.5.12-CE-ubuntu24.04-r3.trail.json`, published beside this archive and signed with the release key (`ReadyStack-uptimekuma-2.5.12-CE-ubuntu24.04-r3.trail.json.sigstore`), and readable at https://readystack.dev/products/uptimekuma/trail/2.5.12-CE-ubuntu24.04-r3.

