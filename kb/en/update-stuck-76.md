# Update stays around 76 percent

The 76 percent stage usually means VaultPilot has verified the release manifest and MSI package, then entered the quiet Windows Installer phase. The server service may restart during this step, so the browser can temporarily lose contact even when the update is healthy.

## Triage

1. Open [Updates](../../docs/en/screen-updates.md) and leave the job detail visible before refreshing.
2. Wait for the expected service restart window to finish before retrying.
3. Reopen VaultPilot and check the running version from the UI or server status.
4. Review the update job detail for final state, MSI path, SHA-256 and signer status.
5. Inspect Windows Installer event log and verbose MSI log only if the job does not reconcile.
6. Confirm the latest release manifest still points to the expected MSI and SHA-256 hash.

## What To Check

| Evidence | Healthy signal | Problem signal |
| --- | --- | --- |
| Release manifest | Signature, version and package URL match the intended release. | Manifest changed unexpectedly or cannot be verified. |
| Package hash | SHA-256 matches the manifest. | Hash mismatch, missing package or partial download. |
| Signer | Signer thumbprint matches pinned manifest evidence. | Unknown signer or untrusted local-only signer. |
| Windows Installer | Service restart and install completion event appear. | Installer error, rollback or missing completion event. |
| Job state | Job reconciles after service restart. | Job remains stale after the server is reachable again. |

## Safe Evidence

- VaultPilot version before and after the update.
- Update job id placeholder, state, percentage and final error category.
- MSI filename, SHA-256 and signature status.
- Redacted Windows Installer event id and timestamp.
- Whether the service restarted and came back online.

## Do Not Do

Do not bypass manifest verification, replace the MSI manually, alter signer trust, edit the database job row, or publish raw logs that include local paths, user names or secrets.

Related: [Updates screen](../../docs/en/screen-updates.md), [Update Center](../../docs/en/update-center.md), [Release asset verification](../../docs/en/release-asset-verification.md), [Publication runbook](../../docs/en/publication-runbook.md).
