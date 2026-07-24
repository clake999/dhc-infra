# DHC Infrastructure (dhc-infra)

Shared infrastructure utilities for the DieHardCards ecosystem.

## Purpose

This repository contains reusable Linux infrastructure tooling shared by:

- DHC Web Application
- DHC Station (Hans, Holly, Theo, ...)
- AI Servers (Argus)
- Development Workstations

## Planned Utilities

- dhc-system-passport
- dhc-mount-nas
- dhc-health
- install.sh

## Philosophy

Build Once. Manage Everywhere.

Every utility should:

- Be portable
- Fail safely
- Produce human-readable output
- Produce machine-readable output
- Be reusable across every DHC system
