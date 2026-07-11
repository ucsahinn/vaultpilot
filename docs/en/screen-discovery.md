# Discovery Screen

The topbar `?` opens this guide from **Operations > Discovery**. Discovery is a controlled review workspace for approved private-network, TLS, and file-exposure checks. It produces signals and redacted evidence for an operator to review; it is not a vulnerability scanner, credential-testing tool, asset inventory, or automatic cleanup service.

## Access, Role, and License Boundary

Owner, Admin, and Auditor can open Discovery when the license includes the **Discovery** capability. Admin and Auditor have a read-only view of policies, runs, findings, suppressions, and import state. User cannot open the screen.

Every change requires Owner, the Discovery capability, and a writable license. This includes saving a scan, Preview or Run, stopping/restarting/deleting a run log, reviewing or suppressing findings, preparing import material, and completing import. Import also requires an unlocked active vault where the Owner has Editor or Manager access.

The workspace refreshes about every ten seconds while open. Loading uses a three-row skeleton; a workspace query failure has a dedicated error panel.

## Three-Step Workflow

1. **Run** — compose and save approved scope, select checks, record a Preview, or perform a Run.
2. **Findings** — filter redacted signals, inspect evidence, and make review decisions.
3. **Import** — optionally add a narrow class of reviewed file findings to the active vault.

Import is optional. A network surface, certificate issue, or weak file signal can remain an operator finding without becoming a vault record.

## Run: Build an Approved Scan

### Select checks

Only selected and available checks run:

| Check | Actual behavior | Required saved scope |
| --- | --- | --- |
| Login surfaces | Connects to selected ports and issues bounded HTTP/HTTPS `GET` requests to known and same-origin login paths. It does not submit forms or credentials. | At least one accepted private IPv4 target. |
| SSL/TLS certificates | Opens TLS connections and reads certificate metadata, including validity, hostname/fingerprint, self-signed/internal-CA, duplicate-fingerprint, and AD CS web evidence. | At least one accepted private IPv4 target. |
| Exposed secrets in files | Reads approved files transiently and creates metadata-only/redacted findings for supported secret, credential, certificate, and key signals. | At least one resolved preset or approved path. |

Quick choices select all available checks, Files only, or Network + SSL/TLS. Network and file work can run together. They execute concurrently, so failure in either branch fails the overall run.

### Private-network scope

Network scope accepts individual RFC1918 IPv4 addresses, CIDR, or explicit IPv4 ranges. Public addresses, hostnames, IPv6, loopback, and link-local targets are not accepted. The combined limit is 512 hosts; an explicit range must remain inside one `/24`. A nonempty scope containing any rejected entry cannot be saved.

The target preview expands accepted addresses, shows rejected entries, and displays at most 64 matching targets before summarizing the rest. It is a local scope preview, not a reachability test.

Port plans provide common low-noise sets: Premium default, Web login, Windows identity, and Narrow TLS. A policy accepts at most 32 unique ports. The default set is `443, 8443, 9443, 636, 3269, 5986, 80, 8080`.

Network checks make real traffic: TCP connections, TLS handshakes, and bounded HTTP/HTTPS GET requests. Up to 64 KiB of an HTTP response body can be sampled to classify login or AD CS evidence, and a limited set of same-origin login links can be followed. No username, password, authentication form, exploit, brute force, or password spray is sent.

TLS probing deliberately reads certificate metadata even when the certificate is invalid or untrusted. IP-literal targets do not send SNI. A certificate finding is risk evidence; it is not proof that a trusted TLS connection succeeded.

### File scope and presets

Preset groups resolve on the VaultPilot server:

- Windows folders: Desktop, Documents, Downloads, OneDrive, Public Desktop, and Public Documents.
- Server applications: IIS configuration/site/log locations and Nginx or Apache configuration paths.
- DevOps and admin: eligible `.ssh`, `.kube`, `.docker`, `.aws`, Azure, and gcloud profile folders.

Presets can expand across eligible local Windows profiles. What can actually be read depends on the VaultPilot server service account. A missing or inaccessible preset path may simply yield no files.

Additional scope accepts approved absolute drive paths or normal UNC paths. The saved policy resolves at most 32 paths. Drive roots, traversal paths, device paths, most Windows system paths, VaultPilot/legacy PassMan data paths, symbolic links, generated directories/files, unsupported extensions, inaccessible entries, and oversized files are skipped or rejected.

