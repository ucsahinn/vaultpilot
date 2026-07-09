# Audit Log Screen

The topbar `?` opens this page from the Audit log screen. Use it to review event history, actor context, target changes and integrity-chain evidence.

## Work Here

- Filter by action, actor, target and risk before exporting.
- Treat partial chain state as an investigation item.
- Preserve event hashes and timestamps when preparing private support evidence.

## Screen States

| State | Operator response |
| --- | --- |
| Complete | Keep filters and export scope narrow. |
| Partial | Use the audit-chain KB before relying on the event list. |
| Missing context | Capture filter state and adjacent timestamps for private support. |

## Before You Act

- Set actor, action, target and time filters before exporting evidence.
- Preserve event hashes and adjacent timestamps when investigating chain gaps.
- Stop non-essential changes if audit integrity is unclear and the incident is active.

## Safe Evidence

- Safe to share: event category, narrow time window, redacted actor role, event hash and filter summary.
- Keep private: usernames, object IDs, raw audit exports, internal IPs and incident material with customer context.
- If audit-chain integrity is partial, preserve the evidence and use the audit-chain KB before changing records.

## Operator Notes

Audit evidence can expose usernames, internal object IDs and operational timing. Redact public issues and use private support for real incident material.

## Related

- [Audit and security posture](audit-and-security-posture.md)
- [Audit chain partial KB](../../kb/en/audit-chain-partial.md)
- [Support evidence pack](support-evidence-pack.md)
