# In-App Screen Help

Every VaultPilot workspace screen has a topbar `?` button. The button opens the public-safe Markdown page for the current screen and language, so operators can read the right procedure without leaving the context of the task.

Use this index when you are reviewing whether the application shell and public documentation are still aligned.

Two tab-level routes are intentionally more specific than the base workspace route. When the Integrations screen is open on the browser-extension tab, the `?` button opens [screen-browser-extension.md](screen-browser-extension.md). When Server settings is open on the sign-in and session-security tab, the `?` button opens [screen-sign-in-security.md](screen-sign-in-security.md).

| Screen | Help page | Primary decision |
| --- | --- | --- |
| Security Command Center | [screen-security-command-center.md](screen-security-command-center.md) | Decide which operational signal needs attention first. |
| Security dashboard | [screen-security-dashboard.md](screen-security-dashboard.md) | Read posture, 2FA, license and audit-risk signals together. |
| Domain dashboard | [screen-domain-dashboard.md](screen-domain-dashboard.md) | Check directory-sync health before credential work. |
| Certificate dashboard | [screen-certificate-dashboard.md](screen-certificate-dashboard.md) | Track TLS and stored certificate risk. |
| Rotation dashboard | [screen-rotation-dashboard.md](screen-rotation-dashboard.md) | Plan credential rotation without losing custody evidence. |
| New item | [screen-new-item.md](screen-new-item.md) | Choose the correct secret type before saving. |
| Passwords | [screen-passwords.md](screen-passwords.md) | Work with login records safely. |
| API keys | [screen-api-keys.md](screen-api-keys.md) | Store API credentials without publishing or logging them. |
| Secure notes | [screen-secure-notes.md](screen-secure-notes.md) | Keep sensitive text structured and searchable. |
| Certificates | [screen-certificates.md](screen-certificates.md) | Store certificate metadata and encrypted package notes. |
| Files | [screen-files.md](screen-files.md) | Attach approved files without turning the vault into a dump. |
| Active Directory records | [screen-active-directory-records.md](screen-active-directory-records.md) | Review directory-origin credentials and custody state. |
| Sharing | [screen-sharing.md](screen-sharing.md) | Share only the intended records with limits and expiry. |
| Sign-in security | [screen-sign-in-security.md](screen-sign-in-security.md) | Review lock, 2FA and session controls. |
| Discovery | [screen-discovery.md](screen-discovery.md) | Run approved exposure checks and import only confirmed findings. |
| Users | [screen-users.md](screen-users.md) | Manage accounts, roles and access changes. |
| License | [screen-license.md](screen-license.md) | Understand feature gates, trial and read-only state. |
| Audit log | [screen-audit-log.md](screen-audit-log.md) | Prove who did what and preserve the chain. |
| Integrations | [screen-integrations.md](screen-integrations.md) | Configure API clients, extension state and directory connectors. |
| Notifications | [screen-notifications.md](screen-notifications.md) | Route important events without leaking secrets. |
| Executions | [screen-executions.md](screen-executions.md) | Watch active jobs and recover stuck work. |
| Updates | [screen-updates.md](screen-updates.md) | Verify release packages before running updates. |
| Server settings | [screen-server-settings.md](screen-server-settings.md) | Change host, HTTPS, SMTP, maintenance and retention settings. |
| Browser extension | [screen-browser-extension.md](screen-browser-extension.md) | Pair, approve and revoke browser devices. |

Public safety rule: help pages must use placeholders and synthetic examples only. Never add real vault contents, PFX/P12 files, private keys, logs with credentials, API client secrets, license private material or customer screenshots.

Related: [Documentation gateway](../README.md), [Public repository boundary](public-repository-boundary.md), [Public language glossary](public-language-glossary.md).
