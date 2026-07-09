# VaultPilot Discovery

VaultPilot Discovery is a controlled exposure-review workspace for approved operators. It helps teams find login surfaces, certificate risks, and files that look like they contain secrets outside the encrypted vault.

Discovery is not PAM, asset inventory, RDP or SSH management, vulnerability scanning, malware scanning, or data cleanup automation. It is a read-only signal and review workflow that keeps the operator in control.

![VaultPilot Discovery run scope](../../assets/screenshots/discovery-run.png)

Screenshot note: Discovery screenshots are sanitized UI captures from an isolated VaultPilot runtime with synthetic data only. Visible paths, values, evidence hashes and finding states are documentation fixtures, and finding evidence is masked.

## What Discovery Reviews

| Area | What VaultPilot checks | Operator boundary |
| --- | --- | --- |
| Private network and TLS | Approved private IP, CIDR, range, TCP, TLS, and passive HTTP login markers. | No public internet scan by default. No credential submission. |
| Windows folder presets | Desktop, Documents, Downloads, OneDrive, Public desktop, and Public documents for the server runtime account. | Presets prepare scope, but the operator must still confirm read-only file scanning. |
| Approved local or SMB paths | Explicit paths that the operator is authorized to review. | System directories and VaultPilot or legacy PassMan data paths are rejected. |
| Documents and admin files | Text, Office, CSV/TSV, Excel OOXML, env/config, scripts, registry exports, VPN/RDP, Terraform, kubeconfig, Docker config, package-manager credential files, certificates, and key-like files. | Findings store metadata, hashes, and redacted evidence, not plaintext secret values. |

## What It Never Does

- It does not brute force, spray passwords, test default credentials, bypass access controls, or submit login forms.
- It does not read LSASS, SAM, NTDS, browser password stores, Windows Credential Manager, or DPAPI user secrets.
- It does not store raw passwords, API keys, tokens, private keys, connection strings, vault keys, cookies, HTTP bodies, Excel cell contents, or full matched lines.
- It does not modify, delete, quarantine, or clean source files.
- It does not import anything into a vault unless an operator marks a finding ready and the vault is unlocked.

## Operator Workflow

1. Open **Security > Discovery**.
2. Name the scan so the purpose is clear to a later reviewer.
3. Select a network/TLS scope, Windows folder presets, approved local paths, or approved SMB paths.
4. Confirm the read-only file-scan approval when file scope is selected.
5. Review file limits, extensions, timeout, concurrency, and ports before saving.
6. Use Preview for a safe dry-run policy event, or Run after the confirmation prompt.
7. Triage findings by status, signal strength, type, and asset.
8. Mark noise as ignored or suppressed with a reason.
9. Mark real file findings as ready for import only after the owner confirms they belong in the vault.
10. Import ready findings while the vault is unlocked. VaultPilot re-reads the approved value, returns it only for the short import handoff, and stores the encrypted vault record.

## Findings Review

![VaultPilot Discovery findings](../../assets/screenshots/discovery-findings.png)

Findings are signals, not secrets. A finding can show:

- detector id and candidate type,
- severity and confidence,
- asset identity or masked path,
- redacted evidence,
- path hash and evidence hash,
- review decision,
- whether the finding can become a vault record.

Use the detail drawer before any decision. If evidence is too weak, keep it in review or suppress it with a reason instead of importing it.

## Import Handoff

![VaultPilot Discovery import candidates](../../assets/screenshots/discovery-import.png)

Import is intentionally narrow:

- Only findings marked ready for import appear in the import step.
- The source value is re-read from the approved source during the import handoff.
- The browser encrypts the value with the unlocked vault key.
- The server stores the encrypted vault item, redacted finding metadata, and audit events.
- Plaintext discovered values are not persisted.

## Safe Evidence For Support

When asking for help, send only:

- scan name and run timestamp,
- selected scope type, not real secret-bearing paths unless redacted,
- detector id, severity, confidence, candidate type, status, and redacted evidence,
- path hash and evidence hash,
- whether the vault was locked or unlocked during import,
- relevant component version.

Do not send raw source files, screenshots with real secret records, unmasked paths, tokens, private keys, database files, backups, or vault exports.

## Related Pages

- [Security and trust model](security-and-trust-model.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Operator runbook](operator-runbook.md)
- [Knowledge base: Discovery finding review](../../kb/en/discovery-finding-review.md)
