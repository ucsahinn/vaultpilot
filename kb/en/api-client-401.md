# Integration API client gets 401, scope denied, or no data

Use this when an integration API client cannot read `/api/public/v1/secrets`, `/api/public/v1/server/status`, `/api/public/v1/directory/status` or `/api/public/v1/updates/status`; receives 401; receives scope denied; or gets an empty encrypted snapshot.

## First Checks

1. Confirm the request goes to the intended endpoint under `https://<SERVER_HOST>:1903/api/public/v1/...`.
2. Confirm the client is active, not revoked.
3. Confirm the client has the scope required by that endpoint: `SECRETS_READ`, `SERVER_STATUS_READ`, `DIRECTORY_STATUS_READ` or `UPDATE_STATUS_READ`.
4. If the endpoint is a secret snapshot endpoint, confirm at least one vault is assigned to the client.
5. Confirm the consuming system sends either Basic auth or both compatibility headers.
6. Confirm the consuming system is not logging the authorization header.

## What The Errors Usually Mean

| Symptom | Most likely cause |
| --- | --- |
| 401 or auth failure | Missing, malformed, wrong or revoked client credentials. |
| Scope denied | The client exists but does not have the scope required by the endpoint. |
| Empty `vaults` array | No allowed vault has been assigned, or the assigned vault has no records. |
| Secret endpoint says not found | The ID is malformed, deleted or outside the client's allowed vaults. |

## Safe Evidence

Safe to share privately after redaction:

- Endpoint path and timestamp.
- Client display name, not the secret.
- Scope list and vault count.
- Endpoint path, such as `/api/public/v1/server/status`, without credentials.
- Redacted status code and error name.

Never send real client secrets, authorization headers, vault payloads, databases, logs with credentials or screenshots showing secret values.

Related:

- [Integration API clients](../../docs/en/api-clients.md)
- [Support evidence pack](../../docs/en/support-evidence-pack.md)
