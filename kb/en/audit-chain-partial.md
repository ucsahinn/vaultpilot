# Audit chain is partial or inconsistent

Use this when the Audit Log screen reports a partial chain, an inconsistent hash sequence, missing rows after restore, or a chain warning that cannot be explained by the visible filters. Treat the case as security-relevant until the operator can connect it to an approved restore, backup import, update, retention policy or maintenance action.

## Triage

1. Open [Audit Log](../../docs/en/screen-audit-log.md) from the workspace, then use the topbar `?` to confirm the current operator procedure.
2. Capture the active filters, date range and visible chain state before changing anything.
3. Identify the first inconsistent event and the closest known-good event before it.
4. Check whether a restore, backup import, update, retention cleanup or maintenance job ran in the same window.
5. Stop non-essential write operations if the chain appears broken and no approved maintenance event explains it.

## What To Check

| Area | Check | Expected result |
| --- | --- | --- |
| Filters | User, category, date and severity filters | A partial view caused by filters is clearly distinguishable from a broken chain. |
| Maintenance | Backup import, restore, update and retention events | The chain transition has a matching administrative event. |
| Storage | Server restart, disk full, database replacement or manual copy | No unsupported database movement occurred outside VaultPilot procedures. |
| Evidence | Last known-good export or backup metadata | The operator can explain what changed without exposing secret payloads. |

## Safe Evidence

- VaultPilot server version and approximate incident time.
- Redacted filter set, event ids and event categories around the first warning.
- Whether restore, import, update, retention cleanup or maintenance ran.
- Chain status text and count summary, not raw database rows.
- Windows service restart timestamps when relevant.

## Escalate Privately

Open a private support channel when the warning remains after filter review, when the first inconsistent row cannot be tied to approved maintenance, or when multiple admins were active during the same window. Do not continue normal rotation, sharing or user-administration work until the chain status is understood.

## Do Not Send

Do not send database files, backups, secret payloads, master passwords, raw logs containing credentials, screenshots showing vault records, or customer/user identities to public support channels.

Related: [Audit Log screen](../../docs/en/screen-audit-log.md), [Operator runbook](../../docs/en/operator-runbook.md), [Support evidence pack](../../docs/en/support-evidence-pack.md), [Public issue redaction](public-issue-redaction.md).
