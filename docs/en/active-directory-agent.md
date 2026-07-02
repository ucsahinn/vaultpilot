# Active Directory and VaultPilot DC Agent Service

VaultPilot DC Agent Service runs near the domain controller and synchronizes directory metadata into VaultPilot. It does not send the AD bind password or AD user passwords to VaultPilot.

![VaultPilot Active Directory sync tree](../../assets/screenshots/active-directory-sync-tree.png)

Screenshot note: this capture is retained from the PassMan compatibility line as a temporary layout reference. It is not VaultPilot 2.0 release or branding evidence until the final 2.0 screenshots are recaptured.

## Service Identity

| Item | Value |
| --- | --- |
| Service name | `VaultPilotDCAgent` |
| Display name | `VaultPilot DC Agent Service` |
| Config file | `%ProgramData%\VaultPilot\ad-agent\vaultpilot-dc-agent.json` |
| Service log | `%ProgramData%\VaultPilot\ad-agent\vaultpilot-dc-agent-service.log` |
| Agent log | `%ProgramData%\VaultPilot\ad-agent\vaultpilot-dc-agent.log` |

## Enrollment Flow

1. Open VaultPilot: Integrations -> Active Directory.
2. Create an agent record.
3. Download `vaultpilot-dc-agent.ps1` from the release assets or the UI.
4. Run the install command on the agent machine from an Administrator PowerShell.

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File "$env:USERPROFILE\Downloads\vaultpilot-dc-agent.ps1" -InstallService -PassManUrl "<VAULTPILOT_URL>" -AgentId "<AGENT_ID>" -AgentToken "<AGENT_TOKEN>" -TrustPassManCertificate
```

The generated 2.0 command may still use `-PassManUrl` and `-TrustPassManCertificate`. Treat those as compatibility flag names from the current agent script surface; do not rename them unless the release script adds VaultPilot aliases.

The script asks for:

- Domain controller IP or hostname.
- AD bind username.
- AD bind password through the local terminal prompt.

The password is captured locally, not written to logs, and never posted to VaultPilot.

## Operations Commands

```powershell
powershell -ExecutionPolicy Bypass -File .\vaultpilot-dc-agent.ps1 -Status
```

```powershell
powershell -ExecutionPolicy Bypass -File .\vaultpilot-dc-agent.ps1 -TailLog
```

```powershell
powershell -ExecutionPolicy Bypass -File .\vaultpilot-dc-agent.ps1 -RepairService
```

For an installed service, use the Rotate token command from the existing provider card. The generated repair command keeps the same Windows service and can preserve or update the DC host and bind username. On VaultPilot 2.0.0 and newer, freshly generated or rotated agent tokens are authorized independently of server-secret/data-directory context drift on the server; the same fix first landed in the PassMan 1.8.19 compatibility line.

```powershell
powershell -ExecutionPolicy Bypass -File .\vaultpilot-dc-agent.ps1 -UninstallService
```

## What Appears In VaultPilot

After sync, the Active Directory tab shows:

- Provider status and last sync.
- Domain controller, domain, base DN and agent version.
- OU, group and user tree with search.
- Separate checkbox scopes for login access and credential import.
- Import action for selected credential candidates.

## Hardening Notes

- Prefer `DOMAIN\username` or `username@domain.local` for bind users.
- Use a delegated account with the narrowest read scope that meets the sync need.
- Keep the agent on a controlled Windows host close to the DC.
- Rotate the agent token if the setup command was copied into an unsafe channel.
- Use the VaultPilot UI to revoke or recreate the agent record when rebuilding the agent machine.

## Troubleshooting

| Symptom | Action |
| --- | --- |
| Service does not install | Run Administrator PowerShell and inspect the service log. |
| Wrapper compile fails | Use the latest `vaultpilot-dc-agent.ps1`; repair stops the old service and rebuilds the wrapper safely. |
| VaultPilot URL unreachable | Test the URL from the agent machine and verify firewall/DNS. |
| Install or repair returns 401 Unauthorized | On VaultPilot 2.0.0 and newer, use the published release or an internally approved build. On older compatibility deployments, use PassMan 1.8.19 or newer. Then rotate the provider token and rerun the displayed command. If it still fails, check the server log for the redacted reason: `provider_not_found`, `token_revoked`, `token_missing` or `token_mismatch`. |
| Sync shows zero objects | Confirm bind account scope and base DN. |
| Agent connected but tree stale | Use Sync now, then check service and agent logs. |
