# Users Screen

The topbar `?` opens this page from the Users screen. Use it for account state, roles, 2FA status and vault access review.

## Work Here

- Keep at least one protected Owner account.
- Grant the minimum role and vault access needed.
- Record why privileged role changes were made.

## Screen States

| State | Operator response |
| --- | --- |
| Normal | Review owner coverage, inactive accounts and 2FA state. |
| Privileged change | Confirm business reason and preserve audit context before saving. |
| Last owner risk | Stop and create a recovery-safe owner plan before disabling access. |

## Before You Act

- Check role, vault access, 2FA state and last activity before changing a user.
- Maintain at least two accountable owner paths before disabling or deleting privileged access.
- Record the reason for access changes without exposing identity documents or personal data publicly.

## Safe Evidence

- Safe to share: role category, account state, 2FA coverage summary and redacted change reason.
- Keep private: names, email addresses, recovery status, identity documents and screenshots of real user lists.
- Use private support for owner recovery, disputed access removal or suspected account takeover.

## Operator Notes

Do not publish usernames, public keys, role-change screenshots or user lists from a real tenant. Use redacted support evidence instead.

## Related

- [First run, owner and license](first-run-owner-license.md)
- [Security and trust model](security-and-trust-model.md)
- [Audit log screen](screen-audit-log.md)
