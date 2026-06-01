# Troubleshooting

## MSI installation fails

Check:

- Is the MSI running as Administrator?
- Is the port already in use?
- Is there an installer log under `C:\ProgramData\PassMan\logs`?
- What is the Windows service state?

## Server does not open

1. Check `https://127.0.0.1:1903/api/profile` on the server.
2. Check the `PassManServer` service state.
3. Verify firewall and port routing.
4. Review server logs with sensitive values redacted.

## DC Agent cannot connect

- Test `<PASSMAN_URL>` from the agent machine.
- Use `-Status` to view config, service, and log state.
- Use a domain-qualified bind username.
- Do not write token or password values to logs.

## Extension pairing stays pending

- The pairing code may have expired.
- The wrong username may have been entered.
- The user may not have an unlocked vault.
- The device may still be waiting for approval in PassMan.

## Update stays around 76 percent

The MSI may be in the service restart phase. When the service returns, Update Center reconciles state from the target version, installer log, and running version. If it remains blocked, inspect verbose MSI logs.
