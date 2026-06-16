# &#128274; PassMan Enterprise Vault Console - vollständige deutsche README

[🇬🇧](README.md) | [🇩🇪](README.de.md) | [🇪🇸](README.es.md) | [🇧🇷](README.pt-BR.md) | [🇹🇷](README.tr.md) | [🇫🇷](README.fr.md)

> Diese Datei ist eine vollständige deutsche Einstiegseite, kein kurzer Platzhalter. Sie fasst Zweck, Grenzen, Bedienung, Prüfung, Sicherheit und Veröffentlichung in einer Datei zusammen.
>
> Kanonische englische README: [README.md](README.md)

Public documentation and release hub for the PassMan enterprise password manager.

Beginnen Sie mit der kanonischen README, wenn Sie die aktuellste englische Beschreibung brauchen. Verwenden Sie diese Seite, wenn Sie den gleichen Vertrag auf Deutsch lesen wollen.

## Status und Vertrauensrahmen

|Bereich | Details|
|--- | ---|
|Status | Public repository: ucsahinn/passman|
|Wahrheit | [Kanonische englische README](README.md)|
|Benutzer | Enterprise operators installing or reviewing PassMan.; Admins checking update, backup, AD and browser extension workflows.|
|Prüfung | English and Turkish doc indexes remain reachable.; Screenshots and visual assets referenced by README exist.|
|Sicherheit | Documents enterprise operating contract and release trust path.; Provides English and Turkish documentation trees plus knowledge base articles.|

## Was dieses Repository ist

- A public documentation hub for PassMan Enterprise Vault Console.
- A release and verification gateway for users checking public assets.
- A documentation map for admin quickstart, Windows Server install, AD agent, backups, browser extension, sharing, update center and troubleshooting.
- A safe public surface for product explanation without exposing private source or customer vault data.

## Was es nicht ist

- Not the private application source repository.
- Not a vault, credential store or customer tenant.
- Not a place for signing keys, license secrets, update keys or private support bundles.
- Not a replacement for validating downloaded release assets.

## Für wen es gedacht ist

- Enterprise operators installing or reviewing PassMan.
- Admins checking update, backup, AD and browser extension workflows.
- Security reviewers checking trust model and release verification.
- Support users looking for public troubleshooting and evidence-pack guidance.

## Schnellstart

1. Repository klonen oder aktualisieren.
2. README, Sicherheitsdateien und Dokumentationskarte lesen.
3. Die passenden Prüfungen ausführen.
4. Nur explizit geänderte Dateien stagen.
5. Vor Push oder Release Remote-Status, Secrets und Links erneut prüfen.

## Entscheidungshilfe

- Need overview -> docs/en/overview.md or docs/tr/overview.md.
- Need install -> docs/en/install-windows-server.md or docs/tr/install-windows-server.md.
- Need release verification -> docs/en/release-asset-verification.md.
- Need troubleshooting -> docs/en/troubleshooting.md or kb articles.
- Need public security posture -> docs/en/security-and-trust-model.md and SECURITY.md.

## Repository-Karte

|Pfad | Warum es wichtig ist|
|--- | ---|
|`docs/en/ and docs/tr/` | main product documentation|
|`kb/en/ and kb/tr/` | knowledge base troubleshooting articles|
|[assets/screenshots/](assets/screenshots/) | public screenshots|
|[assets/visuals/](assets/visuals/) | public SVG diagrams|
|[RELEASES.md](RELEASES.md) | release and asset notes|
|[PRIVACY.md](PRIVACY.md) | privacy policy|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | documentation validator|
|[SECURITY.md](SECURITY.md) | security disclosure policy|

## Arbeitsablauf

1. Update docs in both language trees when the product contract changes.
2. Keep release notes and verification guidance aligned with actual public assets.
3. Validate docs and links before commit.
4. Run secret scan before push.
5. Verify remote HEAD and GitHub release/page rendering after publication.

## Befehle und Prüfung

Führen Sie diese Befehle nur aus, wenn Sie das Repository lokal geclont haben und die Wirkung verstehen.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Validierungs-Checkliste

- English and Turkish doc indexes remain reachable.
- Screenshots and visual assets referenced by README exist.
- No private vault data, customer names, licenses, signing keys or update secrets appear.
- Release verification wording matches RELEASES.md.
- Remote HEAD is verified after push.

## Sicherheitsgrenze

- Documents enterprise operating contract and release trust path.
- Provides English and Turkish documentation trees plus knowledge base articles.
- Keeps release assets and update trust chain documented.
- Includes screenshots, visual assets and validation scripts for public docs.

Public-safe rule: do not add secrets, tokens, cookies, private keys, private prompts, customer data, local-only auth files, generated logs, archives or build outputs unless the canonical README explicitly says they belong in the public repo.

## Release- und Publikationshygiene

- Publish installers and archives through GitHub Releases, not source commits.
- Do not commit build output, private support packs or signing material.
- Update documentation before announcing public release status.
- Check release asset names, versions and remote HEAD after push/release.

## Wartung

- Keep this localized README aligned with README.md when the repo contract changes.
- Prefer factual repo links over marketing claims.
- Do not invent install commands, metrics, users, releases or support promises.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Beitragspfad

- Open a focused change against the smallest set of files.
- Read AGENTS.md or CONTRIBUTING.md when present before editing.
- Run the repo validation commands listed above.
- Review staged diffs explicitly before commit.
- Use security disclosure paths instead of public issues for sensitive reports.

## Definition von fertig

Fertig bedeutet: Inhalt ist lokal vollständig, Links funktionieren, Sicherheitsgrenzen sind klar, Validierung ist gelaufen, Git ist sauber und der Remote-Stand ist nach dem Push geprüft.

|Empfehlung | Warum es wichtig ist|
|--- | ---|
|Content | Public documentation and release hub for the PassMan enterprise password manager.|
|Links | All referenced local files must exist and resolve from the repository root.|
|Security | No private vault data, customer names, licenses, signing keys or update secrets appear.|
|Verification | Prüfen Sie Struktur, Links, Markdown, Secrets, relevante Skripte und Remote-HEAD, bevor Sie eine öffentliche Aussage machen.|
|Remote | After push, compare local HEAD with origin/main and GitHub remote HEAD.|

## Wichtige Links

|Pfad | Warum es wichtig ist|
|--- | ---|
|[Canonical README](README.md) | README.md|
|[English docs](docs/en/README.md) | docs/en/README.md|
|[Turkish docs](docs/tr/README.md) | docs/tr/README.md|
|[English knowledge base](kb/en/README.md) | kb/en/README.md|
|[Turkish knowledge base](kb/tr/README.md) | kb/tr/README.md|
|[Release notes](RELEASES.md) | RELEASES.md|
|[Privacy](PRIVACY.md) | PRIVACY.md|
|[Security policy](SECURITY.md) | SECURITY.md|
