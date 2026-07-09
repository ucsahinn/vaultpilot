# Server Settings Need Restart Or Maintenance Review

Use this article when Server System settings were saved but browser access, HTTPS, notifications, logs or service restart state still need review.

## First Checks

| Check | Healthy result |
| --- | --- |
| Access URL | Operators use one canonical `https://<SERVER_HOST>:<PORT>` URL. |
| Service state | `VaultPilotServer` is running; upgraded hosts may also expose legacy `PassManServer` compatibility evidence. |
| HTTPS state | Certificate subject/SAN matches the host users open in the browser. |
| Notification test | Test mail returns success or a non-secret provider error. |
| Maintenance state | Retention values are visible; cleanup is Owner-only, backup-first, and not required for normal operation. |

## Common Causes

- Host or port changed, but DNS, firewall or client bookmarks still point to the old route.
- Certificate package was saved, but the browser opens a hostname that is not in the SAN.
- SMTP credentials or relay policy changed outside VaultPilot.
- A configuration change needs the service restart that the UI requested.
- An operator expects maintenance to purge broad data, but VaultPilot cleanup is limited to `AUDIT`, `DISCOVERY` or `EXECUTIONS` records and requires backup-clear mode.

## Maintenance Cleanup Boundary

Maintenance cleanup is Owner-only. It is not routine troubleshooting and should be used only when a private support or retention decision explicitly calls for it.

VaultPilot accepts cleanup only in backup-clear mode. A plain clear request is rejected with `MAINTENANCE_BACKUP_REQUIRED`. Before clearing the selected category, VaultPilot writes a maintenance backup named `vaultpilot-maintenance-<scope>-<timestamp>-<id>.json`.

Restore affects only the category in that backup. Records created after the backup may change or be lost during restore; the restore warning is `RESTORE_REPLACES_NEWER_CATEGORY_RECORDS`. Cleanup and restore do not target vault secrets, source files, service logs, databases, backup files, certificates or customer data.

## Safe Evidence To Collect

- VaultPilot version and installed service name.
- Host shape with the real host replaced by `<SERVER_HOST>`.
- Configured port and whether the service was restarted after saving.
- Certificate subject/SAN summary and expiration date.
- Notification test timestamp and non-secret error name.
- Log retention and audit retention values.
- Maintenance cleanup scope, backup file name and redacted digest if cleanup was explicitly approved.

Do not send certificate files, private keys, certificate passwords, SMTP secrets, cookies, API tokens, raw logs that may contain secrets, databases, backups or maintenance backup JSON files through public channels.

## Resolution Path

1. Reopen VaultPilot from one canonical URL.
2. Confirm the Windows service is running.
3. Confirm DNS and firewall route to the configured host and port.
4. If HTTPS was changed, restart only when the UI asks for it, then test from a client browser.
5. If notification testing fails, confirm relay host, port, TLS mode and sender policy with the mail administrator.
6. If maintenance cleanup was explicitly approved, confirm the scope is `AUDIT`, `DISCOVERY` or `EXECUTIONS`, confirm backup-clear mode, and store the maintenance backup JSON privately.
7. If the issue continues, send the safe evidence pack through a private support channel.

Related:

- [Server System settings](../../docs/en/server-system.md)
- [Public host and HTTPS](../../docs/en/public-host-https-certificate.md)
- [HTTPS certificate warning](certificate-warning.md)
- [Support evidence pack](../../docs/en/support-evidence-pack.md)
