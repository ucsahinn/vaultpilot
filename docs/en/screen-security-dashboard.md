# Security Dashboard Screen

The topbar `?` opens this page from the Security dashboard. Use it to interpret sign-in security, audit integrity, license state, update readiness and extension posture as one operational view.

## Work Here

- Confirm whether weak posture is caused by missing 2FA, read-only license state, audit-chain issues, stale updates or missing browser approvals.
- Prefer fixing root controls over hiding warnings.
- Escalate if audit integrity is partial or a privileged account changed unexpectedly.

## Screen States

| State | Operator response |
| --- | --- |
| Healthy | Record the score window and continue routine review. |
| Degraded | Open the lowest-scoring signal and verify whether it is configuration, license or audit related. |
| Unknown | Refresh diagnostics once, then preserve the unavailable component name instead of guessing. |

## Before You Act

- Separate account-protection findings from server or update findings before assigning work.
- Confirm the observed score was refreshed after the last user, license or update change.
- Capture only redacted posture summaries for support; keep user names and internal host data out of public notes.

## Safe Evidence

- Safe to share: posture band, signal category, refresh window, redacted score change and affected control family.
- Keep private: real usernames, hostnames, vault names, tenant identifiers, internal counts and screenshots with customer context.
- Summarize security posture publicly only after removing user, host and vault identifiers.

## Operator Notes

Security dashboard data is safe to summarize, but not safe to screenshot with real usernames, host names, vault names or internal customer context.

## Related

- [Security and trust model](security-and-trust-model.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Sign-in security screen](screen-sign-in-security.md)
