# Notifications Screen

The topbar `?` opens this guide for the Notifications screen. This screen controls which persisted audit events are eligible for SMTP email and which addresses receive those emails. SMTP server connectivity lives on the separate **Server settings > SMTP** tab; live application notifications in the topbar are a different, session-scoped surface.

## Access, Role, and License Boundary

Owner, Admin, and Auditor system roles can open Notifications. Only the **Owner** can change recipients or event selections, save settings, and send an SMTP test. Admin and Auditor see the same data read-only. The User role cannot view system settings and therefore cannot open this screen.

Notifications is not gated by a separate license feature. **Read-only** on this screen describes a non-Owner system role, not the license mode. A read-only license that blocks vault writes also does not automatically disable these server-level settings or SMTP tests for an Owner; apply any stricter organizational policy separately.

## Work Here

- Read SMTP enabled/disabled state, normalized recipient count, and selected event-rule count.
- Add, deduplicate, or remove addresses under **Email recipients**.
- Use **Test recipient** to check the current SMTP form values before saving.
- Filter the event catalog with **All**, **Selected**, **Info**, **Suspicious**, and **Critical**.
- Change one event, an entire severity group, or the full catalog's email selection.
- Read each row's **Immediate**, cooldown, or threshold policy before balancing visibility and noise.
- **Save notifications** and **Reset** operate on the full form shared by Notifications and the other Server settings tabs. Do not use either action while another tab has unsaved changes.

## Screen Structure

The Notifications screen has no tabs of its own. It contains a status strip and two main areas:

- The SMTP status button and **SMTP settings** open **Server settings > SMTP**.
- **Delivery** contains the recipient list and SMTP test.
- **Event rules** contains filters, bulk selection, severity groups, and individual event rows.

**Ready to send** means only that SMTP is enabled in the form, host and sender are populated, and at least one recipient and event are selected. It does not prove that the SMTP connection works, a remote server accepted a message, or a recipient inbox received it.

## Delivery and SMTP

### Recipient list

Each line, comma, or semicolon separates recipients. Before saving, addresses are lowercased, blank entries are removed, and duplicate addresses are retained only once. While SMTP is enabled, host, sender email, and at least one recipient are required. When authentication is enabled, username and either a new or previously stored password/token are required.

Notifications does not edit SMTP account name, host, port, sender, TLS/STARTTLS, authentication username, or password. Manage those on the separate **SMTP settings** tab. When SMTP is disabled, connection details are retained; audit records and session-local application notifications continue while email delivery stops. Email candidates created during that period are skipped during processing and their outbox rows are deleted; they are not backfilled when SMTP is re-enabled.

### Test delivery

**Send test** is available only to an Owner, while SMTP is enabled, and while no other test is running. A test requires:

- A valid port from `1-65535`,
- SMTP host and sender email,
- A separate **Test recipient**,
- When authentication is enabled, a username and either the form password/token or a previously stored value.

The test can use valid unsaved SMTP form values. While SMTP is enabled, the server also requires at least one notification event selection in the test request; with zero selections, the button may appear available but server validation rejects the test. The server accepts at most five test requests per ten minutes. An address in the success notice means the SMTP server accepted that recipient; it is not proof of final inbox, quarantine, or end-user delivery. A successful test writes a `SERVER_MAINTENANCE` audit event. A failed test produces an on-screen error and live application notification, but does not create successful-delivery evidence. The current test message template is generated in Turkish; changing the interface language does not change the test email language.

## Event Rules and Severity Groups

Filters change only the visible rows, not saved selection:

| Filter | Shows |
| --- | --- |
| All | Every audit event defined for SMTP. |
| Selected | Events currently marked as email candidates. |
| Info | Maintenance and informational events. |
| Suspicious | Suspicious access and review-required signals. |
| Critical | Critical security and action-required events. |

**Select all** marks every event. **Clear** removes all marks. If SMTP is enabled with zero selected events, **Save notifications** remains disabled and the SMTP test is also rejected by server validation; select at least one event before saving or testing. If SMTP is disabled, settings can be saved with no selected event.

The checkbox in a severity header selects or clears the entire group; a partial selection appears as a mixed checkbox. An individual row changes only that event. Unselected events are not deleted and remain in Audit Log; they are simply not eligible for SMTP email.

### Delivery policy

Selection does not mean every occurrence immediately sends an email. Each row shows its policy:

- **Immediate:** the event becomes eligible for the SMTP queue when it occurs.
- **First event, then Nm cooldown:** the first event is eligible and the same group is suppressed during cooldown.
- **N events / Mm:** the event becomes eligible only after the threshold is reached inside the stated window.

Grouping can use actor or actor-and-target depending on the event. The server processes eligible emails through a persistent outbox and retries transient failures a bounded number of times; permanent rejection or the attempt limit can still prevent final delivery. Notifications has no per-recipient delivery receipt, read status, or outbox history. Event selection and **Rules ready** therefore are not delivery guarantees.

## Live Notifications and Persisted Events Are Different

The topbar bell and live notifications visible for about 5.2 seconds represent action successes, errors, and system messages in this browser session. At most three live notifications appear at once. The bell center keeps up to 30 notifications in session memory and displays the newest eight; repeated notifications with the same kind and message are deduplicated.

