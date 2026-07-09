# Sign-In Security Screen

The topbar `?` opens this page from the Sign-in security screen. Use it when reviewing lock behavior, 2FA posture and session safety.

## Work Here

- Enable 2FA for privileged users before broad rollout.
- Confirm lock and timeout settings match the operator environment.
- Treat repeated login errors or unexpected session noise as support evidence, not as a reason to weaken authentication.

## Screen States

| State | Operator response |
| --- | --- |
| Strong | Confirm recovery and owner access still work. |
| Weak | Tighten one control at a time and verify sign-in afterward. |
| Locked out | Use owner recovery procedures; do not ask for master passwords. |

## Before You Act

- Confirm at least one owner has a working recovery path before tightening policy.
- Review lockout, 2FA and session controls together so a change does not strand operators.
- Keep identity evidence redacted when escalating authentication problems.

## Safe Evidence

- Safe to share: policy summary, lockout state, 2FA enrollment category and approximate timestamp.
- Keep private: usernames, recovery codes, TOTP seeds, master passwords, session tokens and device fingerprints.
- Use private support if identity proof or owner recovery evidence is needed.

## Operator Notes

Never publish master passwords, recovery codes, TOTP seeds, auth hashes, cookies or screenshots showing one-time codes.

## Related

- [First run, owner and license](first-run-owner-license.md)
- [Session 401 after login KB](../../kb/en/session-401-after-login.md)
- [Security and trust model](security-and-trust-model.md)
