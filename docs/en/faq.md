# FAQ

## Is VaultPilot a cloud service?

No. VaultPilot is a self-hosted Windows Server application.

## Is the master password sent to the server?

No. The master password is used in the browser; the plaintext master password is not sent to the server.

## Does this public repo contain source code?

No. The git tree contains documentation, release notes, knowledge-base articles, public policies, and sanitized visual assets. Customer delivery files are attached to GitHub Releases or distributed through Chrome Web Store; source code remains in the private repository.

## Is a local signer safe?

For the VaultPilot-managed update chain, a local signer can be accepted when the signed manifest pins the MSI signer thumbprint. CA-backed or trusted signing is recommended for Windows SmartScreen reputation.

## Can files be shared?

Yes. Selected file records can be included in external share packages. Expiry and maximum usage should be configured.

## Related

- [Admin quickstart](admin-quickstart.md)
- [First run, owner and license](first-run-owner-license.md)
- [Security and trust model](security-and-trust-model.md)
- [Support evidence pack](support-evidence-pack.md)
