# Audit and Security Posture

The VaultPilot Overview screen shows system health, security score, and risks that need action.

## Score Signals

- 2FA state.
- Audit chain verification.
- License health.
- Extension pairing state.
- Update and package health.

## Audit Chain

Audit events are tracked with chained hash fields. If the chain is partial or inconsistent, inspect the relevant events with advanced filters.

## Recommended Actions

- Enable 2FA for owner and admin accounts.
- Investigate partial or broken audit chain state.
- Revoke stale extension devices.
- Check update manifest and MSI signature state.
