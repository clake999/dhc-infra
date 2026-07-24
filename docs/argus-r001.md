# Argus R-001 Infrastructure Closeout

**Status: COMPLETE**

Argus R-001 established and validated the production infrastructure baseline
for the Argus GPU host. The facts below were verified on 2026-07-24.

## Host baseline

| Item | Verified value |
| --- | --- |
| Hostname | `argus` |
| Operating system | Ubuntu 26.04 LTS |
| Kernel | `7.0.0-28-generic` |
| Architecture | `x86_64` |
| CPU | Intel Core i9-14900KF |
| Logical CPUs | 32 |
| Memory | Approximately 64 GB |
| GPU | NVIDIA GeForce RTX 5080 |
| NVIDIA driver | `595.84` |
| CUDA reported by `nvidia-smi` | `13.2` |

## Docker, containerd, and GPU runtime

| Item | Verified value |
| --- | --- |
| Docker version | `29.6.2` |
| Docker data root | `/srv/docker/docker` |
| containerd root | `/srv/docker/containerd` |
| Docker service | Enabled and active |
| containerd service | Enabled and active |
| NVIDIA Docker runtime | Installed and verified |

GPU access from a container was proved with:

```bash
docker run --rm --gpus all nvidia/cuda:13.0.1-base-ubuntu24.04 nvidia-smi
```

The same GPU-container validation passed after reboot. `/var/lib/docker` and
`/var/lib/containerd` were inspected and contain only expected small runtime
metadata, not legacy payload storage. Both directories are intentionally
retained.

## NAS

| Item | Verified value |
| --- | --- |
| Share | `//192.168.12.128/DHC` |
| Mountpoint | `/mnt/dhc-nas-01` |
| Protocol | CIFS SMB 3.1.1 |
| Ownership | `uid=1000,gid=1000` |
| systemd service | `dhc-nas-mount.service` |
| Service state | Enabled and active |

NAS read/write access and reboot persistence were verified. After reboot, the
share was mounted and remained writable.

## System Passport and archive

The System Passport is installed at `/usr/local/bin/dhc-system-passport` and
uses:

```bash
DHC_INFRA_REPO=/home/dhc/dev/dhc-infra
```

Its output was validated as JSON. The official archived passport is:

```text
/mnt/dhc-nas-01/infrastructure/passports/argus/argus-2026-07-24-113142.json
```

The archived file's SHA-256 is:

```text
024ef1861797f37b6d6db3d038bafdc50d331323a974cebc426255155d4ea82c
```

The hash matched before and after reboot.

## Repository state at closeout

| Item | Verified value |
| --- | --- |
| Repository | `/home/dhc/dev/dhc-infra` |
| Commit | `e114229a4e02ec518ae2dde3e736832552bc923e` |
| Git describe | `v0.2.0-3-ge114229` |
| Working tree | Clean after the prior push |

## Reboot validation

The closeout reboot validation passed for:

- NAS mount presence;
- NAS write access;
- Docker service;
- containerd service;
- Docker data root;
- NVIDIA GPU container access;
- System Passport JSON output; and
- archived-passport integrity.

No legacy payload migration or directory removal is required for
`/var/lib/docker` or `/var/lib/containerd`. Argus R-001 is complete.
