# Certificates Screen

The topbar `?` opens this page from the Certificates screen. Use it for certificate records stored in the vault, separate from the server HTTPS package configured in Server settings.

## Work Here

- Record subject, issuer, SAN summary, expiry and owner.
- Keep package passwords and private key material encrypted, never in titles or public notes.
- Use expiry filters to plan renewal before browser or service warnings begin.

## Screen States

| State | Operator response |
| --- | --- |
| Valid | Confirm owner, expiry and system association are present. |
| Expiring | Schedule renewal before uploading replacement material. |
| Upload issue | Validate file type, size and passphrase privately before retrying. |

## Before You Act

- Confirm whether the certificate record is inventory-only or tied to an installed server package.
- Verify owner, expiry and host coverage before uploading or replacing metadata.
- Keep private-key handling outside public support; document only redacted fingerprints or expiry windows.

## Safe Evidence

- Safe to share: certificate record type, expiry window, redacted fingerprint prefix and owner/review status.
- Keep private: private keys, package passwords, full SAN lists, customer hostnames, imported certificate files and unredacted screenshots.
- Treat any exposed private key or package passphrase as compromised until private review confirms the response.

## Operator Notes

Do not confuse vault certificate records with the server's public HTTPS certificate upload. Production HTTPS replacement belongs in Server settings.

## Related

- [Certificate dashboard screen](screen-certificate-dashboard.md)
- [Server settings screen](screen-server-settings.md)
- [Public host and HTTPS](public-host-https-certificate.md)
