# Homelab Samba File Server

## Overview
- **OS**: Ubuntu Server LTS
- **Service**: Samba SMB share at `/srv/samba/shared`
- **Tested with**: `smbclient` & CIFS mount

## Files
- `smb.conf` - Samba share definition
- *(Optional)* `mount.sh` -helper script for CIFS mounting

## Quickstart
```bash
# Copy smb.conf into /etc/samba/, then:
sudo systemctl restart smbd nmbd
smbclient //localhost/Shared -N
