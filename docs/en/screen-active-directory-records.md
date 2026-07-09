# Active Directory Records Screen

The topbar `?` opens this page from the Active Directory records screen. Use it for directory-origin credentials, account metadata and custody review.

## Work Here

- Confirm the record source, domain, account state and last sync before changing custody.
- Treat disabled, locked, expired or privileged directory signals as review prompts.
- Use the DC Agent health path before assuming the record is stale.

## Screen States

| State | Operator response |
| --- | --- |
| Synced | Review owner and last sync before using the record. |
| Orphaned | Confirm the source account still exists before changing vault state. |
| Conflict | Resolve directory source truth before manual edits. |

## Before You Act

- Compare the vault record with provider status before deciding it is stale.
- Check whether the credential is synced, manually imported or awaiting review.
- Preserve the provider evidence trail when changing owner, vault assignment or review state.

## Safe Evidence

- Safe to share: record state, sync age, provider health category and redacted review decision.
- Keep private: distinguished names, OU paths, domain names, bind accounts, agent IDs, agent tokens and raw directory-tree screenshots.
- Use private support when custody, privileged account state or source-of-truth conflicts cannot be explained with redacted metadata.

## Operator Notes

Never publish distinguished names, OU paths, domain names, agent IDs, agent tokens or screenshots with real account metadata.

## Related

- [Domain dashboard screen](screen-domain-dashboard.md)
- [Active Directory agent](active-directory-agent.md)
- [DC Agent troubleshooting](../../kb/en/dc-agent-service.md)
