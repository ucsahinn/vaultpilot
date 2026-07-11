# Security Screen

The top-bar `?` opens this guide while **Security** is active. Rather than reducing security to one score, this screen shows which record, behavior, or access signal deserves investigation. Every system role can open it, while query content, drill-downs, and actions narrow by role.

The cards are built from vault, audit, license, update, integration, and execution queries. Not every visual is interactive: button-shaped rows and metrics route to source screens, while chart bars and **Risk breakdown** are read-only. The single **Dashboard tools** menu opens documentation, refreshes data, and controls edit mode. There is no per-widget menu; hide and reorder controls appear only in edit mode.

## Reading the Dashboard

- **Security coverage:** all ten weighted factors behind Command Center: 2FA, license, extension, update, password exposure, AD risk, completeness of certificate expiry-date metadata, execution history, directory-provider sync errors, and vault content. The certificate row is not a live validity test, and the directory row is not a general connectivity test. Each row shows earned/total weight and routes to its source.
- **Leak check:** passwords grouped as exposed, clear, or not yet checked.
- **Risk breakdown:** juxtaposes different counts: **Healthy signals** counts healthy score factors, while **Watch items** and **Critical actions** count recommendations after tone normalization. They are not one incident or signal population, and the segments are not buttons.
- **Behavior analysis:** the chart compares access, session, and administrative events. Up to five **Risk access** rows beside it are clickable and open the specific Audit Log event.
- **Audit summary:** the latest six events with actor, target, risk, and time. Only the button in the **Event** column opens that audit event.
- **Access trend:** a read-only seven-day count of unlock, view, copy, fill, and integration-sync events. Day bars do not open a time filter.

## Access and Data Requirements

Owner, Admin, Auditor, and User can open the dashboard, but some system queries and drill-down destinations remain empty, restricted, or disabled for unauthorized roles. Auditors cannot open vault records. Revealing or copying requires a non-Auditor role with readable vault access; writing a vault record also requires **Editor** or **Manager** membership in the active vault and a writable license. System destinations apply their own role gates.

## Investigation Workflows

### Respond to exposed passwords

1. Select the exposed count, donut, or matching status row in **Leak check**.
2. On Passwords, confirm the prepared exposure filter and the record owner.
3. Change the credential in its source system first, update the VaultPilot record, and run the check again.

Completion means the old value is invalid and the replacement returns a clear result. Stop if the source system cannot be changed or ownership is unknown; changing only the vault copy does not contain the exposure.

### Explain an access spike

Identify the day and total behind the increase. The chart does not split event types and its bars are not clickable. Because **Audit summary** contains only the latest six events, use the main navigation to open Audit Log for detailed time and action filters; use a **Risk access** row or **Event** button for a specific event. The expected result is an approved task or explainable user action; otherwise review session and account security through the private incident process.

### Correlate a critical risk with audit activity

**Risk breakdown** is summary-only, so its critical segment does not open detail. Note the count, then use a **Behavior analysis > Risk access** row or the **Audit summary** event button to open the source. Do not assume both cards describe the same event; compare redacted time, action class, and target type. If they disagree, refresh once and pause further changes until the source is verified.

## Screen States

| State | Operator response |
| --- | --- |
| Loading | Do not interpret scores, ratios, or trends until all relevant widgets settle. |
| Healthy | Confirm coverage and unchecked records, then record the review; there is no single global last-refresh timestamp on this screen. |
| Watch | Open the card, verify the destination record or event, and assign follow-up. |
| Critical | Contain potentially affected access first, then investigate record and audit detail privately. |
| Empty | Before reporting no activity, check the active vault, time window, filters, and widget visibility. |
| Unchanged after refresh | Do not look for a global freshness timestamp; verify the source widget query and destination-screen data. |
| Permission limited | Verify role and vault membership when drill-down is unavailable; do not grant broad access as a shortcut. |
| Error | Preserve the message and time, and do not report a partial widget as complete coverage. |

## Before You Act

- Confirm the time window and source represented by the widget.
- Do not treat exposure status as a risk label, or access trend as an audit event; verify each at its source.
- Before clearing a prepared filter, note which dashboard signal opened it.
- Confirm vault role and writable license state before editing a record.
- Hiding a widget in edit mode does not remove its data or risk; restore the hidden component from that mode when needed.

## Safe Evidence

- **Safe to share:** broad risk level, signal category, redacted event class, time range, last check time, and remediation steps taken.
- **Keep private:** usernames, vault names, real record titles, URLs, internal hosts and domains, complete access timelines, and any image showing secret material.
- Never include a value found by the exposure check as an example. If a real password reaches a public surface, change it in the source system before discussing the case.

## When to Stop or Escalate

Escalate when a critical signal survives refresh, access trends conflict with audit records, several users or vaults may be affected, or dashboard data remains stale. Version, timezone-qualified time, widget name, redacted error, and attempted steps are sufficient for private support.

## Operator Notes

This dashboard supports investigation; the authoritative detail remains in the underlying record or Audit Log. A healthy color does not prove that every password was checked. Exposure coverage is incomplete while unchecked records remain.

## Related

- [Security and trust model](security-and-trust-model.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Security Command Center screen](screen-security-command-center.md)
- [Sign-In Security screen](screen-sign-in-security.md)
