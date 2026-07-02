# &#128274; VaultPilot Enterprise Vault Console - deutsche README-Einstiegseite

<p align="center">
  &#127760; <strong>Dokumentation:</strong>
  <a href="README.de.md"><img src="https://flagcdn.com/w20/de.png" alt="Deutsch" width="20"></a> |
  <a href="README.es.md"><img src="https://flagcdn.com/w20/es.png" alt="Espa&#241;ol" width="20"></a> |
  <a href="README.md"><img src="https://flagcdn.com/w20/gb.png" alt="English" width="20"></a> |
  <a href="README.pt-BR.md"><img src="https://flagcdn.com/w20/br.png" alt="Portugu&#234;s (Brasil)" width="20"></a> |
  <a href="README.tr.md"><img src="https://flagcdn.com/w20/tr.png" alt="T&#252;rk&#231;e" width="20"></a> |
  <a href="README.fr.md"><img src="https://flagcdn.com/w20/fr.png" alt="Fran&#231;ais" width="20"></a>
</p>

> Diese Datei ist eine deutsche Einstiegseite, kein kurzer Platzhalter. Sie fasst Zweck, Grenzen, Bedienung, Prüfung, Sicherheit und Veröffentlichung in einer Datei zusammen.
>
> Kanonische englische README: [README.md](README.md)

Öffentliche Dokumentations- und Release-Zentrale für den VaultPilot Password and Secrets Manager.

Beginnen Sie mit der kanonischen README, wenn Sie die aktuellste englische Beschreibung brauchen. Verwenden Sie diese Seite, wenn Sie den gleichen Vertrag auf Deutsch lesen wollen.

## Status und Vertrauensrahmen

|Bereich | Details|
|--- | ---|
|Status | Öffentliches Repository: ucsahinn/vaultpilot|
|Aktueller öffentlicher Release | VaultPilot 2.0.0 wurde am 30. Juni 2026 als GitHub Release `v2.0.0` veröffentlicht.|
|Kompatibilität | Der Name PassMan bleibt für alte Services, Datenpfade, Umgebungsvariablen, Cookies, Header, Protokoll-Strings, Update-Aliase und Rollback-Entscheidungen erhalten.|
|Wahrheit | [Kanonische englische README](README.md)|
|Benutzer | Enterprise-Operatoren, die VaultPilot installieren oder prüfen; Admins, die Update-, Backup-, AD- und Browser-Extension-Abläufe kontrollieren.|
|Prüfung | Englische und türkische Dokumentationsindizes bleiben erreichbar; die in der README referenzierten Screenshots und visuellen Assets existieren.|
|Sicherheit | Dokumentiert den Enterprise-Betriebsvertrag und den Release-Vertrauenspfad; stellt englische/türkische Dokumentationsbäume plus Knowledge-Base-Artikel bereit.|

## Was dieses Repository ist

- Öffentliche Dokumentationszentrale für VaultPilot Enterprise Vault Console.
- Release- und Prüfgateway für Benutzer, die öffentliche Assets kontrollieren.
- Dokumentationskarte für Admin-Quickstart, Windows-Server-Installation, AD-Agent, Backups, Browser-Erweiterung, Sharing, Update Center und Troubleshooting.
- Sichere öffentliche Produktoberfläche ohne private Quellen oder Kundenvault-Daten.
- Verweist für aktuelle VaultPilot-Release-Assets auf GitHub Releases und stellt alte PassMan-Builds nicht als neuen Installationspfad dar.

## Was es nicht ist

- Nicht das private Source-Repository der Anwendung.
- Kein Vault, Credential Store oder Kunden-Tenant.
- Kein Ort für Signing Keys, Lizenzgeheimnisse, Update Keys oder private Support-Bundles.
- Kein Ersatz für die Prüfung heruntergeladener Release-Assets.

## Für wen es gedacht ist

- Enterprise-Operatoren, die VaultPilot installieren oder prüfen.
- Admins, die Update-, Backup-, AD- und Browser-Extension-Abläufe kontrollieren.
- Security Reviewer, die Trust Model und Release-Prüfung kontrollieren.
- Support-Benutzer, die öffentliche Troubleshooting- und Evidence-Pack-Hinweise suchen.

## Schnellstart

1. Repository klonen oder aktualisieren.
2. README, Sicherheitsdateien und Dokumentationskarte lesen.
3. Die passenden Prüfungen ausführen.
4. Nur explizit geänderte Dateien stagen.
5. Vor Push oder Release Remote-Status, Secrets und Links erneut prüfen.

## Entscheidungshilfe

- Überblick nötig -> docs/en/overview.md oder docs/tr/overview.md.
- Installation nötig -> docs/en/install-windows-server.md oder docs/tr/install-windows-server.md.
- Release-Prüfung nötig -> docs/en/release-asset-verification.md oder docs/tr/release-asset-verification.md.
- Troubleshooting nötig -> docs/en/troubleshooting.md, docs/tr/troubleshooting.md oder KB-Artikel.
- Öffentliche Security Posture nötig -> docs/en/security-and-trust-model.md, docs/tr/security-and-trust-model.md und SECURITY.md.

