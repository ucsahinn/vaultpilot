# Domain

The top-bar `?` opens this guide while Domain is active. Its four widgets combine different sources: the DC Agent sync snapshot and selected directory scope, RDP/SSH records in the vault, credential-access audit events, directory work, and browser sessions that may already be cached. These sources do not share one scope or refresh time, and their totals are not a complete inventory of Active Directory.

Domain is primarily a review surface. Some cards open a filtered destination, while other metrics are read-only. A populated widget has no generic **Open related view** menu; that call to action may appear only in a compact empty state. In populated views, use a card rendered as a button or navigate to the destination from the sidebar.

## The Four Widgets

### Domain inventory

Shows the live-agent ratio, user, group/OU, and risk metrics together with provider name, last seen/sync time, and selected sign-in and credential counts. Its source is the directory-provider query, which runs only for Owners. Topology, metrics, and provider rows inside this widget are read-only; use sidebar navigation for Integrations > Active Directory.

### Domain sync health

Clickable **Users**, **Groups**, and **OUs** rows open the corresponding directory-tree filter under Integrations; they are disabled when the count is zero or the operator is not an Owner. **Computers**, **Privileged**, and **Stale** rows are read-only. The **Agent queue** card uses pending/leased directory-action counts and opens Executions when non-zero and system visibility is available. Other scope cards and agent-health rows are informational.

### Remote sessions

Clickable RDP and SSH cards combine vault credential counts with audit access events and open Active Directory Records with the matching protocol filter. **AD login** is a read-only selected-scope count from the provider. **Agent queue** comes from directory actions and may route to Executions. The access chart comes from audit events; browser-session rows come from the session query. Domain does not activate that session query itself, so only data cached by an authorized security screen may appear. Use Sign-In Security for a current, authoritative session review.

### Credential lifecycle

This widget is derived from Active Directory credential records in the vault and their audit access events, not from selected directory scope. **Credentials**, **Managed**, **Expired**, and **Information** cards open Active Directory Records with the corresponding filter. **In use** and **Updated** cards are read-only. There is no Unmanaged lifecycle KPI. Access charts and the device, credential, last-view, and total table are also read-only.

## Access, Data, and Agent Capabilities

The directory-provider query is enabled only for Owners. If an Admin, Auditor, or User reaches the dashboard shell, empty or zero values mean **data was not loaded because of permission**, not “no agent exists.” Even as Owner, wait for the query to complete before interpreting an empty state.

Capabilities advertised by the agent constrain both data and actions. Inventory requires `READ_INVENTORY`; password-state information requires `READ_PASSWORD_STATE`. Unlock, require-password-change, and temporary-password operations require `UNLOCK_ACCOUNT`, `REQUIRE_PASSWORD_CHANGE`, and `RESET_TEMP_PASSWORD` respectively. When a capability is absent, zero or missing data does not mean healthy—it may not have been collected. Sensitive actions also require a `CONNECTED` agent, writable license, Owner role, and a target that is not marked privileged.

## Recommended Review Workflows

### Verify agent health

1. Read the live-agent ratio, provider state, and last seen/sync times in Domain Inventory.
2. Read status precedence correctly: when agent health is not `CONNECTED`, health labels such as `STALE`, `OFFLINE`, `AWAITING`, or `REVOKED` win. For a connected agent, `ERROR` wins first, then `SYNCING`; only a connected, error-free, idle agent with a pending command shows **SYNC QUEUED**.
3. For a non-connected or error state, use sidebar navigation to open Integrations > Active Directory and inspect the provider card.

The expected result is `CONNECTED` with advancing last-seen and synchronization times. Stop imports and scope changes while those timestamps remain stale.

### Reconcile selected scope with counts

Open a clickable **Users**, **Groups**, or **OUs** row in Domain Sync Health and inspect the prepared filter under Integrations. Computers are read-only; navigate to Integrations for computer scope. For an unexpected increase or decrease, compare the last successful synchronization and advertised capabilities. Completion means the change is explained by an approved scope update or a confirmed source-system issue.

### Investigate an RDP/SSH signal

Select a non-zero RDP or SSH card and confirm the protocol filter on Active Directory Records. Review source, risk label, and last sync time there. Do not expect browser-session rows or the access chart to open detail; those elements are summaries only.

### Review lifecycle state

Open only **Credentials**, **Managed**, **Expired**, or **Information**, then confirm the filtered list. **In use**, **Updated**, and the access table are summaries only. Do not manually recreate a record sourced from `ad_sync`. Pause bulk work when the record and directory object disagree until synchronization completes.

## Screen States

| State | Operator response |
| --- | --- |
| Loading | Do not interpret totals or empty states until the Owner query completes. |
| `CONNECTED` | When no error, sync, or command is active, confirm timestamps advance and required capabilities are advertised. |
| `ERROR` | On a connected agent, error takes precedence over sync and queue labels; inspect the provider's latest error. |
| `SYNCING` | Appears only for a connected, error-free agent; wait for the current synchronization. |
| SYNC QUEUED | Appears only for a connected, error-free, idle agent with pending work; track it in Executions. |
| `AWAITING` | Do not import or run sensitive work before the first agent poll completes. |
| `STALE` | Check the agent service, server reachability, and latest provider error. |
| `OFFLINE` | Stop new directory work and collect service/connectivity evidence privately. |
| `REVOKED` | Do not reuse the old agent token; follow the Owner-approved enrollment or repair path. |
| Empty by permission | On a non-Owner role, never report zero as no agent; hand the review to an Owner. |
| Capability missing | Treat the data or action as unsupported, not as a healthy zero result. |
| Error | Preserve the last successful sync time and avoid repeated scope changes that hide the first failure. |

## Before You Act

- Confirm the operator is an Owner, the provider query completed, and timestamps are current.
- Evaluate agent health together with the last successful synchronization.
- Confirm the agent advertises the capability required for the data or action.
- Distinguish a read-only metric from a clickable filter card.
- For credential import, confirm the active vault is unlocked, writable, and its key is available.
- Do not force sensitive actions against privileged accounts; use the approved Active Directory administration path.

## Safe Evidence

- **Safe to share:** agent health category, age of last seen/sync, de-identified totals by object type, queue state, advertised capability name, and an error code without personal data.
- **Keep private:** domain and domain-controller names, distinguished names, OU/group paths, bind identity, agent token, real user lists, RDP/SSH targets, and directory-tree screenshots.
- If logs are required, remove user, domain, IP, token, and LDAP detail. Use private support when complete redaction is not possible.

## Escalation

Escalate to directory operations when an agent cannot return to `CONNECTED`, `SYNCING` or queue state does not advance, selected scope changes unexpectedly, a required capability disappears, or this screen conflicts with Active Directory Records. Agent version, broad health state, timezone-qualified timestamps, redacted error, and attempted preflight steps are sufficient.

## Operator Notes

Object counts are capacity and health signals, not a public identity inventory. Active Directory and the agent are authoritative for directory-sourced credential records. Creating the same record manually introduces duplicate and incorrect-rotation risk.

## Related

- [Active Directory agent](active-directory-agent.md)
- [Active Directory Records screen](screen-active-directory-records.md)
- [Sign-In Security screen](screen-sign-in-security.md)
- [DC Agent troubleshooting](../../kb/en/dc-agent-service.md)
