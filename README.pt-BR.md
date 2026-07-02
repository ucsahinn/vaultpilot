# &#128274; VaultPilot Enterprise Vault Console - README de entrada em português do Brasil

<p align="center">
  &#127760; <strong>Documenta&#231;&#227;o:</strong>
  <a href="README.de.md"><img src="https://flagcdn.com/w20/de.png" alt="Deutsch" width="20"></a> |
  <a href="README.es.md"><img src="https://flagcdn.com/w20/es.png" alt="Espa&#241;ol" width="20"></a> |
  <a href="README.md"><img src="https://flagcdn.com/w20/gb.png" alt="English" width="20"></a> |
  <a href="README.pt-BR.md"><img src="https://flagcdn.com/w20/br.png" alt="Portugu&#234;s (Brasil)" width="20"></a> |
  <a href="README.tr.md"><img src="https://flagcdn.com/w20/tr.png" alt="T&#252;rk&#231;e" width="20"></a> |
  <a href="README.fr.md"><img src="https://flagcdn.com/w20/fr.png" alt="Fran&#231;ais" width="20"></a>
</p>

> Este arquivo é uma porta de entrada em português do Brasil, não um resumo curto. Ele cobre objetivo, limites, uso, validação, segurança e publicação.
>
> README canônico em inglês: [README.md](README.md)

Central pública de documentação e releases para o VaultPilot password and secrets manager.

Comece pelo README canônico quando precisar da descrição em inglês mais atual. Use esta página para ler o mesmo contrato operacional em português do Brasil.

## Estado e sinais de confiança

|Área | Detalhe|
|--- | ---|
|Status | Repositório público: ucsahinn/vaultpilot|
|Release pública atual | VaultPilot 2.0.0 foi publicado em 30 de junho de 2026 como GitHub Release `v2.0.0`.|
|Compatibilidade | O nome PassMan continua preservado para serviços antigos, caminhos de dados, variáveis de ambiente, cookies, headers, strings de protocolo, aliases de update e decisões de rollback.|
|Fonte da verdade | [README canônico em inglês](README.md)|
|Usuários | Operadores enterprise que instalam ou revisam o VaultPilot; admins que validam fluxos de update, backup, AD e extensão de navegador.|
|Validação | Os índices de documentação em inglês e turco seguem acessíveis; screenshots e assets visuais referenciados pelo README existem.|
|Segurança | Documenta o contrato operacional enterprise e o caminho de confiança de releases; fornece árvores de documentação em inglês/turco e artigos KB.|

## O que este repositório é

- Hub público de documentação para o VaultPilot Enterprise Vault Console.
- Gateway de release e verificação para usuários que conferem assets públicos.
- Mapa de documentação para quickstart admin, instalação em Windows Server, AD agent, backups, extensão de navegador, sharing, update center e troubleshooting.
- Superfície pública segura para explicar o produto sem expor source privado ou dados de vault de clientes.
- Direciona os assets atuais do VaultPilot para GitHub Releases e não apresenta builds antigos do PassMan como novo caminho de instalação.

## O que ele não é

- Não é o repositório privado de source da aplicação.
- Não é vault, credential store ou tenant de cliente.
- Não é local para signing keys, segredos de licença, update keys ou bundles privados de suporte.
- Não substitui a validação de assets baixados de releases.

## Para quem é

- Operadores enterprise que instalam ou revisam o VaultPilot.
- Admins que validam fluxos de update, backup, AD e extensão de navegador.
- Revisores de segurança que conferem trust model e verificação de release.
- Usuários de suporte que procuram troubleshooting público e orientação de evidence pack.

## Início rápido

1. Clone ou atualize o repositório.
2. Leia README, segurança e mapa de documentação.
3. Execute as validações adequadas.
4. Stage somente os arquivos alterados de forma explícita.
5. Antes de push ou release, revise remoto, segredos e links novamente.

## Guia de decisão

