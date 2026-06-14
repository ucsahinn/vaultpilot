# &#128274; PassMan Enterprise Vault Console - README completa em português do Brasil

[&#127468;&#127463; English](README.md) | [&#127465;&#127466; Deutsch](README.de.md) | [&#127466;&#127480; Español](README.es.md) | [&#127463;&#127479; Português (Brasil)](README.pt-BR.md) | [&#127481;&#127479; Türkçe](README.tr.md) | [&#127467;&#127479; Français](README.fr.md)

> Este arquivo é uma porta de entrada completa em português do Brasil, não um resumo curto. Ele cobre objetivo, limites, uso, validação, segurança e publicação.
>
> README canônico em inglês: [README.md](README.md)

Public documentation and release hub for the PassMan enterprise password manager.

Comece pelo README canônico quando precisar da descrição em inglês mais atual. Use esta página para ler o mesmo contrato operacional em português do Brasil.

## Estado e sinais de confiança

|Área | Detalhe|
|--- | ---|
|Status | Public repository: ucsahinn/passman|
|Fonte da verdade | [README canônico em inglês](README.md)|
|Usuários | Enterprise operators installing or reviewing PassMan.; Admins checking update, backup, AD and browser extension workflows.|
|Validação | English and Turkish doc indexes remain reachable.; Screenshots and visual assets referenced by README exist.|
|Segurança | Documents enterprise operating contract and release trust path.; Provides English and Turkish documentation trees plus knowledge base articles.|

## O que este repositório é

- A public documentation hub for PassMan Enterprise Vault Console.
- A release and verification gateway for users checking public assets.
- A documentation map for admin quickstart, Windows Server install, AD agent, backups, browser extension, sharing, update center and troubleshooting.
- A safe public surface for product explanation without exposing private source or customer vault data.

## O que ele não é

- Not the private application source repository.
- Not a vault, credential store or customer tenant.
- Not a place for signing keys, license secrets, update keys or private support bundles.
- Not a replacement for validating downloaded release assets.

## Para quem é

- Enterprise operators installing or reviewing PassMan.
- Admins checking update, backup, AD and browser extension workflows.
- Security reviewers checking trust model and release verification.
- Support users looking for public troubleshooting and evidence-pack guidance.

## Início rápido

1. Clone ou atualize o repositório.
2. Leia README, segurança e mapa de documentação.
3. Execute as validações adequadas.
4. Stage somente os arquivos alterados de forma explícita.
5. Antes de push ou release, revise remoto, segredos e links novamente.

## Guia de decisão

- Need overview -> docs/en/overview.md or docs/tr/overview.md.
- Need install -> docs/en/install-windows-server.md or docs/tr/install-windows-server.md.
- Need release verification -> docs/en/release-asset-verification.md.
- Need troubleshooting -> docs/en/troubleshooting.md or kb articles.
- Need public security posture -> docs/en/security-and-trust-model.md and SECURITY.md.

## Mapa do repositório

|Caminho | Por que importa|
|--- | ---|
|`docs/en/ and docs/tr/` | main product documentation|
|`kb/en/ and kb/tr/` | knowledge base troubleshooting articles|
|[assets/screenshots/](assets/screenshots/) | public screenshots|
|[assets/visuals/](assets/visuals/) | public SVG diagrams|
|[RELEASES.md](RELEASES.md) | release and asset notes|
|[PRIVACY.md](PRIVACY.md) | privacy policy|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | documentation validator|
|[SECURITY.md](SECURITY.md) | security disclosure policy|

## Fluxo de trabalho

1. Update docs in both language trees when the product contract changes.
2. Keep release notes and verification guidance aligned with actual public assets.
3. Validate docs and links before commit.
4. Run secret scan before push.
5. Verify remote HEAD and GitHub release/page rendering after publication.

## Comandos e validação

Execute estes comandos somente depois de clonar o repositório e entender o que eles verificam ou escrevem.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Lista de verificação

- English and Turkish doc indexes remain reachable.
- Screenshots and visual assets referenced by README exist.
- No private vault data, customer names, licenses, signing keys or update secrets appear.
- Release verification wording matches RELEASES.md.
- Remote HEAD is verified after push.

## Limite de segurança

- Documents enterprise operating contract and release trust path.
- Provides English and Turkish documentation trees plus knowledge base articles.
- Keeps release assets and update trust chain documented.
- Includes screenshots, visual assets and validation scripts for public docs.

Public-safe rule: do not add secrets, tokens, cookies, private keys, private prompts, customer data, local-only auth files, generated logs, archives or build outputs unless the canonical README explicitly says they belong in the public repo.

## Higiene de release e publicação

- Publish installers and archives through GitHub Releases, not source commits.
- Do not commit build output, private support packs or signing material.
- Update documentation before announcing public release status.
- Check release asset names, versions and remote HEAD after push/release.

## Manutenção

- Keep this localized README aligned with README.md when the repo contract changes.
- Prefer factual repo links over marketing claims.
- Do not invent install commands, metrics, users, releases or support promises.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Caminho de contribuição

- Open a focused change against the smallest set of files.
- Read AGENTS.md or CONTRIBUTING.md when present before editing.
- Run the repo validation commands listed above.
- Review staged diffs explicitly before commit.
- Use security disclosure paths instead of public issues for sensitive reports.

## Definição de concluído

Concluído significa: conteúdo completo, links corretos, limites de segurança claros, validação executada, Git limpo e remote HEAD verificado depois do push.

|Recomendação | Por que importa|
|--- | ---|
|Content | Public documentation and release hub for the PassMan enterprise password manager.|
|Links | All referenced local files must exist and resolve from the repository root.|
|Security | No private vault data, customer names, licenses, signing keys or update secrets appear.|
|Verification | Valide estrutura, links, Markdown, segredos, scripts relevantes e remote HEAD antes de afirmar que algo foi publicado.|
|Remote | After push, compare local HEAD with origin/main and GitHub remote HEAD.|

## Links importantes

|Caminho | Por que importa|
|--- | ---|
|[Canonical README](README.md) | README.md|
|[English docs](docs/en/README.md) | docs/en/README.md|
|[Turkish docs](docs/tr/README.md) | docs/tr/README.md|
|[English knowledge base](kb/en/README.md) | kb/en/README.md|
|[Turkish knowledge base](kb/tr/README.md) | kb/tr/README.md|
|[Release notes](RELEASES.md) | RELEASES.md|
|[Privacy](PRIVACY.md) | PRIVACY.md|
|[Security policy](SECURITY.md) | SECURITY.md|
