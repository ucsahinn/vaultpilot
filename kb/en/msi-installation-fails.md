# MSI installation fails

Use this checklist when the VaultPilot MSI does not complete or the service does not start after install.

## Checks

1. Confirm the MSI was launched as Administrator.
2. Confirm the configured port is not already in use.
3. Check the `VaultPilotServer` Windows service state; upgraded hosts may still expose `PassManServer` as a legacy alias.
4. Review installer logs under `C:\ProgramData\VaultPilot\logs`; upgraded hosts may still have legacy `C:\ProgramData\PassMan\logs` evidence.
5. Re-run only after the previous service state is understood.

## Safe data for support

- VaultPilot version, plus the legacy PassMan version only for upgraded installs.
- Windows version.
- MSI file name and signature status.
- Redacted installer log excerpt.
- Port number and service state.

Do not send database files, master passwords, secret values, license private keys, certificates or screenshots showing secrets.

## Related

- [Windows Server installation](../../docs/en/install-windows-server.md)
- [Admin quickstart](../../docs/en/admin-quickstart.md)
- [Troubleshooting](../../docs/en/troubleshooting.md)
- [Support evidence pack](../../docs/en/support-evidence-pack.md)