- Precisa de overview -> docs/en/overview.md ou docs/tr/overview.md.
- Precisa de instalação -> docs/en/install-windows-server.md ou docs/tr/install-windows-server.md.
- Precisa de verificação de release -> docs/en/release-asset-verification.md ou docs/tr/release-asset-verification.md.
- Precisa de troubleshooting -> docs/en/troubleshooting.md, docs/tr/troubleshooting.md ou artigos KB.
- Precisa de postura pública de segurança -> docs/en/security-and-trust-model.md, docs/tr/security-and-trust-model.md e SECURITY.md.

## Mapa do repositório

|Caminho | Por que importa|
|--- | ---|
|`docs/en/` e `docs/tr/` | documentação principal do produto|
|`kb/en/` e `kb/tr/` | artigos KB de troubleshooting|
|[assets/screenshots/](assets/screenshots/) | screenshots públicos|
|[assets/visuals/](assets/visuals/) | diagramas SVG públicos|
|[RELEASES.md](RELEASES.md) | notas de release e assets|
|[PRIVACY.md](PRIVACY.md) | política de privacidade|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | validador de documentação|
|[SECURITY.md](SECURITY.md) | política de security disclosure|

## Fluxo de trabalho

1. Atualize as duas árvores de idioma quando o contrato do produto mudar.
2. Mantenha release notes e orientação de verificação alinhadas aos assets públicos reais.
3. Valide docs e links antes do commit.
4. Execute secret scan antes do push.
5. Verifique remote HEAD e rendering de GitHub release/page após publicação.

## Comandos e validação

Execute estes comandos somente depois de clonar o repositório e entender o que eles verificam ou escrevem.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Lista de verificação

- Os índices de documentação em inglês e turco estão acessíveis.
- Screenshots e assets visuais referenciados pelo README existem.
- Não há dados privados de vault, nomes de clientes, licenças, signing keys ou update secrets.
- O texto de verificação de release coincide com RELEASES.md.
- Remote HEAD é verificado após o push.

## Limite de segurança

- Documenta o contrato operacional enterprise e o caminho de confiança de releases.
- Fornece árvores de documentação em inglês e turco mais artigos KB.
- Mantém release assets e update trust chain documentados.
- Inclui screenshots, assets visuais e scripts de validação para docs públicas.

Regra public-safe: não adicione secrets, tokens, cookies, private keys, prompts privados, dados de clientes, arquivos auth locais, logs gerados, arquivos compactados ou build outputs, salvo quando o README canônico disser explicitamente que pertencem ao repo público.

## Higiene de release e publicação

- Publique installers e arquivos via GitHub Releases, não em commits de source.
- Não commite build output, support packs privados ou signing material.
- Atualize a documentação antes de anunciar status de release pública.
- Confira nomes de assets, versões e remote HEAD após push/release.

## Manutenção

- Mantenha este README localizado alinhado com README.md quando o contrato do repo mudar.
- Prefira links factuais do repo em vez de claims de marketing.
- Não invente comandos de instalação, métricas, usuários, releases ou promessas de suporte.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Caminho de contribuição

- Abra uma mudança focada no menor conjunto de arquivos.
- Leia AGENTS.md ou CONTRIBUTING.md antes de editar quando existirem.
- Execute os comandos de validação do repo listados acima.
- Revise explicitamente os staged diffs antes do commit.
- Use canais de security disclosure, não issues públicas, para relatos sensíveis.

## Definição de concluído

Concluído significa: conteúdo completo, links corretos, limites de segurança claros, validação executada, Git limpo e remote HEAD verificado depois do push.

|Recomendação | Por que importa|
|--- | ---|
|Conteúdo | Central pública de documentação e releases para o VaultPilot password and secrets manager.|
|Links | Todos os arquivos locais referenciados devem existir e resolver a partir da raiz do repositório.|
|Segurança | Não devem aparecer dados privados de vault, nomes de clientes, licenças, signing keys ou update secrets.|
|Verification | Valide estrutura, links, Markdown, segredos, scripts relevantes e remote HEAD antes de afirmar que algo foi publicado.|
|Remote | Após o push, compare local HEAD com origin/main e GitHub remote HEAD.|

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
