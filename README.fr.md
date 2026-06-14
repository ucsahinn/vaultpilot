# &#128274; PassMan Enterprise Vault Console - README français complet

[&#127468;&#127463; English](README.md) | [&#127465;&#127466; Deutsch](README.de.md) | [&#127466;&#127480; Español](README.es.md) | [&#127463;&#127479; Português (Brasil)](README.pt-BR.md) | [&#127481;&#127479; Türkçe](README.tr.md) | [&#127467;&#127479; Français](README.fr.md)

> Ce fichier est une page d’entrée française complète, pas un court résumé. Il couvre objectif, limites, usage, validation, sécurité et publication.
>
> README canonique en anglais: [README.md](README.md)

Public documentation and release hub for the PassMan enterprise password manager.

Commencez par le README canonique si vous voulez la description anglaise la plus actuelle. Utilisez cette page pour lire le même contrat opérationnel en français.

## Statut et signaux de confiance

|Zone | Détail|
|--- | ---|
|Statut | Public repository: ucsahinn/passman|
|Source de vérité | [README canonique en anglais](README.md)|
|Utilisateurs | Enterprise operators installing or reviewing PassMan.; Admins checking update, backup, AD and browser extension workflows.|
|Validation | English and Turkish doc indexes remain reachable.; Screenshots and visual assets referenced by README exist.|
|Sécurité | Documents enterprise operating contract and release trust path.; Provides English and Turkish documentation trees plus knowledge base articles.|

## Ce que contient ce dépôt

- A public documentation hub for PassMan Enterprise Vault Console.
- A release and verification gateway for users checking public assets.
- A documentation map for admin quickstart, Windows Server install, AD agent, backups, browser extension, sharing, update center and troubleshooting.
- A safe public surface for product explanation without exposing private source or customer vault data.

## Ce que ce dépôt n’est pas

- Not the private application source repository.
- Not a vault, credential store or customer tenant.
- Not a place for signing keys, license secrets, update keys or private support bundles.
- Not a replacement for validating downloaded release assets.

## Public visé

- Enterprise operators installing or reviewing PassMan.
- Admins checking update, backup, AD and browser extension workflows.
- Security reviewers checking trust model and release verification.
- Support users looking for public troubleshooting and evidence-pack guidance.

## Démarrage rapide

1. Clonez ou mettez à jour le dépôt.
2. Lisez README, sécurité et carte documentaire.
3. Lancez les validations adaptées.
4. Stagez uniquement les fichiers explicitement modifiés.
5. Avant push ou release, revérifiez remote, secrets et liens.

## Guide de décision

- Need overview -> docs/en/overview.md or docs/tr/overview.md.
- Need install -> docs/en/install-windows-server.md or docs/tr/install-windows-server.md.
- Need release verification -> docs/en/release-asset-verification.md.
- Need troubleshooting -> docs/en/troubleshooting.md or kb articles.
- Need public security posture -> docs/en/security-and-trust-model.md and SECURITY.md.

## Carte du dépôt

|Chemin | Pourquoi c’est important|
|--- | ---|
|`docs/en/ and docs/tr/` | main product documentation|
|`kb/en/ and kb/tr/` | knowledge base troubleshooting articles|
|[assets/screenshots/](assets/screenshots/) | public screenshots|
|[assets/visuals/](assets/visuals/) | public SVG diagrams|
|[RELEASES.md](RELEASES.md) | release and asset notes|
|[PRIVACY.md](PRIVACY.md) | privacy policy|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | documentation validator|
|[SECURITY.md](SECURITY.md) | security disclosure policy|

## Flux de travail

1. Update docs in both language trees when the product contract changes.
2. Keep release notes and verification guidance aligned with actual public assets.
3. Validate docs and links before commit.
4. Run secret scan before push.
5. Verify remote HEAD and GitHub release/page rendering after publication.

## Commandes et validation

Exécutez ces commandes seulement après avoir cloné le dépôt et compris ce qu’elles vérifient ou modifient.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Liste de vérification

- English and Turkish doc indexes remain reachable.
- Screenshots and visual assets referenced by README exist.
- No private vault data, customer names, licenses, signing keys or update secrets appear.
- Release verification wording matches RELEASES.md.
- Remote HEAD is verified after push.

## Limite de sécurité

- Documents enterprise operating contract and release trust path.
- Provides English and Turkish documentation trees plus knowledge base articles.
- Keeps release assets and update trust chain documented.
- Includes screenshots, visual assets and validation scripts for public docs.

Public-safe rule: do not add secrets, tokens, cookies, private keys, private prompts, customer data, local-only auth files, generated logs, archives or build outputs unless the canonical README explicitly says they belong in the public repo.

## Hygiène de release et publication

- Publish installers and archives through GitHub Releases, not source commits.
- Do not commit build output, private support packs or signing material.
- Update documentation before announcing public release status.
- Check release asset names, versions and remote HEAD after push/release.

## Maintenance

- Keep this localized README aligned with README.md when the repo contract changes.
- Prefer factual repo links over marketing claims.
- Do not invent install commands, metrics, users, releases or support promises.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Chemin de contribution

- Open a focused change against the smallest set of files.
- Read AGENTS.md or CONTRIBUTING.md when present before editing.
- Run the repo validation commands listed above.
- Review staged diffs explicitly before commit.
- Use security disclosure paths instead of public issues for sensitive reports.

## Définition de terminé

Terminé signifie: contenu complet, liens corrects, limites de sécurité claires, validation exécutée, Git propre et remote HEAD vérifié après le push.

|Recommandation | Pourquoi c’est important|
|--- | ---|
|Content | Public documentation and release hub for the PassMan enterprise password manager.|
|Links | All referenced local files must exist and resolve from the repository root.|
|Security | No private vault data, customer names, licenses, signing keys or update secrets appear.|
|Verification | Validez structure, liens, Markdown, secrets, scripts pertinents et remote HEAD avant toute annonce publique.|
|Remote | After push, compare local HEAD with origin/main and GitHub remote HEAD.|

## Liens importants

|Chemin | Pourquoi c’est important|
|--- | ---|
|[Canonical README](README.md) | README.md|
|[English docs](docs/en/README.md) | docs/en/README.md|
|[Turkish docs](docs/tr/README.md) | docs/tr/README.md|
|[English knowledge base](kb/en/README.md) | kb/en/README.md|
|[Turkish knowledge base](kb/tr/README.md) | kb/tr/README.md|
|[Release notes](RELEASES.md) | RELEASES.md|
|[Privacy](PRIVACY.md) | PRIVACY.md|
|[Security policy](SECURITY.md) | SECURITY.md|
