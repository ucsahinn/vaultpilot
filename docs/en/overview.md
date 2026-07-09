# VaultPilot Overview

VaultPilot Enterprise Vault Console is a self-hosted, zero-knowledge enterprise vault console installed on Windows Server with an MSI. Users access it from a browser through the server IP address or DNS name over HTTPS. First-run profile creation and vault unlock require browser Web Crypto; the installed server exposes managed self-signed HTTPS until a trusted PFX/P12 certificate is configured.

VaultPilot is the current product identity for the 2.0 line. PassMan remains a compatibility name for older services, data paths, update aliases, protocol strings, and historical release artifacts only.

## Principles

- The master password is not sent to the server.
- Vault keys are unlocked in browser-session RAM.
- Secret payloads are encrypted in the browser before persistence.
- The server stores ciphertext, wrapped keys, and metadata in local SQLite.
- Update packages are verified with a signed manifest and SHA-256 hashes.

## Components

| Component | Purpose |
| --- | --- |
| VaultPilot Server | Main Windows service and browser application. |
| Chromium Extension | Autofill, save/update login prompts, and active-site badge counts. |
| Offline Share Decrypter | Opens external share packages fully in the browser. |
| VaultPilot DC Agent Service | Synchronizes Active Directory metadata into VaultPilot. |

## Start Here

- [Windows Server installation](install-windows-server.md)
- [First run, owner and license](first-run-owner-license.md)
- [Public host, HTTPS and certificates](public-host-https-certificate.md)
- [Server System settings](server-system.md)
- [Update Center](update-center.md)
- [Troubleshooting](troubleshooting.md)

## In-App Documentation Button

VaultPilot 2.0 adds a topbar help button with a question-mark icon. It opens the GitHub documentation page that matches the current screen, and the target language follows the console language: English screens open `docs/en/...`, Turkish screens open `docs/tr/...`.
