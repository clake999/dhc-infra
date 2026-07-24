# Roadmap

## Repository vision

`dhc-infra` will be the shared production infrastructure toolkit for the
DieHardCards ecosystem. It will give DHC application servers, station hosts,
AI/GPU systems, and development workstations a consistent way to install,
identify, validate, maintain, and recover their host infrastructure.

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

Specific distribution, package, hardware, or privilege requirements will be
documented per utility as support is implemented.

## Planned milestones

### v0.3.0 — System Passport

Inventory each host's identity, operating system, hardware, storage, network,
and DHC role, producing a consistent report for operators and future automation.

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

Milestone scope may be refined as earlier utilities are deployed and reviewed.
