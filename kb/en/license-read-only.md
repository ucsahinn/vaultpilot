# License read-only state

Use this when VaultPilot allows login, vault viewing, audit review or backup export, but blocks writes, user changes, sharing, pairing, discovery import or update install actions. Read-only mode is a controlled safety state; do not bypass it with database edits or unsupported configuration changes.

## Triage

1. Open [License](../../docs/en/screen-license.md) and use the topbar `?` to confirm the expected state.
2. Record whether the status is trial, active, expired, over capacity, invalid signature or read-only.
3. Compare active users with the licensed capacity.
4. Review feature gates for sharing, browser extension, integrations, discovery and updates.
5. Paste a valid offline license code only when the owner or support has provided one through the approved channel.
6. If the signature fails, stop and escalate privately instead of retrying random license material.

## Expected Behavior

| Capability | Read-only expectation |
| --- | --- |
| Login and unlock | Available when the account is valid. |
| Secret viewing | Available for permitted records so operators can recover safely. |
| Audit review | Available so the state change can be investigated. |
| Backup export | Usually available for owner-led recovery. |
| Writes, sharing, pairing, discovery import and update install | Blocked until the license state is valid again. |

## Safe Evidence

- License state label and plan name.
- Active user count versus capacity.
- Expiry date or trial state.
- Feature gate list with enabled/disabled state.
- Signature validation state, not the license payload.

## Do Not Send

Do not send license codes, signed payloads, private license material, customer entitlement screenshots, internal billing records or raw database rows in public channels.

Related: [License screen](../../docs/en/screen-license.md), [License lifecycle](../../docs/en/license-lifecycle.md), [First run, owner and license](../../docs/en/first-run-owner-license.md), [Public issue redaction](public-issue-redaction.md).