The policy permits at most 80 allowed extensions. Default maximum file size is 5 MB; the hard limit is 25 MB. Timeout is 250–15,000 ms and concurrency is 1–16.

File inspection can transiently read supported text, configuration, scripts, VPN/RDP, registry, Terraform, package-manager credential files, certificate/key files, and supported Office/Excel OOXML content into server process memory. Persistent Discovery data contains detector metadata, masked paths, hashes, reason codes, and a redacted preview—not the source secret value. Source files are never changed, moved, quarantined, cleaned, or deleted.

### Explicit approval and policy behavior

Network scope requires **I am authorized to scan these private targets**. File scope requires **These file paths are approved for read-only scanning**. Editing either scope clears its corresponding approval. A scan can be saved only with valid network scope, approved file scope, or both.

**Save scan** always creates a new policy; the current screen has no saved-policy edit or delete action. Clearing **Scan enabled** creates a Disabled policy. The Run button is disabled for it; Preview can still appear enabled in the current UI, but the server rejects Preview and Run for a Disabled policy.

## Preview, Run, and Job Controls

Preview and Run are intentionally different:

- **Preview** records an immediately completed `PREVIEW` job and audit event. It performs no TCP, TLS, HTTP, or file probes and creates no findings.
- **Run** performs the selected checks. It can take several minutes and returns only after the run reaches a terminal state, while polling can expose persisted progress.

Only one job may be active per policy. Job states are Queued, Running, Cancellation requested, Completed, Cancelled, and Failed. Progress shows targets scanned, files scanned, findings processed, and the latest update.

**Stop** records a cancellation request. Cancellation is not immediate: the policy remains active and cannot start another run until the runner acknowledges it. **Delete** is available only for a terminal job after confirmation; it deletes the run log but preserves related findings. **Restart** uses the saved policy and the checks currently selected for that policy, not an immutable copy of the original run's check selection.

The process-log panel shows the six most recent jobs. The expanded run history lists all returned jobs. A server restart can cause an abandoned active job to be recovered later as interrupted or cancelled.

The displayed findings count is the number of processed/upserted signals for the run; it is not guaranteed to be a count of brand-new unique finding rows.

## Findings: Review Redacted Signals

The initial Findings view intentionally shows **High-confidence + Open** findings. Restore default view returns to that filter, not to all findings. Search and advanced filters cover confidence, status, severity, source kind, candidate type, asset identity, reason codes, masked path, and hashes.

The first page loads 200 findings. **Load more findings** retrieves older pages; the API allows at most 500 per page. Filters, bulk selection, review counts, and Import operate on findings loaded into the browser. Selections outside the current filter remain selected until cleared.

The table and detail drawer show severity, confidence, candidate type, asset identity, redacted preview, detector, reason codes, status, compact evidence hash, optional masked path/path hash, and updated time. Even masked evidence can identify internal systems; keep it private unless deliberately sanitized.

### Finding lifecycle

| Current state | Available decisions |
| --- | --- |
| Open | Start review, Ignore, Suppress |
| In review | Allow Add to vault for eligible file material, Ignore, Suppress, Reopen |
| Ready to import | Open Import for eligible material, or Reopen |
| Imported | Mark remediated |
| Remediated | Reopen |
| Ignored | Reopen or Suppress |
| Suppressed | Reopen |

Ignore closes only the current finding. Suppress creates a persistent rule for the detector and suppression key so future similar signals are stored as Suppressed. Current UI suppression is immediate and does not collect a reason, so the rule normally shows **No note**. Reopening a suppressed finding does not remove that persistent suppression rule; there is no suppression-delete control on this screen.

Finding actions do not show a confirmation dialog. Bulk **Start review** affects only visible, selected Open findings. The current UI does not link a finding to an existing vault record.

A completed file Run can automatically mark stale Open, In review, or Ready-to-import file findings as Remediated when evidence disappears from paths that were successfully scanned. Ignore, Suppress, and Imported are not automatically cleared by that pass.

## Import: Short-Lived Material Handoff

Only a narrow file finding can enter Import. It must be Ready to import, `FILE_EXPOSURE`, have a path hash and material locator, and be classified as Password, API key, Certificate, or Credential. Network surfaces, TLS findings, notes, and generic file evidence are signal-only.

Import candidates are drawn from loaded findings. Load older pages in Findings first when an expected candidate is absent.

For each import:

1. VaultPilot re-reads the approved source and revalidates path hash, detector, candidate type, evidence hash, and material fingerprint.
2. The plaintext value is returned only for a user-bound, five-minute import handoff.
3. The browser builds the record and encrypts it with the active vault key.
4. The server verifies the token, evidence, vault write access, and candidate type, then stores the encrypted item and marks the finding Imported.

