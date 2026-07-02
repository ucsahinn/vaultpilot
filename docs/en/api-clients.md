# Integration API Clients

Use integration API clients when an approved system needs read-only VaultPilot data through the public API. Keep the client narrow: grant only the scopes and vaults the system needs, record who owns it, and revoke it when the integration is retired.

## Public API Surface

`GET /api/public/v1/secrets` returns an encrypted snapshot for the vaults assigned to the API client. The response includes vault metadata, encrypted vault names, secret IDs, secret types, encrypted payloads, timestamps and the `ENCRYPTED_SNAPSHOT` mode. It does not return plaintext passwords or decrypted vault data.

`GET /api/public/v1/secrets/{secretId}` returns one encrypted secret from the same allowed snapshot. If the ID is malformed, outside the client's allowed vault list, or missing, the API answers as not found.

The same API client model also supports read-only operational status endpoints. These endpoints never decrypt vault data and do not require vault assignment unless the client also has `SECRETS_READ`.

| Scope | Endpoint | Returns |
| --- | --- | --- |
| `SECRETS_READ` | `GET /api/public/v1/secrets` and `GET /api/public/v1/secrets/{secretId}` | Encrypted vault and secret snapshots for assigned vaults. |
| `SERVER_STATUS_READ` | `GET /api/public/v1/server/status` | App version, uptime, vault count, active API client count and directory provider count. |
| `DIRECTORY_STATUS_READ` | `GET /api/public/v1/directory/status` | Directory provider health, object counts, selected login counts, selected credential counts and last-seen/sync timestamps. |
| `UPDATE_STATUS_READ` | `GET /api/public/v1/updates/status` | Update Center status in the same shape shown to the console, scoped to read-only monitoring. |

## Create A Client

1. Sign in as an Owner.
2. Open Integrations or the API client surface.
3. Pick only the endpoint scopes the consuming system needs.
4. If `SECRETS_READ` is selected, assign the minimum vault list. Status-only clients do not need vault scope.
5. Create the client with a clear name.
6. Copy the client secret once and store it in the approved secret store for the consuming system.
7. Record owner, purpose, allowed vaults, scopes and review date.

The client secret is stored hashed on the server. If it is lost, create a new client and revoke the old one.

## Authentication

VaultPilot accepts either HTTP Basic auth or the legacy compatibility headers. Prefer Basic auth for new integrations.

```http
Authorization: Basic base64(<CLIENT_ID>:<CLIENT_SECRET>)
```

Compatibility headers remain available for older clients:

```http
x-passman-client-id: <CLIENT_ID>
x-passman-client-secret: <CLIENT_SECRET>
```

Do not log either header. Do not paste real client IDs or secrets into public issues, screenshots, docs or support threads.

## Example Request

```powershell
$pair = "<CLIENT_ID>:<CLIENT_SECRET>"
$basic = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($pair))
Invoke-RestMethod -Headers @{ Authorization = "Basic $basic" } -Uri "https://<SERVER_HOST>:1903/api/public/v1/secrets"
```

Status-only example:

```powershell
$pair = "<CLIENT_ID>:<CLIENT_SECRET>"
$basic = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($pair))
Invoke-RestMethod -Headers @{ Authorization = "Basic $basic" } -Uri "https://<SERVER_HOST>:1903/api/public/v1/server/status"
```

Use placeholders in public examples. Real values belong only in the consuming system's approved secret store.

## Expected Errors

| Symptom | Meaning | Operator action |
| --- | --- | --- |
| 401 or auth failure | Client ID/secret is missing, malformed, wrong or revoked. | Rotate the client secret by creating a new client, update the consuming system, then revoke the old client. |
| Scope denied | The client does not have the scope required by the endpoint. | Add the intended scope or create a new least-privilege client. |
| Empty vault list | The client has no vaults assigned for secret snapshot access. This matters only for `SECRETS_READ`. | Assign only the vaults the integration needs, or remove `SECRETS_READ` for status-only clients. |
| Secret not found | The secret ID is malformed, deleted or outside the client's allowed vaults. | Confirm the secret ID from an allowed snapshot. |

Related:

- [Security and trust model](security-and-trust-model.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Knowledge base: API client access](../../kb/en/api-client-401.md)
- [Support evidence pack](support-evidence-pack.md)
