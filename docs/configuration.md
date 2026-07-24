# Configuration

The NAS utility reads `/etc/dhc-infra.conf` by default. Set `DHC_INFRA_CONFIG`
when invoking that utility to use another trusted configuration file. System
Passport sources `/etc/dhc-infra.conf` when it exists.

| Setting | Purpose |
| --- | --- |
| `DHC_NAS_HOST` | NAS hostname or IP address |
| `DHC_NAS_SHARE` | CIFS share name |
| `DHC_NAS_MOUNT` | Local mount point |
| `DHC_NAS_CREDENTIALS` | Path to the CIFS credentials file |
| `DHC_NAS_VERSION` | SMB protocol version; defaults to `3.1.1` |
| `DHC_NAS_UID` | Optional CIFS file owner UID |
| `DHC_NAS_GID` | Optional CIFS file owner GID |
| `DHC_INFRA_REPO` | Optional Git working tree reported by System Passport |

Use `config/dhc-infra.conf.example` as a starting point. Keep credentials out
of both the repository and the main configuration file. The separate
credentials file must have permissions `0600`.

## Verified Argus values

Argus R-001 uses:

```bash
DHC_NAS_HOST=192.168.12.128
DHC_NAS_SHARE=DHC
DHC_NAS_MOUNT=/mnt/dhc-nas-01
DHC_NAS_VERSION=3.1.1
DHC_NAS_UID=1000
DHC_NAS_GID=1000
DHC_INFRA_REPO=/home/dhc/dev/dhc-infra
```

The credentials path and credentials remain host-managed and are deliberately
not recorded here. See [NAS mounting](nas.md), [System Passport](passport.md),
and the [Argus R-001 closeout](argus-r001.md).
