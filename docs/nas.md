# NAS mounting

`scripts/dhc-mount-nas` is the current utility released in v0.2.0. It requires
Linux with Bash, root privileges, CIFS support, `mount`, `mountpoint`, `findmnt`,
and `stat`.

Prepare `/etc/dhc-infra.conf` from `config/dhc-infra.conf.example` and create a
separate CIFS credentials file with permissions `0600`. The default
configuration path can be overridden with `DHC_INFRA_CONFIG`.

The utility validates its prerequisites, creates the mount point when needed,
and accepts an existing mount only when it is the configured share. It then
mounts with CIFS, verifies the filesystem type, and creates and removes a
temporary file to confirm read/write access. It stops if another source already
occupies the mount point.

Review the utility and configuration before running them as root. Persistent
boot-time mounting is outside the v0.2.0 scope.
