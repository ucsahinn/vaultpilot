# Updates Screen

The topbar `?` opens this page from the Updates screen. Use it to verify server, extension and support-component update state before running an update.

## Work Here

- Review manifest, package URL, SHA-256, signer and version before starting.
- Use live check when package evidence looks stale.
- Treat update failures as evidence-driven incidents, not as a reason to bypass verification.

## Screen States

| State | Operator response |
| --- | --- |
| Update available | Verify manifest, hash and signer before starting. |
| Installing | Expect a service restart window and watch the job detail. |
| Stuck | Use the 76 percent KB before replacing packages or retrying. |

## Before You Act

- Confirm release tag, manifest signature, SHA-256 and signer before starting installation.
- Review backup and maintenance-window readiness before allowing a service restart.
- Treat failed verification as a stop condition, not as a reason to bypass checks.

## Safe Evidence

- Safe to share: release tag, component name, job ID, hash match or mismatch and signer summary.
- Keep private: copied installer files, local download paths, private support bundles and machine-specific logs.
- Treat signature, hash or manifest verification failure as a stop condition until support reviews the evidence.

## Operator Notes

Release binaries, ZIP packages and manifests belong in GitHub Releases or approved extension channels, not committed into the public docs repository.

## Related

- [Update Center](update-center.md)
- [Release asset verification](release-asset-verification.md)
- [Update stuck near 76 percent KB](../../kb/en/update-stuck-76.md)
