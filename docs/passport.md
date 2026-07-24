# System Passport

`scripts/dhc-system-passport` is the completed v0.3.0 read-only host inventory
utility. It runs without `sudo` and writes one JSON document to stdout. Warnings
about unavailable optional data go to stderr.

## Usage

```bash
scripts/dhc-system-passport > passport.json
```

A successful run exits zero. Missing commands, inaccessible hardware details,
an unavailable Docker daemon, or a host without NVIDIA hardware do not prevent
a passport from being produced. The utility exits nonzero only if execution
fails before it can emit valid JSON.

The utility does not install packages, change services, mount filesystems, or
write host configuration. Redirecting stdout to a file is an action performed
by the calling shell, not by the utility.

## Configuration

When `/etc/dhc-infra.conf` exists, the utility sources it and uses
`DHC_NAS_MOUNT` to inspect the configured NAS location. If that setting or the
configuration file is absent, the mountpoint defaults to `/mnt/dhc-nas-01`.

Set the optional `DHC_INFRA_REPO` value to the path of the `dhc-infra` Git
working tree whose metadata should be reported. Repository discovery uses this
order:

1. a valid Git working tree configured by `DHC_INFRA_REPO`;
2. the Git repository surrounding the running script;
3. the Git repository containing the current working directory; or
4. unavailable (`null`) when no valid working tree can be discovered.

Configuration is sourced as Bash and therefore must be trusted and maintained
by an administrator.

## JSON sections

The top-level JSON object always contains:

- `identity` — UTC timestamp, hostname, operating system, kernel, architecture,
  and uptime;
- `hardware` — system vendor and model, BIOS version, CPU model and logical CPU
  count, and total memory;
- `gpu` — NVIDIA models, driver and CUDA versions reported by `nvidia-smi`, and
  per-GPU memory;
- `storage` — filesystem details for `/`, `/srv` when that directory is present,
  and configured NAS mount state;
- `network` — default interface, primary IPv4 address, and default gateway;
- `docker` — installation and version details, Docker root and runtimes, Docker
  service state, and containerd root and service state;
- `dhc_infra` — discoverable repository path, commit, Git description, and
  clean or dirty working-tree state.

Unavailable scalar values are `null`; unavailable lists are empty arrays. The
`storage.srv` value is `null` when `/srv` is not present. Storage sizes from
`df` use 1 KiB blocks, while NVIDIA GPU memory is reported in MiB.

## Collection behavior

The utility prefers standard Linux interfaces such as `/proc`, `/sys`, and
`/etc/os-release`, then uses available host commands for richer information.
Optional collectors include `lscpu`, `nvidia-smi`, `df`, `findmnt`, `ip`,
`docker`, `systemctl`, `containerd`, and `git`.

No optional command is a runtime dependency. Git commands run with optional
locking disabled so repository inspection does not refresh or modify the Git
index. Docker and systemd queries inspect state but do not start, stop, enable,
or alter services.

## Argus production validation

The utility is installed on Argus at `/usr/local/bin/dhc-system-passport` with
`DHC_INFRA_REPO=/home/dhc/dev/dhc-infra`. Its JSON output was validated before
and after reboot.

The official passport is archived at
`/mnt/dhc-nas-01/infrastructure/passports/argus/argus-2026-07-24-113142.json`.
Its SHA-256 is
`024ef1861797f37b6d6db3d038bafdc50d331323a974cebc426255155d4ea82c`, and the
pre- and post-reboot hashes matched.

See the [Argus R-001 closeout](argus-r001.md) for the full verified host record.
