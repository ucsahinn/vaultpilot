# License Lifecycle

VaultPilot uses offline license verification. The server verifies a license code with public verification material; issuer-side private signing material is never installed on customer servers.

## Normal Lifecycle

| Stage | Operator view | Action |
| --- | --- | --- |
| Trial | VaultPilot runs with trial limits and an expiry date. | Validate the deployment, backup flow, HTTPS and owner access before production use. |
| Active license | License page shows plan, capacity, expiry, signature status and enabled modules. | Review capacity and expiry during monthly operations. |
| Renewal window | Expiry is close enough to plan replacement. | Request the next offline license code through the approved support channel. |
| Replacement | A new code is pasted into the License screen. | Confirm signature verification, capacity, expiry and module availability. |
| Expired or over capacity | VaultPilot can restrict writes while keeping safe read and backup-export paths available. | Reduce usage, apply a valid license, or work with support before adding users or enabling new workflows. |

## Read-only Behavior

When trial or license time expires, VaultPilot can keep login, secret viewing, audit review and backup export available while blocking writes, user creation, sharing, extension pairing and update install actions. This keeps operators from losing access to encrypted data while preventing unlicensed expansion.

## What To Record

- License state, plan and expiry date.
- Active user count and capacity.
- Signature verification status.
- Modules that are enabled or unavailable.
- Date and approver for replacement.

Do not put license codes, issuer private material or screenshots containing customer data into public tickets.

Related:

- [First run, owner and license](first-run-owner-license.md)
- [Operator runbook](operator-runbook.md)
- [Knowledge base: license read-only](../../kb/en/license-read-only.md)
- [Support evidence pack](support-evidence-pack.md)
