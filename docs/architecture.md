# Architecture

`dhc-infra` is the host-infrastructure layer shared by the DieHardCards
ecosystem. Product repositories retain application code and product-specific
workflows; this repository contains portable Linux operations useful across
multiple DHC host types.

It covers reusable host tasks such as storage mounts, system inventory,
bootstrap checks, diagnostics, and recovery support. Host configuration and
credentials live outside the repository, normally under `/etc`.

## Utility and deployment boundaries

The NAS utility owns safe, verified on-demand CIFS mounting. A host may invoke
it through host-managed service configuration for boot persistence. The System
Passport is a read-only observer: it reports host and repository state without
changing mounts, services, Docker, hardware, or Git state.

Argus R-001 is the first completed production validation of these layers. Its
host-specific Docker, containerd, NVIDIA runtime, systemd, storage, and archive
configuration remains operational state rather than portable application code.
The reusable cross-host Docker/GPU bootstrap remains a later roadmap milestone.

On Argus, Docker payload storage is rooted at `/srv/docker/docker` and
containerd storage at `/srv/docker/containerd`. The conventional
`/var/lib/docker` and `/var/lib/containerd` directories were inspected and
contain only expected small runtime metadata; they are intentionally retained.

Only utilities identified as current in the [README](../README.md) and
[changelog](../CHANGELOG.md) should be treated as released or completed. See the
[roadmap](../ROADMAP.md) and [Argus R-001 closeout](argus-r001.md).
