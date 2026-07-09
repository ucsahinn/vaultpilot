# Discovery Screen

The topbar `?` opens this page from the Discovery screen. Use it for approved network, TLS and file-exposure checks before importing confirmed findings into the vault.

## Work Here

- Run only approved scopes and paths.
- Review finding confidence before importing.
- Import only material that belongs in VaultPilot and has an owner.

## Screen States

| State | Operator response |
| --- | --- |
| Ready | Confirm scope approval before starting a run. |
| Findings present | Review confidence and owner before import. |
| Scope denied | Do not widen the scan; fix the approved scope or stop. |

## Before You Act

- Verify network ranges, file paths and TLS targets are explicitly approved for the run.
- Treat each finding as evidence to review, not as an automatic vault import.
- Import only items with a clear owner, destination vault and remediation purpose.

## Safe Evidence

- Safe to share: finding category, confidence level, redacted path or host shape and evidence hash.
- Keep private: raw files, unmasked paths, internal hostnames, plaintext snippets, tokens, private keys and database exports.
- Import only after ownership and destination vault are clear; public discussion should stay at finding-summary level.

## Operator Notes

Discovery evidence often contains internal hosts, filenames, certificate fingerprints or secret-like snippets. Redact before sharing outside private support.

## Related

- [Discovery guide](discovery.md)
- [Discovery finding review KB](../../kb/en/discovery-finding-review.md)
- [Public issue redaction KB](../../kb/en/public-issue-redaction.md)
