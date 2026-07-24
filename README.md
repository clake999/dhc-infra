# DHC Infrastructure (`dhc-infra`)

Shared Linux infrastructure utilities for the DieHardCards ecosystem.

## Project purpose

`dhc-infra` provides reusable tooling for preparing, identifying, operating,
and recovering DHC hosts. It centralizes host-level tasks shared by application
servers, stations, AI/GPU systems, and development workstations.

The latest tagged release is **v0.2.0**. The System Passport implementation and
its first production deployment are complete for v0.3.0. Other utility files in
the repository remain placeholders for later milestones.

## Design philosophy

**Build once. Manage everywhere.** Utilities should be portable, focused, easy
to audit, explicitly configured, safe to repeat where practical, and clear when
they fail. They should provide human-readable output and, where appropriate,
machine-readable data. Credentials and other secrets stay outside the repository.

## Supported host types

- DHC application and web servers
- DHC Station hosts, including Hans, Holly, and Theo
- AI and GPU servers, including Argus
- Linux development and administrative workstations

Support is currently aimed at Linux hosts with Bash and standard GNU/Linux
administration tools. Individual utilities may require additional packages.

## Repository layout

```text
.
├── config/       Example host configuration
├── docs/         Architecture and utility documentation
├── scripts/      Released utilities and planned placeholders
├── templates/    Data and report templates
├── CHANGELOG.md  Released changes
├── ROADMAP.md    Project direction and milestones
└── README.md      Project overview
```

## Installation philosophy

Installation is explicit and host-controlled. Administrators should review a
utility and its configuration, install only what a host needs, and keep
site-specific settings under `/etc`. Runtime credentials must be stored
separately with restrictive permissions.

The repository does not yet provide a released automated installer.
`scripts/install.sh` is a placeholder. Until an installer is released, follow
the documentation for each utility.

## Current utilities

### `dhc-mount-nas`

Available in v0.2.0. This root-operated utility reads NAS settings from
`/etc/dhc-infra.conf` by default, validates its configuration and credentials,
safely mounts a CIFS share, and verifies read/write access. It requires the
credentials file to have permissions `0600` and refuses to replace a mount point
occupied by another source.

See [NAS mounting](docs/nas.md) and the
[configuration reference](docs/configuration.md).

The optional `DHC_NAS_UID` and `DHC_NAS_GID` settings control ownership of
files exposed through the CIFS mount. If omitted, the utility uses
`SUDO_UID`/`SUDO_GID` when run through `sudo`; otherwise, both values default
to `1000`.

### `dhc-system-passport`

Complete for v0.3.0 and deployed on Argus at
`/usr/local/bin/dhc-system-passport`. This read-only utility emits a JSON
inventory to stdout covering identity, hardware, NVIDIA GPUs, storage and NAS
state, networking, Docker and containerd, and the local `dhc-infra` checkout.
It runs without `sudo`, tolerates unavailable hardware and optional host
commands, and sends collection warnings to stderr.

```bash
scripts/dhc-system-passport > passport.json
```

See [System Passport](docs/passport.md) for its schema and collection behavior.

## Planned utilities

- Docker / GPU bootstrap tooling (v0.4.0)
- `dhc-health` — run host and service diagnostics (v0.5.0)
- Backup and recovery tooling (v0.6.0)
- `install.sh` — provide a reviewed installation entry point as the toolkit matures

Placeholder files are not released utilities and should not be installed or
relied upon.

## Version roadmap

| Version | Milestone | Status |
| --- | --- | --- |
| v0.1.0 | Repository scaffold | Complete |
| v0.2.0 | NAS mount utility | Complete and deployed |
| v0.3.0 | System Passport | Complete |
| v0.4.0 | Docker / GPU bootstrap | Planned |
| v0.5.0 | Health and diagnostics | Planned |
| v0.6.0 | Backup and recovery | Planned |
| v1.0.0 | Production infrastructure toolkit | Planned |

See [ROADMAP.md](ROADMAP.md) for milestone details.

## Argus R-001

Argus R-001 is complete. The Ubuntu 26.04 LTS GPU host passed pre- and
post-reboot validation for the persistent CIFS NAS mount and write access,
Docker and containerd with their `/srv/docker` data roots, NVIDIA RTX 5080
access from Docker, System Passport JSON generation, and archived-passport
integrity.

The official passport is
`/mnt/dhc-nas-01/infrastructure/passports/argus/argus-2026-07-24-113142.json`
with SHA-256
`024ef1861797f37b6d6db3d038bafdc50d331323a974cebc426255155d4ea82c`.
Its pre- and post-reboot hashes matched. See the
[Argus R-001 closeout](docs/argus-r001.md) for the complete verified record.

## Relationship to other DHC repositories

- **`dhc`** is the core DHC application. `dhc-infra` supplies reusable host
  infrastructure around it rather than application features.
- **`dhc-station`** contains station-specific software and workflows.
  `dhc-infra` supplies host setup and operational utilities shared by stations.
- **`diehardcards-www`** contains the public website. `dhc-infra` may support
  its Linux hosts, but website content and application code remain there.

This separation keeps product code in product repositories and portable
machine-management tooling in `dhc-infra`.

## Documentation

- [Argus R-001 closeout](docs/argus-r001.md)
- [Architecture](docs/architecture.md)
- [Configuration](docs/configuration.md)
- [NAS mounting](docs/nas.md)
- [System Passport](docs/passport.md)
- [Changelog](CHANGELOG.md)
- [Roadmap](ROADMAP.md)
