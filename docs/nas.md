# NAS mounting

`scripts/dhc-mount-nas` is the utility released in v0.2.0. It requires Linux
with Bash, root privileges, CIFS support, `mount`, `mountpoint`, `findmnt`, and
`stat`.

Prepare `/etc/dhc-infra.conf` from `config/dhc-infra.conf.example` and create a
separate CIFS credentials file with permissions `0600`. The default
configuration path can be overridden with `DHC_INFRA_CONFIG`.

The utility validates its prerequisites, creates the mount point when needed,
and accepts an existing mount only when it is the configured share. It then
mounts with CIFS, verifies the filesystem type, and creates and removes a
temporary file to confirm read/write access. It stops if another source already
occupies the mount point.

The optional `DHC_NAS_UID` and `DHC_NAS_GID` values control CIFS ownership. When
they are omitted, the utility uses `SUDO_UID` and `SUDO_GID` when available and
otherwise defaults both values to `1000`.

## Argus R-001 deployment

Argus mounts `//192.168.12.128/DHC` at `/mnt/dhc-nas-01` using CIFS SMB 3.1.1
with `uid=1000,gid=1000`. The host-managed `dhc-nas-mount.service` is enabled
and active.

Read/write access and reboot persistence were verified. After reboot, the mount
was present, NAS writes succeeded, and the archived System Passport retained
its expected SHA-256. The utility remains an on-demand mount command; boot-time
persistence on Argus is provided by the host-managed systemd service.

See the [Argus R-001 closeout](argus-r001.md) for the validation record.
