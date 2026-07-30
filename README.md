# Hanzo AML

Real-time AML/CFT transaction monitoring, sanctions screening and case management —
the Hanzo-branded deployment of the canonical [`luxfi/aml`](https://git.hanzo.ai/luxfi/aml)
engine, the way `hanzoai/kms` is the Hanzo deployment of `luxfi/kms`.

All engine logic lives in `github.com/luxfi/aml`. This repository pins an engine
version, publishes the image to Hanzo's registries, and carries the Hanzo
deployment's configuration. The binary itself is brand-neutral: it white-labels by
request host (Lux on `lux.network`, Hanzo on `hanzo.ai`, Zoo on `zoo.ngo`) and
validates every token against that host's brand issuer, so one image serves the
Hanzo surface at `api.hanzo.ai`.

## Deployment shape

One deployment per institution: its own store, its own IAM application
(`AML_CLIENT_ID` — the audience every token is pinned to), its own ingress host.
Per-brand stores make a cross-brand tenant collision structurally impossible
rather than merely guarded.

- Canonical source: `git.hanzo.ai/hanzoai/aml` (this repo), mirrored to GitHub.
- Image: `ghcr.io/hanzoai/aml` (canonical mirror `oci.hanzo.ai/hanzoai/aml`).
- Engine module: `github.com/luxfi/aml` at the pinned `ENGINE_VERSION`.
