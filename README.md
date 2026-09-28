# Homelab Samba File Server

## Overview
- **OS**: Ubuntu Server LTS
- **Service**: Samba SMB share at `/srv/samba/shared`
- **Tested with**: `smbclient` & CIFS mount

## Files
- `smb.conf` - Samba share definition
- *(Optional)* `mount.sh` - helper script for CIFS mounting

## Quickstart
```bash
# Copy smb.conf into /etc/samba/, then:
sudo systemctl restart smbd nmbd
smbclient //localhost/Shared -N
```

## Security Review

**Review status:** Audited  
**Last reviewed:** September 2026

The current `[Shared]` configuration permits anonymous guest access and write access:

```ini
[Shared]
path = /srv/samba/shared
browsable = yes
read only = no
guest ok = yes
```

This was identified during the September 2026 homelab security audit as a security hardening item. The configuration may be appropriate for an isolated lab, but anonymous writable SMB access creates a broader trust boundary than authenticated access.

### Planned remediation

The intended remediation is to:
- disable guest access to the writable share;
- use authenticated Samba access;
- preserve the existing file-sharing/backup workflow;
- validate access from the systems that legitimately use the share before considering the remediation complete.

**Remediation is intentionally pending until the Samba host can be accessed and the existing clients/workflows can be verified.**

### Validation plan

After the configuration is changed:

1. Run `testparm` to validate Samba configuration syntax.
2. Restart Samba only after the configuration passes validation.
3. Verify authenticated access from an authorized client.
4. Verify that unauthorized/guest access is rejected.
5. Verify any existing backup or file-transfer workflows.
6. Document the final access boundary.

No infrastructure configuration has been changed as part of this documentation update.
