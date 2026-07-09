# Certificate Dashboard Screen

The topbar `?` opens this page from the Certificate dashboard. Use it to review certificate age, expiry windows, trusted-host alignment and stored certificate records.

## Work Here

- Prioritize expired, expiring and hostname-mismatch certificates.
- Confirm whether a warning belongs to browser HTTPS access, a stored certificate record or a Discovery finding.
- Replace production HTTPS packages through Server settings, not through public documentation or issue attachments.

## Screen States

| State | Operator response |
| --- | --- |
| Current | Confirm owner and renewal window are still documented. |
| Expiring | Assign a renewal owner before uploading or replacing material. |
| Invalid | Move to private support if the package, passphrase or trust chain is unclear. |

## Before You Act

- Confirm whether the certificate is used for browser access, stored inventory or both.
- Check expiry, issuer, host binding and renewal owner before uploading a replacement.
- Keep PFX/P12 handling inside the approved server workflow; public docs should reference only redacted metadata.

## Safe Evidence

- Safe to share: certificate status, expiry window, issuer family, redacted subject/SAN summary and renewal owner state.
- Keep private: `.pfx` and `.p12` files, private keys, passphrases, full certificate chains and host-specific package screenshots.
- Use private support when trust-chain, passphrase or production HTTPS replacement evidence cannot be fully redacted.

## Operator Notes

Never attach `.pfx`, `.p12`, private keys or certificate passwords to support evidence. Share only redacted subject/SAN summaries and expiry dates.

## Related

- [Public host and HTTPS](public-host-https-certificate.md)
- [Certificates screen](screen-certificates.md)
- [HTTPS certificate warning KB](../../kb/en/certificate-warning.md)
