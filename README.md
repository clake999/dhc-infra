# DHC Infrastructure (`dhc-infra`)

Shared Linux infrastructure utilities for the DieHardCards ecosystem.

## Project purpose

`dhc-infra` provides reusable tooling for preparing, identifying, operating,
and recovering DHC hosts. It centralizes host-level tasks shared by application
servers, stations, AI/GPU systems, and development workstations.

The repository is currently at **v0.2.0**. The NAS mount utility is the first
deployed utility; other utility files in the repository are planned placeholders.

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

## Planned utilities

- `dhc-system-passport` — create a host System Passport (v0.3.0)
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
| v0.3.0 | System Passport | Planned |
| v0.4.0 | Docker / GPU bootstrap | Planned |
| v0.5.0 | Health and diagnostics | Planned |
| v0.6.0 | Backup and recovery | Planned |
| v1.0.0 | Production infrastructure toolkit | Planned |

See [ROADMAP.md](ROADMAP.md) for milestone details.

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

- [Architecture](docs/architecture.md)
- [Configuration](docs/configuration.md)
- [NAS mounting](docs/nas.md)
- [System Passport](docs/passport.md)
- [Changelog](CHANGELOG.md)
- [Roadmap](ROADMAP.md)
