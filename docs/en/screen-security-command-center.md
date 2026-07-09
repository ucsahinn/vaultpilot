# Security Command Center Screen

The topbar `?` opens this page from the Security Command Center. Use it when an operator needs the fastest overview of vault health, security posture, directory state, certificate risk, rotation activity and update readiness.

## Work Here

- Start with the highest-risk card, not the newest event.
- Treat score drops as triage prompts; confirm the underlying audit, license, 2FA, certificate or directory signal before acting.
- Use dashboard drill-through actions to move into the exact workspace that owns the remediation.

## Screen States

| State | Operator response |
| --- | --- |
| Quiet | Confirm the last refresh time, then continue with scheduled review. |
| Warning | Open the linked screen before changing records so the root signal stays visible. |
| Blocked | Collect redacted status, affected component and timestamp for private support. |

## Before You Act

- Check whether the signal is global, vault-specific or tied to one integration.
- Prefer drill-through links over manual navigation so the same filter context is preserved.
- If more than one card is red, work from authentication, license and update blockers before cosmetic findings.

## Safe Evidence

- Safe to share: posture category, affected component, redacted status, refresh window and next-screen route.
- Keep private: raw dashboard counts, hostnames, usernames, vault names, tenant timing and screenshots that reveal internal context.
- Use private support when multiple red cards indicate auth, license or update blockers that require real environment evidence.

## Operator Notes

The screen is a command surface, not a final report. Do not copy raw dashboard values into public issues if they reveal host names, users, vault names, private counts or internal timing.

## Related

- [Audit and security posture](audit-and-security-posture.md)
- [Security and trust model](security-and-trust-model.md)
- [Operator runbook](operator-runbook.md)
