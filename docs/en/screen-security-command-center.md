# Security Command Center Screen

The `?` button in the top bar opens this guide while Security Command Center is active. This is where VaultPilot answers ?what needs attention first?? by bringing the security score, priority recommendations, server readiness, and operational signals into one workspace. Every system role can open it, while visible data and destination actions narrow by role. It is not an incident report or change approval by itself.

Command Center is primarily a routing surface. Selecting a recommendation or factor opens the relevant Passwords, Active Directory Records, Sign-In Security, Integrations, License, or Update Center view and prepares a useful filter when one is available.

## What You Can See

- **Security score:** calculated from ten weighted factors: 2FA, license mode, browser extension, Update Center, password exposure checks, Active Directory risk, completeness of certificate expiry-date metadata, failed executions, sync errors reported by directory providers, and vault content. The certificate factor is not a live validity/expiry test, and the directory factor is not a general connectivity test. A score is not a verdict.
- **Critical and watch recommendations:** the main surface shows two critical and two watch rows. **More recommendations (n)** opens the rest of the prioritized queue; its rows also route to their source screens.
- **Score sources and dashboard sections:** direct routes into Security, Domain, Certificates, and Rotation dashboards.
- **Current operation signals:** live summaries such as file quota, execution state, and update readiness.
- **Screen tools:** refresh live data, open this documentation, and manage the dashboard view.

## Access and Prerequisites

Owner, Admin, Auditor, and User can open the screen, but some system queries, destinations, and actions remain empty, restricted, or disabled for unauthorized roles. Vault-record drill-downs require an unlocked vault and system/vault access that permits secret use; Auditors cannot open secret records. Read-only mode blocks vault-record creation and changes. License and Integrations are Owner-only; Server Settings reads allow Owner/Admin/Auditor while server mutations are Owner-only.

## Recommended Workflows

### Run the daily security review

1. Read the score, earned/total weight, and open recommendation count together; this screen has no independent score-freshness indicator.
2. Open the first item under **Critical**; VaultPilot routes to the relevant screen and applies a focused filter where appropriate.
3. Confirm the underlying condition, complete the work on that screen, return, and refresh Command Center.

The expected result is either a healthy signal or an explicitly owned follow-up. If the same recommendation remains after refresh, do not make repeated blind changes. Inspect the source screen's error and timestamp first.

### Explain a score decrease

Select the lowest or warning-toned score source. Separate 2FA, license, extension, update, exposure, AD risk, certificate expiry metadata, execution history, directory-provider errors, and vault-content causes, then verify the source screen. Stop and check Server Settings or Executions if the score loss cannot be tied to one concrete control.

### Turn a recommendation into owned work

Open the recommendation, verify the affected record or subsystem, and capture its owner and due time in the organization's change process. Command Center recommendations have no hide or dismiss control. Completion means the source control is corrected and the recommendation leaves the queue after refresh.

## Screen States

| State | Operator response |
| --- | --- |
| Loading | Wait for the cards to settle before interpreting a score or count; refresh once if loading is unusually long. |
| 82?100 | The score is in the green band; still inspect open recommendations and each factor?s weight. |
| 62?81 | The score is in the warning band; verify the highest-impact row at its destination. |
| 0?61 | The score is in the critical band; contain direct access risks first and move the case to the private process. |
| More recommendations | Open the hidden queue; the first four rows may not represent all outstanding work. |
| Readiness signal missing | Open Profile, Active vault, 2FA, License, Extension, or Update Center and verify the source. |
| Permission limited | If a destination or action is unavailable, verify the role and vault membership through the normal access process. |
| Error | Preserve the message, time, and affected component; avoid repeated refreshes that erase the first useful evidence. |

## Before You Act

- Determine whether a signal concerns one vault, a user session, licensing, or a server subsystem.
- Use the card's own route so exposure and risk filters carry into the destination screen.
- Before writing a **vault record**, confirm the active vault role is **Editor** or **Manager** and the license is not read-only. Server, license, and integration destinations apply their own system-role and license rules instead of this vault-role gate.
- When several items are critical, handle direct access risks such as missing 2FA and known exposure first.
- Treat Command Center counts as orientation, not final audit evidence; verify the relevant record, audit event, or execution result.

## Safe Evidence

- **Safe to share:** the broad score band, recommendation category, affected VaultPilot component, redacted error code, observation time, and destination screen name.
- **Keep private:** usernames, vault names, real record titles, internal domain and host names, customer counts, access timelines, and any screenshot that could reveal a secret.
- If a screenshot is necessary, capture only the relevant card and redact navigation, user, host, and record context. Use private support when the environment cannot be fully de-identified.

## When to Stop or Escalate

Escalate internally when a critical signal returns after a verified fix, score sources cannot load, dashboard summaries conflict with audit evidence, or a risk affects several users. A support package should contain version, timezone-qualified timestamps, component, steps taken, and redacted errors?never secret values.

## Operator Notes

Command Center accelerates triage; it does not replace the destination screens and offers no recommendation-card hide control. Confirm the outcome in the target screen and, where relevant, in the Audit Log.

## Related

- [Audit and security posture](audit-and-security-posture.md)
- [Security and trust model](security-and-trust-model.md)
- [Security Dashboard screen](screen-security-dashboard.md)
- [Operator runbook](operator-runbook.md)
