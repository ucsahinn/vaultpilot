# Server System Settings

Use Server System when an Owner needs to review the server-facing settings that affect browser access, HTTPS trust, notifications, logs and maintenance. Treat this page as the operational companion to [Public host and HTTPS](public-host-https-certificate.md).

![VaultPilot Server System settings](../../assets/screenshots/server-settings.png)

The screenshot above is a sanitized UI capture from an isolated runtime with synthetic configuration only. The visible host, port, trial state, 2FA state and extension counts are documentation fixtures. Do not treat the screenshot as release asset evidence or production guidance.

## What This Surface Controls

| Area | Operator action | Public-safe evidence |
| --- | --- | --- |
| Access and HTTPS | Review public host, public port, managed HTTPS state and certificate package state. | Host shape with the real value replaced by `<SERVER_HOST>`, port and certificate subject/SAN summary. |
| Notifications | Confirm SMTP host, port, sender and test result when email notifications are enabled. | SMTP provider family, redacted sender domain and timestamp of the last test. |
| Logs and maintenance | Review log retention, audit retention, safe diagnostics and restart guidance. | Retention values, service state, redacted timestamps and non-secret error names. |

Server System is an administrative surface. Only Owners or approved server administrators should change these settings.

## Access And HTTPS Checklist

1. Confirm the canonical browser URL before changing host or port.
2. Confirm firewall and DNS routing for the target host and port.
3. Use a trusted PFX/P12 certificate package for broad production access.
4. Keep the package password out of screenshots, logs, tickets and docs.
5. Save the configuration.
6. Restart or reload only when VaultPilot asks for it.
7. Open `https://<HOST>:<PORT>` from a client machine and confirm the browser certificate state.

If the browser warns after HTTPS is enabled, use [HTTPS certificate warning](../../kb/en/certificate-warning.md).

## Notifications Checklist

Use notification settings only for operational mail such as security, update or administrative alerts.

| Check | Healthy result |
| --- | --- |
| SMTP host and port | Match the approved mail relay. |
| Sender address | Uses an approved operational mailbox. |
| Credential handling | Passwords or app secrets are entered only in the UI and never shared publicly. |
| Test result | Sends to an approved recipient without exposing vault data. |

Do not paste SMTP passwords, app passwords or message bodies containing customer data into public issues.

## Logs And Maintenance Checklist

| Setting | Operator expectation |
| --- | --- |
| Log retention | Long enough for support and audit review, short enough to limit stored operational noise. |
| Audit retention | Aligned with the organization's compliance and incident-review needs. |
| Diagnostics | Redacted before leaving the environment. |
| Restart guidance | Used only after configuration changes, updates or support guidance that explicitly require a restart. |

Owner maintenance cleanup is a backup-first maintenance action, not routine troubleshooting. It can target only `AUDIT`, `DISCOVERY` or `EXECUTIONS` records. VaultPilot rejects cleanup unless the request uses backup-clear mode; otherwise it returns `MAINTENANCE_BACKUP_REQUIRED`.

When cleanup runs, VaultPilot writes a maintenance backup named `vaultpilot-maintenance-<scope>-<timestamp>-<id>.json` before clearing the selected category. Restore affects only that category, and records created after the backup may change or be lost; the restore warning is `RESTORE_REPLACES_NEWER_CATEGORY_RECORDS`.

Maintenance cleanup does not target vault secrets, source files, service logs, databases, backups, certificates or customer data. Do not attach maintenance backup JSON publicly; keep it in the approved private support channel only.

## Safe Support Evidence

Collect:

- VaultPilot version and installed service name.
- Public host shape, with the real host replaced by `<SERVER_HOST>`.
- Configured port.
- HTTPS state and certificate subject/SAN summary.
- Notification test timestamp and non-secret error name.
- Log and audit retention values.
- Whether a restart was requested by the UI.

Do not collect:

- Certificate packages, private keys or certificate passwords.
- SMTP passwords, app passwords, cookies or API tokens.
- Raw logs that may contain secrets.
- Screenshots showing real users, internal URLs or secret records.

Related:

- [Public host and HTTPS](public-host-https-certificate.md)
- [Operator runbook](operator-runbook.md)
- [Troubleshooting](troubleshooting.md)
- [Knowledge base: Server settings restart and maintenance](../../kb/en/server-settings-restart-maintenance.md)
