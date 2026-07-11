# Updates Screen

The topbar `?` opens this guide for the Updates screen. This screen evaluates local or signed remote evidence for the VaultPilot server MSI, starts an eligible installation job, and tracks Windows Installer and service-restart progress. It does not create, tag, upload, sign, or publish a release.

## Access, Role, and License Boundary

The **auto-update** feature is a client/UI navigation gate for the Updates view. With it available, Owner, Admin, and Auditor system roles can view the screen and existing server status; the User role cannot access this system view. A read-only license does not expose the feature view, so normal navigation is blocked in that mode. Current status, jobs, check, and start routes do not independently enforce the `auto-update` feature flag; that implementation detail is not authorization to bypass the UI gate.

**Check live** requires Owner or Admin and accepts at most ten requests per ten minutes. Its route does not separately reject a read-only license. An `UPDATE_CHECK` audit event is written only after status returns successfully; a manifest fetch or parse exception returns no status and creates no such audit event. Do not bypass the normal feature gate by calling the route directly.

The authoritative server-side role for starting a server MSI installation is **Owner**. An Admin is not authorized to start the server installer even if a client button or generic message suggests otherwise. A read-only license also rejects installation start. Auditor is view-only and cannot run a remote check or installation.

## Work Here

- Review current server version, target version, the package/URL label shown by the card, size, SHA-256, and verification steps.
- Read **Verification steps** to understand why the package is **Current**, **Ready**, or **Action required**.
- Use **Check live** to fetch the configured remote update manifest and verify signature/package evidence again.
- When evidence is eligible, use **Install server MSI** as Owner.
- During installation, monitor percentage, last-record age, target version, steps, and the **Advanced technical log** summary.
- After installation, verify that the running version matches the target and the console reconnects.

There is no update-job cancellation control or general **Retry** action. A blocked job remains as evidence. After correcting the cause and re-verifying the package, choosing install again creates a new job rather than resuming the old one.

## Components and Release Surfaces

The only installation card rendered here is the **VaultPilot server** MSI lane. It shows **Artifact**, **Latest version**, **Package size**, and SHA-256 when available. **Artifact** is derived from the last segment of `packageUrl`, not the known `fileName`; without a URL it says **Package path pending** even when the backend knows the filename. Normal server status does not render a separate manifest-address row. **Download MSI** appears only when a package URL is exposed.

Customer browser-extension installation and update are owned by Chrome Web Store; this screen does not create a separate extension installation job. Offline Share Decrypter, DC Agent, and other components can appear in the bundled **Release notes**, but they do not have independent installation cards or jobs here.

The **Release notes** timeline is bundled into the current console build and groups versions, components, and notes. The topbar's latest GitHub release summary is a separate informational query. When GitHub data is unavailable, the ticker can fall back to the local application version and still say **released**; that fallback wording is not external publication evidence. A bundled note, ticker, latest-release summary, or **Check live** result alone does not prove that a release was created, published, or complete with every asset.

## Local Status and Live Check

The screen first reads local server status:

- Without an eligible staged MSI, the running version is **Current** and no installation starts.
- A newer, version-identifiable local MSI has its size and SHA-256 calculated and can become **Ready** when version intent is acceptable. This is local preflight only.
- A downgrade, unknown-version package, or same-version repair package is **Action required** for automatic install. Same-version repair belongs to the manual MSI Repair path.

**Check live** reads the configured HTTPS GitHub manifest from the server. A successful check means the signed manifest was verified and the server MSI's presence and eligibility were evaluated. If the verification key is missing or signature verification fails, remote package URLs remain hidden and download is blocked. A panel can note that a local package exists, but while remote status is `BLOCKED` the current screen does not render a separate local package card or download link.

When remote connectivity or the latest-release query fails, the screen does not create a release, alter the manifest, or treat a local package as remote evidence. The local package is evaluated separately through version/SHA preflight and Authenticode verification inside the installation job.

## Package and Signature Verification

Remote automatic installation follows this trust chain:

1. Verify the manifest's Ed25519 signature with the configured or bundled release public key.
2. Match the server asset to an allowed HTTPS URL, filename, version, and expected size from that signed manifest.
3. Download with a bounded size on the server and compare the computed SHA-256 to the complete manifest value.
4. Read MSI Authenticode evidence on Windows. If the manifest pins a signer SHA-1 thumbprint, the MSI signer must match it; without a pin, a remote MSI requires a valid Windows signature status.
5. Do not start the quiet Windows Installer step until those checks pass.

