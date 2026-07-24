# Architecture

`dhc-infra` is the host-infrastructure layer shared by the DieHardCards
ecosystem. Product repositories retain application code and product-specific
workflows; this repository contains portable Linux operations useful across
multiple DHC host types.

It covers reusable host tasks such as storage mounts, system inventory,
bootstrap checks, diagnostics, and recovery support. Host configuration and
credentials live outside the repository, normally under `/etc`.

Only utilities identified as current in the [README](../README.md) and
[changelog](../CHANGELOG.md) should be treated as released. See the
[roadmap](../ROADMAP.md) for planned capabilities.
