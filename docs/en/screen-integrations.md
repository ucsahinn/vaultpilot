# Integrations Screen

The topbar `?` opens this page from the Integrations screen. Use it for read-only API clients, browser extension state and directory integration health.

## Work Here

- Create API clients with only the needed scopes and vault assignments.
- Copy generated secrets once into the consuming system's approved secret store.
- Revoke unused clients and browser devices instead of leaving dormant access.

## Screen States

| State | Operator response |
| --- | --- |
| Healthy | Confirm scopes, owner and last-used state remain justified. |
| Unauthorized | Rotate credentials or tokens through the owning integration path. |
| Over-scoped | Reduce permissions before issuing new client material. |

## Before You Act

- Identify whether the change affects API clients, browser extension devices or directory connectors.
- Check owner, scope, last use and downstream system before revocation or rotation.
- Prefer creating a narrow replacement before removing a credential used by automation.

## Safe Evidence

- Safe to share: integration type, required scope, endpoint path, status code and redacted client identifier.
- Keep private: client secrets, agent tokens, pairing codes, callback URLs with tenant data and request headers.
- Rotate or revoke private credentials before public discussion if any value may have been exposed.

## Operator Notes

Never publish `pmc_` client IDs with real context, `pms_` client secrets, extension pairing codes, agent tokens or connector screenshots containing internal host data.

## Related

- [Integration API clients](api-clients.md)
- [Public API reference](public-api-reference.md)
- [Browser extension screen](screen-browser-extension.md)
