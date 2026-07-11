# Audit Log Screen

The topbar `?` opens this guide for the Audit Log. The screen is more than a chronological list: it brings the actor, affected target, role, timestamp, operation details, and integrity hashes into one investigation context.

The **Operations > Audit log** navigation is shown only to Owner, Admin, and Auditor roles. The GET API that lists audit events accepts every authenticated role, including User. Do not treat navigation visibility and API authorization as equivalent; server-side role enforcement remains authoritative for each request. The screen does not modify existing events. CSV and Excel exports contain the raw events allowed by the current filters.

## Work Here

- Narrow the list with category buttons, the **Action type** selector, and **Search audit**.
- Check the raw event count, selected category, and action type before exporting. The search term is not shown in this summary.
- Open a row to review actor, target, role, time, operation details, the current event hash, and the previous hash together.
- Use **Clear filters** to return to the full view; CSV and Excel export only the visible result set.
- An `Nx` marker means events with the same action, actor, and target in the same minute are grouped into one display row.

## How to Read the Screen

Category buttons divide events into meaningful groups, and each count represents raw events in that category. **Action type** isolates one operation. Search matches action label, actor, target, narrative, details, timestamp, hashes, and target ID. There are no separate actor, target, risk, or time filter controls.

The result summary shows raw event count, selected category, and action type; it omits the search term. Events sharing action, actor, target, and minute are grouped into one representative row with an `Nx` marker. Opening that row shows only the representative event, not every member. Category counts, the result summary, and exports continue to use ungrouped raw events.

The detail drawer shows actor, target, role, time, operation metadata, current hash, and previous hash. These are fields for manual comparison; the screen does not calculate or display a complete, partial, or invalid chain state. For critical changes, open adjacent events and compare their order and hash linkage manually.

## Investigation Workflows

### Find one operational change

1. Establish the approximate time and likely actor or target.
2. Select a category, then choose **Action type**.
3. Use **Search audit** for the final narrowing step.
4. Open the row and confirm that actor, target, role, and timestamp fit the expected operation.

The expected outcome is an identified event that retains its surrounding context. If nothing appears, do not conclude that logging failed. Choose **Clear filters**, check spelling and time-zone assumptions, then search again.

### Compare event hashes manually

1. Open the relevant event detail.
2. Preserve both the current event hash and the previous hash.
3. If the row is marked `Nx`, note that the drawer represents only one event from the group.
4. Use search and export to compare adjacent raw events in the same time window.

The presence of hashes does not mean the application has validated the chain on this screen. If the previous hash is absent, unexpected, or appears not to match the adjacent raw event, keep records unchanged and escalate privately with a narrow time window and redacted context.

### Export a tightly scoped evidence set

1. Reduce category, action type, and search term to the smallest useful scope.
2. Record raw event count, category, and action type; record the search term separately.
3. Choose CSV or the Excel-compatible table according to the fields required.
4. Store the filters in a separate investigation note because the file does not describe its own filter scope.
5. Keep the original private and immutable; redact user, object, IP, and customer context in the shareable copy.

CSV includes `created_at`, `action`, `actor`, `target`, `summary`, `details`, `target_id`, `integrity_hash`, and `previous_hash`. The **Excel** button does not create `.xlsx`; it creates an Excel-compatible HTML table with a `.xls` extension. That table contains Created, Action, Actor, Target, Summary, Details, and Integrity hash, but omits `target_id` and `previous_hash`.

When the filtered raw event count is zero, both export buttons are disabled and no empty file is created. After downloading a file, each export requests a new `EXPORT` audit event and refreshes the list. The event is recorded only if the server accepts that write. For example, an Auditor can download the file, but the `EXPORT` event may be absent because the Auditor role cannot create audit events. Even when recorded, the new event is not present in the file prepared before it.

### Hold a safe position during an active incident

For suspected unauthorized access, an unexplained role change, or unexpected hash linkage, pause non-essential administrative changes. Preserve the time window, actual filter scope, and relevant hashes, then hand the case to the incident owner. Do not run cleanup or alter retention while review is active.

## Screen States and Operational Conditions

| State | Operator response |
| --- | --- |
| Loading | Wait for skeleton rows to resolve before changing filters. |
| No filtered results | Clear filters, then re-check time and search text. |
| Grouped `Nx` row | Remember that the drawer shows a representative event while counts and exports use raw events. |
| Export disabled | The filtered raw event count is zero; review the filters. |
| Export completed | Keep a separate scope note; the `EXPORT` event appears only if the server accepts the write. |

## Before You Act

- Set category, action type, and search term before exporting; there are no separate actor, target, or time filters.
- Account for `Nx` grouping when manually comparing hashes and adjacent raw events.
- Stop non-essential changes if hash linkage is unclear and an active incident is underway.
- Decide the secure storage location and intended recipients before exporting.
- Coordinate cleanup or retention work with the evidence owner before it affects raw history.
- Record search term, time-zone assumption, category, and action type in a scope note separate from the file.

## Safe Evidence

- Safe to share: event category, narrow time window, redacted actor role, a short hash prefix, and the actual filter scope.
- Keep private: usernames, object IDs, raw audit exports, internal IPs and incident material with customer context.
- If a previous hash is missing or unexpected, preserve evidence and state clearly that this screen does not produce a visible chain-health result.
- Keep category, action type, search term, and raw event count in the shareable copy because the export is not self-describing.
- Never upload raw CSV/Excel, detail-drawer metadata, or customer context to a public channel.

## When to Stop and Escalate

Stop administrative changes when hashes cannot be reconciled with adjacent raw events, actor or target cannot be reconciled, exports omit expected events, or an active security incident is underway. Open a private case with category, action type, search term, narrow time range, redacted actor role, and event hashes?never raw customer data.

## Operator Notes

Audit evidence can expose usernames, internal object IDs and operational timing. Redact public issues and use private support for real incident material.

## Related

- [Audit and security posture](audit-and-security-posture.md)
- [Audit chain partial KB](../../kb/en/audit-chain-partial.md)
- [Support evidence pack](support-evidence-pack.md)
