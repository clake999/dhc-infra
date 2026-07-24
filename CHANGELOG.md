# Changelog

All notable released changes to `dhc-infra` are documented here.

## [Unreleased]

### Added

- Added the read-only `dhc-system-passport` utility with JSON output for host
  identity, hardware, NVIDIA GPU, storage, network, Docker/containerd, and
  `dhc-infra` repository state.
- Added resilient collection when optional commands, services, or hardware are
  unavailable.
- Added System Passport tests for JSON validity, required sections, missing
  optional commands, and read-only operation.

### Completed

- Completed the v0.3.0 System Passport implementation and its first production
  deployment on Argus.
- Completed Argus R-001 validation for persistent NAS access, Docker and
  containerd, NVIDIA GPU containers, System Passport JSON, and archived-passport
  integrity across reboot.
- Archived the official Argus passport with SHA-256
  `024ef1861797f37b6d6db3d038bafdc50d331323a974cebc426255155d4ea82c`.
- Documented that `/var/lib/docker` and `/var/lib/containerd` contain only
  expected small runtime metadata and are intentionally retained.

## [v0.2.0] - 2026-07-23

### Added

- Added the configurable `dhc-mount-nas` utility.
- Added support for overriding the default configuration path with
  `DHC_INFRA_CONFIG`.
- Added an example NAS configuration in `config/dhc-infra.conf.example`.
- Added validation for required settings, root execution, host commands, and
  credentials file permissions.
- Added safe handling for an already-mounted expected share and rejection of a
  mount point occupied by a different source.
- Added post-mount filesystem-type and read/write verification.

## [v0.1.0] - 2026-07-23

### Added

- Created the initial repository scaffold.
- Established the shared infrastructure-tooling purpose and design direction.