## Repository-Karte

|Pfad | Warum es wichtig ist|
|--- | ---|
|`docs/en/` und `docs/tr/` | Hauptproduktdokumentation|
|`kb/en/` und `kb/tr/` | Knowledge-Base-Artikel für Troubleshooting|
|[assets/screenshots/](assets/screenshots/) | öffentliche Screenshots|
|[assets/visuals/](assets/visuals/) | öffentliche SVG-Diagramme|
|[RELEASES.md](RELEASES.md) | Release- und Asset-Notizen|
|[PRIVACY.md](PRIVACY.md) | Datenschutzrichtlinie|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | Dokumentationsvalidator|
|[SECURITY.md](SECURITY.md) | Security-Disclosure-Richtlinie|

## Arbeitsablauf

1. Aktualisieren Sie beide Sprachbäume, wenn sich der Produktvertrag ändert.
2. Halten Sie Release Notes und Prüfanleitung mit den tatsächlichen öffentlichen Assets synchron.
3. Validieren Sie Dokumente und Links vor dem Commit.
4. Führen Sie vor dem Push einen Secret Scan aus.
5. Prüfen Sie nach der Veröffentlichung Remote HEAD sowie GitHub-Release/Page-Rendering.

## Befehle und Prüfung

Führen Sie diese Befehle nur aus, wenn Sie das Repository lokal geclont haben und die Wirkung verstehen.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Validierungs-Checkliste

- Englische und türkische Dokumentationsindizes sind erreichbar.
- Die in der README referenzierten Screenshots und visuellen Assets existieren.
- Keine privaten Vault-Daten, Kundennamen, Lizenzen, Signing Keys oder Update Secrets sind enthalten.
- Die Release-Prüfsprache stimmt mit RELEASES.md überein.
- Remote HEAD ist nach dem Push verifiziert.

## Sicherheitsgrenze

- Dokumentiert den Enterprise-Betriebsvertrag und den Release-Vertrauenspfad.
- Stellt englische und türkische Dokumentationsbäume plus KB-Artikel bereit.
- Hält Release-Assets und Update-Trust-Chain dokumentiert.
- Enthält Screenshots, visuelle Assets und Validierungsskripte für öffentliche Dokumente.

Public-safe-Regel: Fügen Sie keine Secrets, Tokens, Cookies, Private Keys, privaten Prompts, Kundendaten, lokalen Auth-Dateien, generierten Logs, Archiven oder Build Outputs hinzu, sofern die kanonische README sie nicht ausdrücklich als Teil des öffentlichen Repos nennt.

## Release- und Publikationshygiene

- Veröffentlichen Sie Installer und Archive über GitHub Releases, nicht über Source Commits.
- Committen Sie keine Build Outputs, privaten Support Packs oder Signing-Materialien.
- Aktualisieren Sie die Dokumentation, bevor ein öffentlicher Release-Status angekündigt wird.
- Prüfen Sie Asset-Namen, Versionen und Remote HEAD nach Push/Release.

## Wartung

- Halten Sie diese lokalisierte README mit README.md synchron, wenn sich der Repo-Vertrag ändert.
- Bevorzugen Sie faktische Repo-Links gegenüber Marketingaussagen.
- Erfinden Sie keine Installationsbefehle, Metriken, Benutzer, Releases oder Support-Zusagen.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Beitragspfad

- Öffnen Sie eine fokussierte Aenderung im kleinsten passenden Dateisatz.
- Lesen Sie vor Aenderungen AGENTS.md oder CONTRIBUTING.md, sofern vorhanden.
- Führen Sie die oben genannten Repo-Validierungen aus.
- Prüfen Sie staged diffs vor dem Commit ausdrücklich.
- Nutzen Sie für sensible Meldungen Security-Disclosure-Wege statt öffentlicher Issues.

## Definition von fertig

Fertig bedeutet: Inhalt ist lokal vollständig, Links funktionieren, Sicherheitsgrenzen sind klar, Validierung ist gelaufen, Git ist sauber und der Remote-Stand ist nach dem Push geprüft.

|Empfehlung | Warum es wichtig ist|
|--- | ---|
|Inhalt | Öffentliche Dokumentations- und Release-Zentrale für den VaultPilot Password and Secrets Manager.|
|Links | Alle referenzierten lokalen Dateien müssen existieren und vom Repository-Root aus auflösbar sein.|
|Sicherheit | Keine privaten Vault-Daten, Kundennamen, Lizenzen, Signing Keys oder Update Secrets dürfen erscheinen.|
|Verification | Prüfen Sie Struktur, Links, Markdown, Secrets, relevante Skripte und Remote-HEAD, bevor Sie eine öffentliche Aussage machen.|
|Remote | Vergleichen Sie nach dem Push local HEAD mit origin/main und GitHub remote HEAD.|

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
