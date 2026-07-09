# HTTPS certificate warning

Use this when users see a browser warning after HTTPS is enabled.

## Checks

1. Confirm users open the same host name that exists in the certificate SAN.
2. Confirm the PFX/P12 package is readable by the VaultPilot service.
3. Confirm the configured port is open.
4. Confirm the certificate has not expired.
5. Avoid publishing private certificate material in docs, logs or tickets.

## Upload Errors

Certificate upload is Owner-only. Use exactly one `.pfx` or `.p12` package, larger than 0 bytes and no larger than 2 MB. Upload attempts are rate-limited to 6 attempts per 10 minutes. Never attach the package, password or private key material to a public ticket.

| Code | Meaning | Next check |
| --- | --- | --- |
| `UNSUPPORTED_CERTIFICATE_FILE` | The uploaded file is not `.pfx` or `.p12`. | Export the certificate and private key as a PFX/P12 package. |
| `CERTIFICATE_FILE_SIZE` | The package is empty or larger than 2 MB. | Confirm the exported package size and retry. |
| `CONTENT_LENGTH_REQUIRED` | The upload request did not include `Content-Length`. | Retry through the UI or use a client that sends the header. |
| `PAYLOAD_TOO_LARGE` | The multipart upload is over the server limit. | Upload one certificate package and keep it at or below 2 MB. |
| Rate limit response | Too many upload attempts in the current 10-minute window. | Wait before retrying; repeated failures usually mean wrong file type, empty package, oversized package or wrong upload client. |

## Recommended support data

- Public host name.
- Port.
- Certificate subject/SAN summary.
- Expiration date.
- Browser error code.

## Related

- [Public host and HTTPS](../../docs/en/public-host-https-certificate.md)
- [Server settings screen](../../docs/en/screen-server-settings.md)
- [Server System settings](../../docs/en/server-system.md)
- [Public screenshot redaction](public-screenshot-redaction.md)
