# Discovery Finding Review

Use this article when Discovery reports a secret exposure signal, import is disabled, or an operator is unsure whether a finding should become a vault record.

## Symptom

- Discovery shows a password, API key, certificate/key, credential, note, or file candidate.
- The finding looks real, but the evidence is masked.
- Import does not show the finding.
- Import is available, but the operator needs a safe decision path.

## First Checks

| Check | Expected result |
| --- | --- |
| Scope approval | The scan policy shows an approved private network, Windows folder preset, local path, or SMB path. |
| File approval | File scans show explicit read-only approval. |
| Finding status | Only findings marked ready for import appear in the import step. |
| Evidence quality | Strong signals should show detector id, candidate type, masked path, path hash, and redacted evidence. |
| Vault state | Import requires an unlocked vault because the browser encrypts the imported value. |
| Ownership | The source owner confirms the value should be moved into VaultPilot instead of remaining only in the source file. |

## Safe Resolution Path

1. Open the finding drawer.
2. Confirm the detector id, candidate type, severity, confidence, masked path, path hash, and evidence hash.
3. If it is noise, use Ignore or Suppress with a reason.
4. If it is real but should not be vaulted, record the operational decision outside public comments.
5. If it should become a vault item, mark it ready for import.
6. Unlock the target vault.
7. Use the import step to create the encrypted vault record.
8. Review audit events for scan, review, import preparation, and import completion.

## Safe Evidence To Send

- VaultPilot version and component version.
- Scan name and timestamp.
- Detector id, severity, confidence, candidate type, review status, path hash, and evidence hash.
- Redacted evidence shown by the drawer.
- Whether the vault was locked or unlocked during import.

## Do Not Send

- Source files that triggered the finding.
- Unmasked paths containing customer or infrastructure names.
- Plaintext secret values, tokens, private keys, connection strings, or vault exports.
- Database files, backups, PFX/P12 packages, or raw logs with secret values.

## Escalate When

- Import fails after the finding is ready and the vault is unlocked.
- The finding repeats after a justified suppression.
- The scanner reports a system path, VaultPilot data path, or legacy PassMan data path that should have been rejected.
- The audit trail does not show the review or import action.

Related: [Discovery guide](../../docs/en/discovery.md), [Security and trust model](../../docs/en/security-and-trust-model.md), [Support evidence pack](../../docs/en/support-evidence-pack.md).
