# &#128274; VaultPilot Enterprise Vault Console - README d'entrée français

<p align="center">
  &#127760; <strong>Documentation:</strong>
  <a href="README.de.md"><img src="https://flagcdn.com/w20/de.png" alt="Deutsch" width="20"></a> |
  <a href="README.es.md"><img src="https://flagcdn.com/w20/es.png" alt="Espa&#241;ol" width="20"></a> |
  <a href="README.md"><img src="https://flagcdn.com/w20/gb.png" alt="English" width="20"></a> |
  <a href="README.pt-BR.md"><img src="https://flagcdn.com/w20/br.png" alt="Portugu&#234;s (Brasil)" width="20"></a> |
  <a href="README.tr.md"><img src="https://flagcdn.com/w20/tr.png" alt="T&#252;rk&#231;e" width="20"></a> |
  <a href="README.fr.md"><img src="https://flagcdn.com/w20/fr.png" alt="Fran&#231;ais" width="20"></a>
</p>

> Ce fichier est une page d’entrée française, pas un court résumé. Il couvre objectif, limites, usage, validation, sécurité et publication.
>
> README canonique en anglais: [README.md](README.md)

Centre public de documentation et de releases pour VaultPilot password and secrets manager.

Commencez par le README canonique si vous voulez la description anglaise la plus actuelle. Utilisez cette page pour lire le même contrat opérationnel en français.

## Statut et signaux de confiance

|Zone | Détail|
|--- | ---|
|Statut | Dépôt public: ucsahinn/vaultpilot|
|Release publique actuelle | VaultPilot 2.0.0 a été publié le 30 juin 2026 sous GitHub Release `v2.0.0`.|
|Compatibilité | Le nom PassMan reste conservé pour les anciens services, chemins de données, variables d'environnement, cookies, headers, chaînes de protocole, alias d'update et décisions de rollback.|
|Source de vérité | [README canonique en anglais](README.md)|
|Utilisateurs | Opérateurs enterprise qui installent ou vérifient VaultPilot; admins qui contrôlent les flux update, backup, AD et extension navigateur.|
|Validation | Les index de documentation anglais et turcs restent accessibles; les screenshots et assets visuels référencés par README existent.|
|Sécurité | Documente le contrat opérationnel enterprise et le chemin de confiance des releases; fournit les arbres documentaires anglais/turcs et les articles KB.|

## Ce que contient ce dépôt

- Hub public de documentation pour VaultPilot Enterprise Vault Console.
- Passerelle de release et de vérification pour les utilisateurs qui contrôlent les assets publics.
- Carte documentaire pour admin quickstart, installation Windows Server, agent AD, backups, extension navigateur, partage, update center et troubleshooting.
- Surface publique sûre pour expliquer le produit sans exposer source privé ni données de vault client.
- Oriente les assets VaultPilot actuels vers GitHub Releases et ne présente pas les anciens builds PassMan comme chemin de nouvelle installation.

## Ce que ce dépôt n’est pas

- Ce n'est pas le dépôt source privé de l'application.
- Ce n'est pas un vault, un credential store ou un tenant client.
- Ce n'est pas un emplacement pour signing keys, secrets de licence, update keys ou bundles support privés.
- Cela ne remplace pas la validation des assets de release téléchargés.

## Public visé

- Opérateurs enterprise qui installent ou vérifient VaultPilot.
- Admins qui contrôlent les flux update, backup, AD et extension navigateur.
- Revues sécurité qui vérifient le trust model et la validation de release.
- Utilisateurs support qui cherchent troubleshooting public et guide evidence pack.

## Démarrage rapide

1. Clonez ou mettez à jour le dépôt.
2. Lisez README, sécurité et carte documentaire.
3. Lancez les validations adaptées.
4. Stagez uniquement les fichiers explicitement modifiés.
5. Avant push ou release, revérifiez remote, secrets et liens.

## Guide de décision

