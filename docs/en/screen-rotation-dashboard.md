# Rotation Dashboard Screen

The topbar `?` opens this page from the Rotation dashboard. Use it to plan password, credential and API-key rotation without losing ownership or audit evidence.

## Work Here

- Sort by risk and age before choosing rotation work.
- Confirm the owner, system, vault and dependent integration before changing a credential.
- Record why emergency rotation was needed when the change is incident-driven.

## Screen States

| State | Operator response |
| --- | --- |
| On schedule | Keep the owner and next rotation date current. |
| Overdue | Contact the record owner and plan a controlled change window. |
| Blocked | Do not rotate blindly; collect owner, dependency and audit context first. |

## Before You Act

- Confirm the rotation target still has an owner and a rollback path.
- Review last-used signals before rotating a credential that may affect an active integration.
- Record the planned maintenance window and affected vaults before triggering work.

## Safe Evidence

- Safe to share: rotation state, age band, affected system category, owner role and redacted control outcome.
- Keep private: old values, new values, recovery codes, shared passphrases, target usernames and dependency details that identify a customer system.
- Use private support when emergency rotation evidence includes incident context or secret-bearing screenshots.

## Operator Notes

Rotation evidence should describe the business system and control outcome. Do not expose old or new values, recovery codes, shared passphrases or unredacted screenshots.

## Related

- [Operator runbook](operator-runbook.md)
- [Passwords screen](screen-passwords.md)
- [API keys screen](screen-api-keys.md)
