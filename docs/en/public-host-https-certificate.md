# Public Host, HTTPS and Certificates

VaultPilot public browser access uses HTTPS on the configured public port. The installed server can create a managed self-signed HTTPS certificate for first access; operators should replace it with a trusted PFX/P12 package before broad production use. Plain HTTP is only an internal upstream or local development concern, not the public operator entry path.

## What Operators Configure

| Field | Required | Purpose |
| --- | --- | --- |
| Public host | Yes | DNS name or server host users open in the browser. |
| Public port | Yes | Default public HTTPS port is `1903`; use your approved inbound port. |
| HTTPS certificate package | Recommended for production | PFX/P12 package containing the certificate and private key. VaultPilot can start with a managed self-signed certificate until this is configured. |
| Certificate password | Required when the package is protected | Used by the server to load the package. |

VaultPilot does not need a separate "certificate source" selector. The operator chooses the certificate file directly.

## Supported Certificate Package

Use one certificate package:

```text
PFX / P12
```

The certificate must match the host users open in the browser. The subject or SAN should contain the configured host name.

## Upload Boundary And Errors

Certificate upload is an Owner-only server setting. Upload exactly one `.pfx` or `.p12` package. The file must be larger than 0 bytes and no larger than 2 MB. Upload attempts are rate-limited to 6 attempts per 10 minutes.

Browser uploads must include `Content-Length`; if a scripted client receives `CONTENT_LENGTH_REQUIRED`, retry through the UI or send the correct length header. If the upload exceeds the accepted envelope, VaultPilot returns `PAYLOAD_TOO_LARGE`.

| API code | Meaning | Operator action |
| --- | --- | --- |
| `UNSUPPORTED_CERTIFICATE_FILE` | The selected file is not a `.pfx` or `.p12` package. | Export a PFX/P12 package that contains the certificate and private key, then upload that package. |
| `CERTIFICATE_FILE_SIZE` | The selected package is empty or larger than 2 MB. | Re-export the certificate package and confirm its size before uploading. |
| `CONTENT_LENGTH_REQUIRED` | The upload request omitted `Content-Length`. | Use the VaultPilot UI or a client that sends the header. |
| `PAYLOAD_TOO_LARGE` | The multipart request exceeds the server upload limit. | Confirm the package is at most 2 MB and retry with exactly one certificate file. |

Never post the certificate package, certificate password, private key material or private host details in public issues, docs or screenshots.

## Production Checklist

1. Confirm first access at `https://<SERVER_HOST>:1903` or your configured public HTTPS port.
2. Expect a browser warning while the managed self-signed certificate is still in use.
3. Create or obtain the trusted certificate package outside VaultPilot.
4. Confirm the host name resolves to the VaultPilot server.
5. Open Server System and set the public host and port.
6. Upload the PFX/P12 package.
7. Enter the package password if required.
8. Save the HTTPS configuration.
9. Restart or let VaultPilot reload the service when the UI requests it.
10. Open:

```text
https://<HOST>:<PORT>
```

## Security Notes

- Never upload PFX/P12 files, private keys or certificate passwords to this public repository.
- Store certificate packages on the server with restricted ACLs.
- Replace expired certificates before browser warnings appear.
- Use internal PKI for private networks or a trusted public certificate for internet-facing DNS names.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Browser hostname warning | Certificate SAN does not match `<HOST>`. |
| HTTPS does not start | PFX/P12 password is wrong or the package is not readable. |
| Warning appears on first access | Managed self-signed HTTPS is still active; install a trusted PFX/P12 package or trust the issuing CA according to internal policy. |
| Works locally, not remotely | DNS, firewall or reverse proxy path is not aligned with the configured host/port. |
| Certificate accepted on server only | Client devices do not trust the issuing CA. |
