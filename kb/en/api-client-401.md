# Integration API client gets 401 or no secrets

Use this when an integration API client cannot read `/api/public/v1/secrets`, receives 401, receives scope denied, or gets an empty encrypted snapshot.

## First Checks

1. Confirm the request goes to `https://<SERVER_HOST>:1903/api/public/v1/secrets`.
2. Confirm the client is active, not revoked.
3. Confirm the client has the `SECRETS_READ` scope.
4. Confirm at least one vault is assigned to the client.
5. Confirm the consuming system sends either Basic auth or both compatibility headers.
6. Confirm the consuming system is not logging the authorization header.

## What The Errors Usually Mean

| Symptom | Most likely cause |
| --- | --- |
| 401 or auth failure | Missing, malformed, wrong or revoked client credentials. |
| Scope denied | The client exists but does not have `SECRETS_READ`. |
| Empty `vaults` array | No allowed vault has been assigned, or the assigned vault has no records. |
| Secret endpoint says not found | The ID is malformed, deleted or outside the client's allowed vaults. |

## Safe Evidence

Safe to share privately after redaction:

- Endpoint path and timestamp.
- Client display name, not the secret.
- Scope list and vault count.
- Redacted status code and error name.

Never send real client secrets, authorization headers, vault payloads, databases, logs with credentials or screenshots showing secret values.

Related:

- [Integration API clients](../../docs/en/api-clients.md)
- [Support evidence pack](../../docs/en/support-evidence-pack.md)