A locally staged MSI's card status preflights version intent, file presence/size, and computed SHA-256. This local `READY` evaluation does not verify a local manifest Ed25519 signature and does not yet check MSI Authenticode; Authenticode runs after the installation job starts. There is no production documentation or UI control for bypassing unsigned-installer checks. Local **Ready** means only that preflight passed, not that signature verification or installation completed.

The card displays only an initial fragment of SHA-256 as visible text; the complete value can be present in the element detail. Do not use the truncated fragment as proof of a full match.

## Package and Job States

### Package status

| State | Meaning |
| --- | --- |
| **Current** (`CURRENT`) | No eligible newer local or remote MSI is available for the running version. |
| **Ready** (`READY`) | Remote signed-manifest evidence or local version/SHA preflight is eligible. Local Authenticode verification still occurs during the job. |
| **Action required** (`ACTION_REQUIRED`) | Verification key, manifest, asset, version intent, or other package evidence is missing or unsuitable. Read the blocked step. |

### Update job status

| State | Meaning |
| --- | --- |
| `QUEUED` | Recognized for schema and stored-job compatibility; the current start path does not emit it. If encountered, it is treated as active. |
| `RUNNING` | Download, verification, MSI, or restart work is in progress. |
| `BLOCKED` | A security, package, Windows Installer, UAC, or reconnect step stopped progress. This flow has no separate `FAILED` job state. |
| `READY` | Recognized for schema compatibility; the current start path does not emit this job state, and it does not mean installation completed. |
| `COMPLETED` | The job completed with the running VaultPilot version satisfying the target version. |

The current start path writes a new job directly as `RUNNING`, `BLOCKED`, or `COMPLETED`. If the request fails before a job is stored, the screen says **The update action could not be started**; this is not a persisted `FAILED` job row. The server lists at most 12 update jobs, with active jobs first and then the most recently updated terminal jobs.

## Steps and Technical Log

Verification and job steps can be `DONE`, `RUNNING`, `PENDING`, or `BLOCKED`. Server MSI steps can cover:

- reading installed version and accepting the target version,
- selecting a local package or downloading the verified MSI on the server,
- verifying the downloaded SHA-256,
- validating and recording MSI Authenticode evidence,
- running quiet Windows Installer,
- restarting VaultPilotServer and waiting for the target version.

The card's **Verification steps** come from package status or the selected job. While work is active, **Advanced technical log** lists every job step with state, label, and optional detail. This is not the raw PowerShell, MSI, or Windows Event Log. Some installer details are sanitized to reduce local-path exposure, but inspect every line before sharing it.

## Installation, UAC, and Service Restart

Server installation invokes quiet `msiexec` with reboot prompts suppressed, then restarts VaultPilotServer through a separate helper. Browser connectivity can drop during that transition. When health and version signals return, the console attempts to reload on the target version.

If the installer helper needs administrator rights, the server can request Windows UAC elevation. That prompt appears in the Windows server session, not in the browser. If approval is not granted or the elevated helper cannot start, the job becomes **BLOCKED** around the MSI stage. Do not start installation without an authorized Windows administrator session and approved maintenance window.

Updates does not schedule a maintenance window, create a backup, or coordinate user sessions. Prepare an approved backup, brief service interruption, user communication, and rollback path in the operating procedure before starting.

## Blocked-State Recovery

Persisted jobs are read again after a page reload or service return. The server reconciles a stored `RUNNING` job against helper logs and the running version:

- If the target version is already active, the job can become `COMPLETED`.
- If MSI completed but the service has not returned on the target version, the restart step remains active and eventually becomes `BLOCKED` on timeout.
- Missing installer-helper startup evidence can block around `76%`.
- A helper that started but never reported MSI completion/exit can block around `82%`.
- MSI completion without target-version confirmation can block around `96%`.

An unchanged percentage for several minutes is not by itself proof of a stall. If **Last record** remains fresh, wait. After a page reload, a recovered active job can appear without restoring session-driven automatic polling. Refocus the window or refresh the browser page to fetch a newer job snapshot; **Check live** checks package eligibility and is not a job-refresh control. Before starting new work, confirm that neither Updates nor Executions shows an active job.

There is no cancel control. Do not edit the job database, replace a package without verification, or bypass signature checks. Preserve evidence, correct the cause, refresh with **Check live** or trusted local evidence, and only then start a new installation job.

