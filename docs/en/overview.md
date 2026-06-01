# PassMan Overview

PassMan Enterprise Vault Console is a self-hosted, zero-knowledge enterprise vault console installed on Windows Server with an MSI. Users access it from a browser through the server IP address or DNS name. First-run profile creation and vault unlock require HTTPS or `localhost` so the browser exposes Web Crypto; plain HTTP server-IP access is only a reachability check until HTTPS is configured.

## Principles

- The master password is not sent to the server.
- Vault keys are unlocked in browser-session RAM.
- Secret payloads are encrypted in the browser before persistence.
- The server stores ciphertext, wrapped keys, and metadata in local SQLite.
- Update packages are verified with a signed manifest and SHA-256 hashes.

## Components

| Component | Purpose |
| --- | --- |
| PassMan Server | Main Windows service and browser application. |
| Chromium Extension | Autofill, save/update login prompts, and active-site badge counts. |
| Offline Share Decrypter | Opens external share packages fully in the browser. |
| PassMan DC Agent Service | Synchronizes Active Directory objects into PassMan. |

## Start Here

- [Windows Server installation](install-windows-server.md)
- [First run, owner and license](first-run-owner-license.md)
- [Public host, HTTPS and certificates](public-host-https-certificate.md)
- [Update Center](update-center.md)
- [Troubleshooting](troubleshooting.md)
