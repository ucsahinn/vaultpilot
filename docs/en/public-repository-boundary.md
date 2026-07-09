# Public Repository Boundary

This repository is the public operator documentation and support surface for VaultPilot. It is not the product source tree, release-binary store, signing-material archive or customer evidence vault.

Use this page before opening issues, pull requests or documentation changes.

## What Belongs In Git

- Public documentation under `docs/`, `kb/`, localized READMEs and policy files.
- Public-safe screenshots that use synthetic tenant, host, user and vault data.
- Public validation scripts and GitHub workflow definitions that protect documentation hygiene.
- Release notes that describe already-published public GitHub Release assets.
- Link and wording fixes that keep the public operator path current.

## License Terms

This repository does not publish license terms unless a `LICENSE` or `LICENSE.md` file is added by the repository owner. Do not add, infer or promise documentation, asset, binary, or product-source license terms in issues, pull requests or release notes without owner approval.

## What Belongs In GitHub Releases

Release delivery artifacts belong on the signed GitHub Release page, not in the git tree:

- MSI installers.
- Browser extension ZIP archives.
- Offline share decrypter archives.
- DC Agent PowerShell scripts.
- Update manifests and component manifests.
- Checksums, signatures and release evidence that operators must compare against the published release.

The public docs may link to the release and list public asset names, sizes and SHA-256 values. Do not commit copies of those assets.

## What Must Stay Private

Never add these materials to issues, pull requests, comments or committed files:

- Plaintext vault records, passwords, master passwords, share passphrases or recovery phrases.
- API keys, agent tokens, session cookies, private keys, PFX/P12 files or signing material.
- AD bind passwords, Kerberos tickets, hashes, database files, backups or raw customer logs.
- Screenshots that reveal real users, tenants, hostnames, internal URLs, infrastructure addresses or secret records.
- Installer evidence bundles that contain unredacted local paths, customer names or support-ticket exports.

Use placeholders such as `<VAULTPILOT_URL>`, `<SERVER_HOST>`, `<AGENT_ID>`, `<AGENT_TOKEN>`, `<LICENSE_CODE>` and `<REDACTED>`.

## Public Issue Rule

Open public issues only when the full evidence set is safe to publish. If the issue needs unredacted logs, screenshots, database files, certificate material, license material or customer-specific operational data, use the private support channel instead.

Related: [Support policy](../../SUPPORT.md), [Security policy](../../SECURITY.md), [Contributing](../../CONTRIBUTING.md), [public issue redaction KB](../../kb/en/public-issue-redaction.md).
