# Domain Dashboard Screen

The topbar `?` opens this page from the Domain dashboard. Use it before trusting Active Directory-derived credential records, sync-tree health or directory object counts.

## Work Here

- Confirm the DC Agent is connected before reviewing synced users, groups or credentials.
- Treat stale sync timestamps as operational risk until the agent, URL and token path are checked.
- Use directory counts as health signals, not as public reporting values.

## Screen States

| State | Operator response |
| --- | --- |
| Synced | Confirm last sync age and proceed to credential review. |
| Stale | Check agent service status before editing directory-origin records. |
| Unauthorized | Rotate the provider token and use the repair command from the current provider card. |

## Before You Act

- Check the last successful sync time before assuming records are stale.
- Compare provider health, selected object counts and agent status together.
- Do not repair imported credentials from this dashboard; open the provider or record view that owns the change.

## Safe Evidence

- Safe to share: provider health category, last-sync age, selected object counts by category and redacted error code.
- Keep private: domain names, distinguished names, OU paths, bind accounts, agent tokens and internal directory-tree screenshots.
- Use private support when token repair, bind failure or directory-scope evidence requires real tenant values.

## Operator Notes

Do not publish domain names, distinguished names, OU paths, bind accounts, agent tokens or screenshots of internal directory trees.

## Related

- [Active Directory agent](active-directory-agent.md)
- [Active Directory records screen](screen-active-directory-records.md)
- [DC Agent troubleshooting](../../kb/en/dc-agent-service.md)
