# Public API Reference

VaultPilot public integration clients are read-only identities for approved systems. They expose encrypted vault snapshots and operational status metadata only. The public API never returns plaintext passwords, master passwords, decrypted vault payloads or private server material.

Create clients from the Owner-only Integrations/API client surface. Each client has a generated client ID that matches `pmc_[A-Za-z0-9_-]{24}` and a one-time client secret that matches `pms_[A-Za-z0-9_-]{43}`. The secret is stored server-side as a keyed digest; if it is lost, create a replacement client and revoke the old one.

Public v1 endpoints are GET-only read surfaces. Do not send a request body. Requests with a body are rejected before the route reads integration credentials.

## Authentication

Prefer HTTP Basic auth for new integrations:

```http
Authorization: Basic base64(<CLIENT_ID>:<CLIENT_SECRET>)
```

Legacy compatibility headers remain available for older clients:

```http
x-passman-client-id: <CLIENT_ID>
x-passman-client-secret: <CLIENT_SECRET>
```

Do not log either header. Do not paste real client IDs, client secrets, encrypted payloads, vault IDs or secret IDs into public issues, screenshots, docs or support threads.

Malformed credentials are rejected before database lookup. Basic auth headers are bounded to 512 characters; compatibility credential headers are bounded to 256 characters each.

## Scopes And Endpoints

| Scope | Endpoint | Response |
| --- | --- | --- |
| `SECRETS_READ` | `GET /api/public/v1/secrets` | Encrypted vault and secret snapshots for the vaults assigned to the API client. |
| `SECRETS_READ` | `GET /api/public/v1/secrets/{secretId}` | One encrypted secret from the assigned-vault snapshot. The route ID must be a UUID. |
| `SERVER_STATUS_READ` | `GET /api/public/v1/server/status` | App version, uptime, vault count, active API client count and directory provider count. |
| `DIRECTORY_STATUS_READ` | `GET /api/public/v1/directory/status` | Directory provider health, object counts, selected login and credential counts, last-seen timestamps and sync timestamps. |
| `UPDATE_STATUS_READ` | `GET /api/public/v1/updates/status` | Update Center status for read-only monitoring. |

`SECRETS_READ` requires at least one assigned vault. Status-only clients can be created without vault assignment.

## Request Examples

PowerShell Basic auth example:

```powershell
$pair = "<CLIENT_ID>:<CLIENT_SECRET>"
$basic = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($pair))
Invoke-RestMethod -Headers @{ Authorization = "Basic $basic" } -Uri "https://<SERVER_HOST>:1903/api/public/v1/server/status"
```

Compatibility-header example:

```powershell
Invoke-RestMethod `
  -Headers @{
    "x-passman-client-id" = "<CLIENT_ID>"
    "x-passman-client-secret" = "<CLIENT_SECRET>"
  } `
  -Uri "https://<SERVER_HOST>:1903/api/public/v1/secrets"
```

Use placeholders in public examples. Real values belong only in the consuming system's approved secret store.

Run commands containing real `$pair` or `$basic` only in a private operator shell. Never paste those values into public issues, screenshots, transcripts or docs.

## Response Shape

Secret snapshot responses are encrypted data packages, not decrypted records:

```json
{
  "mode": "ENCRYPTED_SNAPSHOT",
  "vaults": [
    {
      "id": "<VAULT_ID>",
      "nameEncrypted": "<ENCRYPTED_VAULT_NAME>",
      "secrets": [
        {
          "id": "<SECRET_ID>",
          "type": "LOGIN",
          "payloadEncrypted": "<ENCRYPTED_PAYLOAD>",
          "updatedAt": "<ISO_TIMESTAMP>"
        }
      ]
    }
  ]
}
```

Status endpoints return operational metadata only. They do not decrypt vault content.

## Status And Error Contract

Public API responses include `Cache-Control: no-store` so API snapshots are not cached by browsers or intermediaries. Public v1 routes are dynamic read endpoints and are rate-limited at 120 requests per minute.

| Status | Meaning | Operator action |
| --- | --- | --- |
| `200` | The client is authenticated and authorized for the requested read-only endpoint. | Consume the encrypted snapshot or status metadata. |
| `401` | Client ID or secret is missing, malformed, wrong or revoked. | Create a replacement client, update the consuming system and revoke the old client. |
| `403` | The client lacks the required scope, vault assignment or secret authorization. | Confirm scope, vault assignment and intended endpoint. Secret lookups that are malformed, deleted or outside the allowed vault list return `403 Integration authorization failed.` |

Related:

- [Integration API clients](api-clients.md)
- [Security and trust model](security-and-trust-model.md)
- [Knowledge base: API client access](../../kb/en/api-client-401.md)
