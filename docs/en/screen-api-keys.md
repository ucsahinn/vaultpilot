# API Keys Screen

The topbar `?` opens this page from the API keys screen. Use it for service tokens, integration secrets and machine-to-machine credentials that must stay encrypted at rest.

## Work Here

- Store the token value only in the encrypted secret field.
- Capture owner, system, scope, expiry and rotation date in metadata.
- Revoke and recreate keys in the source system when exposure is suspected; do not rely on editing the vault record alone.

## Screen States

| State | Operator response |
| --- | --- |
| Missing owner | Assign ownership before relying on the key. |
| Expiring | Plan rotation and consumer update order before changing the value. |
| Exposed | Rotate privately and treat any public appearance as compromised. |

## Before You Act

- Identify the consuming system, owner and permitted scope before copying or rotating.
- Check whether the key is used by automation so downstream changes can be scheduled.
- Treat partial key names, prefixes and integration URLs as sensitive context in public channels.

## Safe Evidence

- Safe to share: endpoint name, required scope, error code, rotation status and redacted client identifier prefix.
- Keep private: API key values, bearer tokens, OAuth client secrets, full client IDs and request headers.
- If exposure is possible, rotate or revoke in the source system before discussing the incident publicly.

## Operator Notes

Public examples must never include real-looking API keys, bearer tokens, OAuth client secrets or integration credentials.

## Related

- [Public API reference](public-api-reference.md)
- [Integration API clients](api-clients.md)
- [API client access KB](../../kb/en/api-client-401.md)
