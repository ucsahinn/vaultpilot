# Integration API Clients

Use integration API clients when an approved system needs read-only VaultPilot data through the public API. Keep the client narrow: grant only the scopes and vaults the system needs, record who owns it, and revoke it when the integration is retired.

## What The Secrets API Returns

`GET /api/public/v1/secrets` returns an encrypted snapshot for the vaults assigned to the API client. The response includes vault metadata, encrypted vault names, secret IDs, secret types, encrypted payloads, timestamps and the `ENCRYPTED_SNAPSHOT` mode. It does not return plaintext passwords or decrypted vault data.

`GET /api/public/v1/secrets/{secretId}` returns one encrypted secret from the same allowed snapshot. If the ID is malformed, outside the client's allowed vault list, or missing, the API answers as not found.

## Create A Client

1. Sign in as an Owner.
2. Open Integrations or the API client surface.
3. Create a client with a clear name, the `SECRETS_READ` scope, and the minimum vault list.
4. Copy the client secret once and store it in the approved secret store for the consuming system.
5. Record owner, purpose, allowed vaults, scopes and review date.

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

Use placeholders in public examples. Real values belong only in the consuming system's approved secret store.

## Expected Errors

| Symptom | Meaning | Operator action |
| --- | --- | --- |
| 401 or auth failure | Client ID/secret is missing, malformed, wrong or revoked. | Rotate the client secret by creating a new client, update the consuming system, then revoke the old client. |
| Scope denied | The client does not have `SECRETS_READ`. | Add the intended scope or create a new least-privilege client. |
| Empty vault list | The client has no vaults assigned for secret snapshot access. | Assign only the vaults the integration needs. |
| Secret not found | The secret ID is malformed, deleted or outside the client's allowed vaults. | Confirm the secret ID from an allowed snapshot. |

Related:

- [Security and trust model](security-and-trust-model.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Knowledge base: API client access](../../kb/en/api-client-401.md)
- [Support evidence pack](support-evidence-pack.md)
