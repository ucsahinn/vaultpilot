# Notifications Screen

The topbar `?` opens this page from the Notifications screen. Use it to decide which events should notify operators and which recipients should receive them.

## Work Here

- Route only actionable events.
- Keep recipient lists current and role-appropriate.
- Test SMTP delivery without exposing passwords or message bodies in public evidence.

## Screen States

| State | Operator response |
| --- | --- |
| Configured | Send a controlled test and confirm the right role receives it. |
| Delivery failed | Check SMTP settings privately without exposing passwords. |
| Too noisy | Disable non-actionable events or narrow recipients. |

## Before You Act

- Confirm which event classes must reach humans and which should stay in audit only.
- Check recipient groups, SMTP health and alert frequency before changing templates.
- Keep sample alerts redacted; messages can reveal hosts, users, vault names or incident timing.

## Safe Evidence

- Safe to share: event class, delivery status, recipient role category, timestamp window and redacted SMTP error code.
- Keep private: SMTP credentials, real email addresses, customer hostnames, message bodies and incident-specific alert payloads.
- Keep failed-delivery logs private if they include transport headers or internal routing details.

## Operator Notes

Notification examples must not include SMTP passwords, real addresses, customer hostnames or incident-specific secret values.

## Related

- [Server settings screen](screen-server-settings.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Server settings restart and maintenance KB](../../kb/en/server-settings-restart-maintenance.md)
