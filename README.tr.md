# &#128274; PassMan Enterprise Vault Console - eksiksiz Türkçe README

[&#127468;&#127463; English](README.md) | [&#127465;&#127466; Deutsch](README.de.md) | [&#127466;&#127480; Español](README.es.md) | [&#127463;&#127479; Português (Brasil)](README.pt-BR.md) | [&#127481;&#127479; Türkçe](README.tr.md) | [&#127467;&#127479; Français](README.fr.md)

> Bu dosya kısa bir özet değil, tam Türkçe giriş sayfasıdır. Amaç, sınır, kullanım, doğrulama, güvenlik ve yayın akışını tek yerde anlatır.
>
> Kanonik İngilizce README: [README.md](README.md)

Public documentation and release hub for the PassMan enterprise password manager.

En güncel İngilizce anlatım için kanonik README ile başlayın. Aynı operasyonel sözleşmeyi Türkçe okumak için bu sayfayı kullanın.

## Durum ve güven sinyalleri

|Alan | Detay|
|--- | ---|
|Durum | Public repository: ucsahinn/passman|
|Doğru kaynak | [Kanonik İngilizce README](README.md)|
|Kullanıcılar | Enterprise operators installing or reviewing PassMan.; Admins checking update, backup, AD and browser extension workflows.|
|Doğrulama | English and Turkish doc indexes remain reachable.; Screenshots and visual assets referenced by README exist.|
|Güvenlik | Documents enterprise operating contract and release trust path.; Provides English and Turkish documentation trees plus knowledge base articles.|

## Bu repo nedir

- A public documentation hub for PassMan Enterprise Vault Console.
- A release and verification gateway for users checking public assets.
- A documentation map for admin quickstart, Windows Server install, AD agent, backups, browser extension, sharing, update center and troubleshooting.
- A safe public surface for product explanation without exposing private source or customer vault data.

## Ne değildir

- Not the private application source repository.
- Not a vault, credential store or customer tenant.
- Not a place for signing keys, license secrets, update keys or private support bundles.
- Not a replacement for validating downloaded release assets.

## Kimler için

- Enterprise operators installing or reviewing PassMan.
- Admins checking update, backup, AD and browser extension workflows.
- Security reviewers checking trust model and release verification.
- Support users looking for public troubleshooting and evidence-pack guidance.

## Hızlı başlangıç

1. Repoyu klonla veya güncelle.
2. README, güvenlik ve doküman haritasını oku.
3. Uygun doğrulamaları çalıştır.
4. Sadece bilinçli değişen dosyaları stage et.
5. Push veya release öncesi remote, secret ve link kontrollerini tekrar yap.

## Karar rehberi

- Need overview -> docs/en/overview.md or docs/tr/overview.md.
- Need install -> docs/en/install-windows-server.md or docs/tr/install-windows-server.md.
- Need release verification -> docs/en/release-asset-verification.md.
- Need troubleshooting -> docs/en/troubleshooting.md or kb articles.
- Need public security posture -> docs/en/security-and-trust-model.md and SECURITY.md.

## Repo haritası

|Yol | Neden önemli|
|--- | ---|
|`docs/en/ and docs/tr/` | main product documentation|
|`kb/en/ and kb/tr/` | knowledge base troubleshooting articles|
|[assets/screenshots/](assets/screenshots/) | public screenshots|
|[assets/visuals/](assets/visuals/) | public SVG diagrams|
|[RELEASES.md](RELEASES.md) | release and asset notes|
|[PRIVACY.md](PRIVACY.md) | privacy policy|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | documentation validator|
|[SECURITY.md](SECURITY.md) | security disclosure policy|

## Çalışma akışı

1. Update docs in both language trees when the product contract changes.
2. Keep release notes and verification guidance aligned with actual public assets.
3. Validate docs and links before commit.
4. Run secret scan before push.
5. Verify remote HEAD and GitHub release/page rendering after publication.

## Komutlar ve doğrulama

Bu komutları sadece repoyu yerelde klonladıktan ve neyi kontrol ettiklerini anladıktan sonra çalıştırın.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Doğrulama listesi

- English and Turkish doc indexes remain reachable.
- Screenshots and visual assets referenced by README exist.
- No private vault data, customer names, licenses, signing keys or update secrets appear.
- Release verification wording matches RELEASES.md.
- Remote HEAD is verified after push.

## Güvenlik sınırı

- Documents enterprise operating contract and release trust path.
- Provides English and Turkish documentation trees plus knowledge base articles.
- Keeps release assets and update trust chain documented.
- Includes screenshots, visual assets and validation scripts for public docs.

Public-safe rule: do not add secrets, tokens, cookies, private keys, private prompts, customer data, local-only auth files, generated logs, archives or build outputs unless the canonical README explicitly says they belong in the public repo.

## Release ve yayın hijyeni

- Publish installers and archives through GitHub Releases, not source commits.
- Do not commit build output, private support packs or signing material.
- Update documentation before announcing public release status.
- Check release asset names, versions and remote HEAD after push/release.

## Bakım

- Keep this localized README aligned with README.md when the repo contract changes.
- Prefer factual repo links over marketing claims.
- Do not invent install commands, metrics, users, releases or support promises.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Katkı yolu

- Open a focused change against the smallest set of files.
- Read AGENTS.md or CONTRIBUTING.md when present before editing.
- Run the repo validation commands listed above.
- Review staged diffs explicitly before commit.
- Use security disclosure paths instead of public issues for sensitive reports.

## Bitti tanımı

Bitti demek: içerik tam, linkler doğru, güvenlik sınırı net, doğrulama çalışmış, Git temiz ve push sonrası remote HEAD kontrol edilmiş demektir.

|Öneri | Neden önemli|
|--- | ---|
|Content | Public documentation and release hub for the PassMan enterprise password manager.|
|Links | All referenced local files must exist and resolve from the repository root.|
|Security | No private vault data, customer names, licenses, signing keys or update secrets appear.|
|Verification | Public bir iddia vermeden önce yapıyı, linkleri, Markdown’u, secret taramasını, ilgili scriptleri ve remote HEAD’i doğrula.|
|Remote | After push, compare local HEAD with origin/main and GitHub remote HEAD.|

## Önemli bağlantılar

|Yol | Neden önemli|
|--- | ---|
|[Canonical README](README.md) | README.md|
|[English docs](docs/en/README.md) | docs/en/README.md|
|[Turkish docs](docs/tr/README.md) | docs/tr/README.md|
|[English knowledge base](kb/en/README.md) | kb/en/README.md|
|[Turkish knowledge base](kb/tr/README.md) | kb/tr/README.md|
|[Release notes](RELEASES.md) | RELEASES.md|
|[Privacy](PRIVACY.md) | PRIVACY.md|
|[Security policy](SECURITY.md) | SECURITY.md|