If source material changed, moved, disappeared, or no longer matches the evidence, import stops and the finding must be reviewed again. The server does not persist the plaintext source value.

Selected imports run sequentially, not as one atomic transaction. If a later item fails, earlier successful imports remain. Import does not clean the source; **Mark remediated** changes only the finding workflow state.

## Audit Trail

Discovery writes audit events for policy save; Preview/Run start; run cancellation and log deletion; finding review, Ignore, and Suppress; import preparation/material read; generic vault `IMPORT`; import completion; and manual remediation. Deleting a job log does not delete its findings. Automatic stale-finding remediation occurs as part of a completed file Run and should not be described as a separate manual-remediation audit event for every row.

## Screen States

| State | Operator response |
| --- | --- |
| Discovery loading | Wait for the skeleton; do not create a second policy from an unknown state. |
| Discovery data unavailable | Check session, Discovery capability, and server connection; preserve the sanitized error. |
| Read-only role or license | Review only. Owner plus a writable Discovery license is required for every action. |
| Scope rejected | Do not widen or work around it; correct the private IPv4 scope or remove the network scope for file-only scanning. |
| Policy Disabled | Do not rely on Preview appearing available; create an enabled policy when a run is required. |
| Run active | Follow persisted progress; the same policy cannot start another job. |
| Cancellation requested | Wait for runner acknowledgement; do not assume scanning stopped immediately. |
| Run Failed | Open job detail, preserve redacted error evidence, correct the approved policy, and restart deliberately. |
| No findings | Check whether a real Run—not Preview—completed and whether the selected checks had valid scope. |
| No findings match | Reset filters; the default view itself hides non-Open and non-High findings. |
| Import queue empty | Review eligible file findings, load older pages if needed, and mark confirmed material Ready to import. |
| Import locked | Unlock a writable active vault where the Owner is Editor or Manager. |
| Import evidence changed | Stop and re-review the source; never bypass hash or fingerprint validation. |

## Before You Act

- Obtain explicit authorization for every private target, UNC share, drive path, and preset-expanded profile area.
- Confirm the VaultPilot server account has only the intended read access; presets do not grant filesystem permission.
- Choose the smallest target, port, path, extension, size, timeout, and concurrency scope that answers the question.
- Treat Preview as a recorded plan only; use Run when actual evidence is required.
- Remember that HTTP checks generate GET traffic and file checks transiently read source content.
- Review status, confidence, detector, masked path, reason codes, and ownership before Ignore, Suppress, or Import.
- Before import, confirm the active vault, write role, record owner, destination category, and source-remediation plan.

## Safe Evidence

- Safe to share: general scan kind, policy/job state, approximate target/file/finding counts, severity, confidence, candidate type, detector ID, broad time window, sanitized error category, and a deliberately redacted path or host shape.
- Keep private: real IP/CIDR/port inventory, hostnames, UNC or local paths, usernames, full asset identity, suppression key, exact timestamp, raw or correlatable preview, full source file, source value, private key/certificate material, import token, vault name, database/backup/export, and imported record content.
- Evidence and path hashes can still correlate systems across reports. Share compact or fully masked values unless exact comparison is required in private support.
- Never attach a source file or recreate the discovered plaintext in a ticket. Use the redacted finding metadata and a private support channel.

## When to Stop and Escalate

Stop when scope ownership is unclear, a public or unexpected target appears, presets resolve outside the approved area, file access is broader than intended, a run remains active without progress, cancellation is not acknowledged, findings expose more context than expected, suppression hides an unexplained class of signals, material changes during import, sequential import partially succeeds, or a remediated/revoked decision conflicts with audit evidence. Open a private support case with role, general state, scan kind, broad time window, compact hashes, sanitized error, and last safe step—without real scope or secret material.

## Operator Notes

Discovery is evidence collection and review, not proof of compromise and not proof of absence. A clean result covers only the selected checks, accepted scope, readable files, supported formats, limits, and time of that Run. Marking a finding Remediated does not modify the source. Suppression is persistent and should be used only when future matching signals are intentionally hidden.

## Related

- [Discovery guide](discovery.md)
- [Discovery finding review KB](../../kb/en/discovery-finding-review.md)
- [Public issue redaction KB](../../kb/en/public-issue-redaction.md)
- [Audit Log screen](screen-audit-log.md)
