# Roadmap

## Repository vision

`dhc-infra` is the shared production infrastructure toolkit for the
DieHardCards ecosystem. It gives DHC application servers, station hosts, AI/GPU
systems, and development workstations a consistent way to install, identify,
validate, maintain, and recover their host infrastructure.

The toolkit complements DHC product repositories. It owns portable host
operations, not application features, station workflows, or website content.

## Design philosophy

**Build once. Manage everywhere.**

Work in this repository should favor:

- portable Linux utilities with minimal, documented dependencies;
- small tools with clear responsibilities and predictable interfaces;
- explicit, external configuration and no committed secrets;
- safe failure modes, actionable diagnostics, and repeatable operation;
- human-readable output plus stable machine-readable output where useful;
- documentation and validation suitable for production operations.

## Supported host types

- DHC application and web servers
- DHC Station hosts
- AI and GPU servers
- Linux development and administrative workstations

Specific distribution, package, hardware, or privilege requirements are
documented per utility as support is implemented.

## Completed milestones

### v0.1.0 — Repository scaffold

Established the repository structure and shared infrastructure-tooling purpose.

### v0.2.0 — NAS mount utility

Delivered and deployed the configurable CIFS mount utility with safe mountpoint
handling and read/write verification.

### v0.3.0 — System Passport

Completed the read-only JSON host inventory, resilient optional collectors,
repository discovery, and automated tests. The first production deployment and
archival workflow were validated on Argus as part of R-001, including successful
post-reboot JSON and archive-integrity checks.

## Completed deployment: Argus R-001

Argus R-001 is complete. The host passed reboot validation for persistent NAS
access, NAS writes, Docker, containerd, the `/srv/docker` data roots, NVIDIA GPU
container access, System Passport JSON, and archived-passport integrity.

This deployment proves the current NAS and System Passport utilities and the
Argus Docker/GPU configuration. It does not by itself complete the reusable
cross-host Docker/GPU bootstrap tooling planned for v0.4.0.

See the [Argus R-001 closeout](docs/argus-r001.md).

## Future milestones

### v0.4.0 — Docker / GPU bootstrap

Standardize prerequisite checks and bootstrap tasks for Docker hosts and
GPU-enabled systems, including hardware-specific requirements.

### v0.5.0 — Health and diagnostics

Add repeatable checks for host resources, required services, mounts, and other
DHC dependencies, with clear results suitable for troubleshooting.

### v0.6.0 — Backup and recovery

Define and automate backup verification, recovery preparation, and documented
restore workflows for supported DHC hosts.

### v1.0.0 — Production infrastructure toolkit

Integrate proven utilities into a documented, stable toolkit with consistent
installation, configuration, output, and operational conventions.

Future milestone scope may be refined as completed utilities are deployed on
additional host types.