## Recommended Workflows

### Verify and install a signed remote MSI

1. Prepare maintenance window, backup, rollback plan, and Windows administrator access.
2. Choose **Check live** and confirm manifest signature and package steps are not blocked.
3. Compare filename, target version, size, full SHA-256, and signer evidence with independent release evidence.
4. If the package is **Ready**, choose **Install server MSI** as Owner.
5. Monitor download, SHA-256, Authenticode, MSI, and restart steps.
6. After reconnect, verify running version, service health, and terminal job state.

### Investigate a blocked job

1. Identify the first blocked step and last-record time.
2. Separate manifest/signature/hash failures from Windows Installer/UAC/service failures.
3. Preserve redacted evidence before changing package or trust configuration.
4. When relevant, use the 76-percent KB and Windows Installer/VaultPilot service evidence.
5. Do not start another job until the cause is corrected; run a fresh check afterward.

## Screen States

| State | Operator response |
| --- | --- |
| Loading | Two skeleton rows appear; do not treat the temporary blank state as final package status. |
| Update status could not be read | Verify vault/session, role, auto-update license scope, and server connectivity. |
| Current | There is no new automatic MSI job; do not use bundled release notes as publication evidence. |
| Ready | Verify version, manifest, full SHA-256, signer, and maintenance window before Owner starts it. |
| Action required | Resolve the first `BLOCKED` verification step; do not force download or installation. |
| Check running | Do not start a second live check; wait for its result or warning. |
| Installing | Monitor **Last record** as well as percentage and expect a service disconnect. |
| Awaiting UAC | Evaluate the prompt in the Windows server session; do not accept an unexpected request. |
| Holding near 76/82 percent | Wait while fresh records arrive; if timeout or `BLOCKED` occurs, inspect the relevant helper evidence. |
| Holding near 96 percent | Compare MSI outcome with running server version; do not call it complete before target-version confirmation. |
| Blocked | Preserve the blocked step and redacted detail; no automatic retry is promised. |
| Completed | Treat it as complete only when running version and service health satisfy the target. |
| Console disconnected | During the approved window, wait for health recovery; after reconnect, refocus or refresh the page and do not immediately start a second install. |

## Before You Act

- Confirm Owner role, auto-update license feature, and a writable license.
- Prepare an approved maintenance window, current backup, rollback method, and Windows administrator access.
- Do not mix local and remote evidence; verify `LOCAL` or `GITHUB_RELEASE` source and target version.
- For remote packages, evaluate manifest signature, allowed package URL, filename/size, full SHA-256, and Authenticode signer together; for local `READY`, remember that Authenticode runs during the job.
- Check Updates and Executions for an existing `QUEUED` or `RUNNING` job.
- Remember that a live check, release note, or latest-release summary does not publish a release or prove installation success.

## Safe Evidence

- Safe to share: general source class, component, public version/tag, public package filename and size, expected/observed SHA-256 match state, Authenticode status or signer summary, step state, broad time window, and redacted error category.
- Keep private: local download/staging path, server host and username, job identifier, private manifest/support URL, copied MSI, raw PowerShell/MSI/Windows Event log, support bundle, environment values, license data, and signing private key/certificate file.
- The complete SHA-256 and signer thumbprint for a public release asset can be public evidence; do not publish internal package evidence until you confirm it belongs to that public asset.
- In screenshots, review and mask the package-URL-derived artifact text, technical step detail, and exact last-record time independently; do not assume the normal card exposes a manifest address.

## When to Stop and Escalate

Stop installation when the manifest signature cannot be verified, SHA-256 or size differs, Authenticode signer does not match trusted evidence, an unexpected UAC prompt appears, MSI rolls back, the service does not return on the target version, or the reconciled job remains `BLOCKED`. Before replacing a package or starting a new job, open a private support case with version, source class, step name, broad time window, general error code, and redacted signature/hash state.

## Operator Notes

Updates is a consumer-side verification and installation surface. It does not build, sign, upload, tag, or publish a GitHub release, manifest, MSI, or other component asset. Bundled release notes are not a live source of external publication state.

## Related

- [Update Center](update-center.md)
- [Release asset verification](release-asset-verification.md)
- [Executions screen](screen-executions.md)
- [Server settings screen](screen-server-settings.md)
- [Update stuck near 76 percent KB](../../kb/en/update-stuck-76.md)