- Besoin d'overview -> docs/en/overview.md ou docs/tr/overview.md.
- Besoin d'installation -> docs/en/install-windows-server.md ou docs/tr/install-windows-server.md.
- Besoin de vérification de release -> docs/en/release-asset-verification.md ou docs/tr/release-asset-verification.md.
- Besoin de troubleshooting -> docs/en/troubleshooting.md, docs/tr/troubleshooting.md ou articles KB.
- Besoin de posture sécurité publique -> docs/en/security-and-trust-model.md, docs/tr/security-and-trust-model.md et SECURITY.md.

## Carte du dépôt

|Chemin | Pourquoi c’est important|
|--- | ---|
|`docs/en/` et `docs/tr/` | documentation produit principale|
|`kb/en/` et `kb/tr/` | articles KB de troubleshooting|
|[assets/screenshots/](assets/screenshots/) | screenshots publics|
|[assets/visuals/](assets/visuals/) | diagrammes SVG publics|
|[RELEASES.md](RELEASES.md) | notes de release et d'assets|
|[PRIVACY.md](PRIVACY.md) | politique de confidentialité|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | validateur de documentation|
|[SECURITY.md](SECURITY.md) | politique de disclosure sécurité|

## Flux de travail

1. Mettez à jour les deux arbres de langue quand le contrat produit change.
2. Gardez les release notes et la vérification alignées avec les assets publics réels.
3. Validez les documents et liens avant commit.
4. Lancez un secret scan avant push.
5. Vérifiez remote HEAD et le rendu GitHub release/page après publication.

## Commandes et validation

Exécutez ces commandes seulement après avoir cloné le dépôt et compris ce qu’elles vérifient ou modifient.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Liste de vérification

- Les index documentaires anglais et turcs sont accessibles.
- Les screenshots et assets visuels référencés par README existent.
- Aucune donnée vault privée, nom client, licence, signing key ou update secret n'apparaît.
- Le wording de vérification de release correspond à RELEASES.md.
- Remote HEAD est vérifié après push.

## Limite de sécurité

- Documente le contrat opérationnel enterprise et le chemin de confiance des releases.
- Fournit les arbres documentaires anglais et turcs plus les articles KB.
- Garde les release assets et l'update trust chain documentés.
- Inclut screenshots, assets visuels et scripts de validation pour docs publiques.

Règle public-safe: n'ajoutez pas secrets, tokens, cookies, private keys, prompts privés, données client, fichiers auth locaux, logs générés, archives ou build outputs sauf si le README canonique dit explicitement qu'ils appartiennent au repo public.

## Hygiène de release et publication

- Publiez les installateurs et archives via GitHub Releases, pas dans les commits source.
- Ne committez pas build output, packs support privés ou signing material.
- Mettez la documentation à jour avant d'annoncer un statut de release publique.
- Vérifiez noms d'assets, versions et remote HEAD après push/release.

## Maintenance

- Gardez ce README localisé aligné avec README.md quand le contrat du repo change.
- Préférez les liens factuels du repo aux claims marketing.
- N'inventez pas commandes d'installation, métriques, utilisateurs, releases ou promesses support.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Chemin de contribution

- Ouvrez une modification ciblée sur le plus petit ensemble de fichiers.
- Lisez AGENTS.md ou CONTRIBUTING.md avant d'éditer quand ils existent.
- Lancez les commandes de validation du repo listées ci-dessus.
- Relisez explicitement les staged diffs avant commit.
- Utilisez les chemins de security disclosure, pas les issues publiques, pour les rapports sensibles.

## Définition de terminé

Terminé signifie: contenu complet, liens corrects, limites de sécurité claires, validation exécutée, Git propre et remote HEAD vérifié après le push.

|Recommandation | Pourquoi c’est important|
|--- | ---|
|Contenu | Centre public de documentation et de releases pour VaultPilot password and secrets manager.|
|Liens | Tous les fichiers locaux référencés doivent exister et se résoudre depuis la racine du dépôt.|
|Sécurité | Aucune donnée vault privée, nom client, licence, signing key ou update secret ne doit apparaître.|
|Verification | Validez structure, liens, Markdown, secrets, scripts pertinents et remote HEAD avant toute annonce publique.|
|Remote | Après push, comparez local HEAD avec origin/main et GitHub remote HEAD.|

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