**Mark read** preserves timestamps while marking current entries read. When read entries exist, **Clear read** removes only them; if none are read, **Clear all** empties the current session list. Dismissing one row also removes its live notification when still visible.

This live list is not persisted to the server database and is not expected to return after a page/session reload. Clearing the bell center does not delete Audit Log, the SMTP outbox, saved event rules, or sent email. Conversely, a persisted audit event does not necessarily produce either a live notification or an email.

## Recommended Workflows

### Verify a first SMTP notification setup

1. Under **SMTP settings**, enable SMTP and enter host, port, sender, TLS, and authentication when required.
2. Return to Notifications and add at least one real recipient.
3. Start with a narrow event set and read each row's threshold or cooldown policy.
4. Choose **Send test** for a separate test recipient and confirm SMTP acceptance.
5. Check inbox, spam/quarantine, and the organization's mail-gateway evidence separately.
6. Confirm that no other Server settings tab has unsaved changes; then choose **Save notifications**, reopen the screen, and confirm recipient and event counts remain.

### Reduce noise

1. Use **Selected** to show only email-candidate events.
2. Review threshold and cooldown policies for high-volume rows first.
3. Clear rows that do not require human action; clear an entire severity group only under an explicit organizational decision.
4. Save and confirm unselected events continue to appear in Audit Log.

## Screen States

| State | Operator response |
| --- | --- |
| Server settings loading | There is no dedicated skeleton here; do not treat the temporary default SMTP-off form as confirmed state or save before values load. |
| Server settings unavailable | The panel may not show a dedicated error card. If expected recipients or rules are missing, verify Server settings and connectivity, then refresh; do not overwrite known settings with an empty form. |
| SMTP off | No email is sent; audit and session-local notifications continue. Skipped email candidates are deleted from the outbox and are not backfilled after SMTP is re-enabled. |
| Needs attention | SMTP is enabled but host, sender, recipient, or event selection is incomplete. |
| Ready to send / Rules ready | Only form completeness is established; testing and recipient-side verification are still required. |
| No recipients | Add at least one valid address while SMTP is enabled. |
| No event selected | With SMTP enabled, at least one event is required before saving; even if the test button appears available, server validation rejects the test request. |
| No events in filter | Switch to **All** or another severity; saved selection does not change automatically. |
| Sending test | Do not start a second test; wait for the result or error notification. |
| Test accepted | The SMTP server accepted the address; verify inbox delivery separately. |
| Test failed | Check host, port, TLS, authentication, sender, recipient, and network access without exposing credentials. |
| Role read-only | Admin and Auditor can review rules but cannot change, save, or test them. |
| Unsaved changes | The shared form also contains changes from other Server settings tabs. **Save notifications** can persist them together; **Reset** can return them all to the last loaded values. |
| No live notifications | This means only that the current browser session has no new action result; it does not prove Audit Log is empty. |

## Before You Act

- Confirm the session role; recipient, rule, SMTP test, and save actions require Owner.
- Before using **Save notifications** or **Reset**, confirm that no other Server settings tab contains unsaved values; both actions affect the entire shared form.
- Confirm SMTP is enabled and remember that **Ready to send** indicates form completeness only.
- Verify organizational approval, data classification, and on-call ownership for every recipient address.
- Read the event row's severity and actual delivery policy; do not assume selection means immediate email.
- Record current recipient and selected-event counts before changing them, without putting real addresses in public evidence.
- Account for the test using unsaved SMTP values and being rate-limited.
- Do not use the live bell center as a substitute for persisted Audit Log.

## Safe Evidence

- Safe to share: SMTP enabled/disabled class, redacted host class, port and TLS mode, recipient count, event name/severity, delivery policy, general error code, and broad time window.
- Keep private: SMTP username and password/token, real recipient and sender addresses, full hostname, message ID, subject/body, audit target, user/vault name, exact incident time, and internal routing information.
- When sharing a test result, mask the accepted address, SMTP host, and message ID; do not present **accepted** as proof of final delivery.
- Do not rely on cropping alone in screenshots; fully mask addresses, hosts, event targets, users, timestamps, and customer context.

## When to Stop and Escalate

Stop if you cannot confirm that loaded values are current, expected recipients disappear, a test goes to the wrong address, SMTP credentials reach a public channel, critical events exist in Audit Log but no queue/mail evidence appears, or one rule produces unexpectedly high email volume. Open a private support case with general SMTP state, redacted event name, delivery policy, broad time window, error code, and last safe step—without secret material.

## Operator Notes

Notifications is not a mailbox or delivery-monitoring console. It stores recipients and event rules; SMTP connection details live under Server settings. Audit records, the SMTP outbox/email channel, and browser-session live notifications have separate lifecycles.

Never publish a notification example containing an SMTP password/token, real email address, customer hostname, message ID, full error response, or incident-specific secret value.

## Related

- [Server settings screen](screen-server-settings.md)
- [Audit Log screen](screen-audit-log.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Server settings restart and maintenance KB](../../kb/en/server-settings-restart-maintenance.md)
