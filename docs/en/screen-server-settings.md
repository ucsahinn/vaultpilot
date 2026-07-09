# Server Settings Screen

The topbar `?` opens this page from the Server settings screen. Use it for public host, HTTPS, SMTP, maintenance, retention and local server configuration.

## Work Here

- Change host and HTTPS settings deliberately; remote browser access depends on them.
- Upload only approved `.pfx` or `.p12` certificate packages through the UI.
- Export required maintenance backups before restore or cleanup workflows.

## Screen States

| State | Operator response |
| --- | --- |
| Pending restart | Plan the restart window and confirm maintenance evidence. |
| Validation error | Fix host, certificate, SMTP or retention input before saving. |
| Maintenance required | Export the required backup before running destructive maintenance. |

## Before You Act

- Confirm whether the change affects browser access, notifications, retention, backup or service restart.
- Record current host, port, HTTPS and SMTP state before changing settings.
- Schedule restart-impacting changes with backup evidence and a rollback path.

## Safe Evidence

- Safe to share: affected setting area, timestamp, redacted host shape such as `<SERVER_HOST>` and the visible validation error.
- Keep private: PFX/P12 files, certificate passwords, SMTP credentials, local paths, database files and raw logs.
- Use private support when restart logs or maintenance evidence includes customer paths, hostnames or account context.

## Operator Notes

Do not publish local paths, PFX/P12 packages, certificate passwords, SMTP credentials, database files or raw logs.

## Related

- [Server System](server-system.md)
- [Public host and HTTPS](public-host-https-certificate.md)
- [Server settings restart and maintenance KB](../../kb/en/server-settings-restart-maintenance.md)
