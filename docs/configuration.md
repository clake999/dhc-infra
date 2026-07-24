# Configuration

The current NAS utility reads `/etc/dhc-infra.conf` by default. Set
`DHC_INFRA_CONFIG` when invoking it to use another trusted configuration file.

| Setting | Purpose |
| --- | --- |
| `DHC_NAS_HOST` | NAS hostname or IP address |
| `DHC_NAS_SHARE` | CIFS share name |
| `DHC_NAS_MOUNT` | Local mount point |
| `DHC_NAS_CREDENTIALS` | Path to the CIFS credentials file |
| `DHC_NAS_VERSION` | SMB protocol version; defaults to `3.1.1` |
| `DHC_INFRA_REPO` | Optional path to the `dhc-infra` Git working tree used by System Passport |

Use `config/dhc-infra.conf.example` as a starting point. Keep credentials out
of both the repository and the main configuration file. The separate
credentials file must have permissions `0600`.

See [NAS mounting](nas.md) for runtime behavior.
