# Public Screenshot Redaction

Use this article when a screenshot planned for a public issue, pull request, README, guide, KB article, Chrome Web Store listing, or social preview might contain sensitive information.

## First Checks

1. Open the image at full size, not only as a thumbnail.
2. Check every visible table row, drawer, modal, toast, browser bar, tab title, filename, terminal prompt, notification, and footer.
3. Look for real customer data, hostnames, user names, email addresses, secret titles, passwords, tokens, license values, hashes tied to private material, support ticket IDs, account names, databases, backups, certificates, private keys, local paths, and logs.
4. Confirm the data is synthetic and fits the public screenshot standards.

## If Sensitive Data Appears

Do not commit, stage, upload, or attach the screenshot publicly.

| Finding | Action |
| --- | --- |
| Real customer, host, user, email, internal URL, database, backup, or support ticket data | Replace the screenshot with a synthetic-data capture. Keep the unsafe image out of git and public issues. |
| Token, password, vault record, secret title, private key, certificate private material, or license private material | Stop public handling. Treat the value as compromised until a private owner reviews it and rotates or revokes it where applicable. |
| Browser account, dashboard, profile, notification, or local folder data | Re-capture with a clean documentation profile and cropped application frame. |
| Release asset hash, size, filename, or manifest value shown as a fixture | Caption it as fixture data or remove it. Published release verification must use the release asset verification guide. |

## Safe Evidence To Send

- Screenshot filename and the page where it would appear.
- Component and documentation version.
- Description of the screen, with sensitive values replaced by `<REDACTED>`.
- Whether the replacement image uses synthetic tenant, user, host, vault, and finding data.
- The validation command and exact validator message if validation failed.

## What Not To Send Publicly

- The unsafe screenshot.
- Crops that still reveal surrounding customer, account, or local operator context.
- Raw logs, databases, backups, certificate packages, vault exports, browser profile data, support exports, or account dashboard screenshots.
- Token, password, license, private key, cookie, session, recovery, or share passphrase values.

## Recovery Path

1. Delete the unsafe local candidate from the review set if it is not needed for private incident review.
2. Capture a replacement from an isolated documentation runtime with synthetic data.
3. Update the relevant guide, visual table, and screenshot manifest if the filename changes.
4. Run:

```powershell
npm run validate
git diff --check
gitleaks detect --no-git --redact --verbose --source .
```

If the unsafe image was already committed, stop and use private security handling before history cleanup. Do not try to hide a secret-like value by adding another commit.

Related: [Public screenshot standards](../../docs/en/public-screenshot-standards.md), [Public issue redaction](public-issue-redaction.md), [Public validation fails](public-validation-fails.md), [Support policy](../../SUPPORT.md).
