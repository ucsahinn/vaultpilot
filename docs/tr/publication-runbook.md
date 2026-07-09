# Public Repo Yayın Runbook'u

Herkese açık VaultPilot doküman, KB, screenshot, policy veya release-note değişiklikleri review için hazırlanırken bu runbook'u kullanın. Akış bilinçli olarak konservatiftir: önce working tree doğrulanır, commit öncesi git index ayrıca doğrulanır ve hesap tarafı publication işleri repo editlerinden ayrı tutulur.

Bu runbook publish, tag, release, store asset upload, Issues açma, lisans şartı ekleme veya repository settings değiştirme izni vermez. Bu aksiyonlar repository owner onayı gerektirir.

## Güvenli Lokal Sıra

| Adım | Komut veya kanıt | Durdurma koşulu |
| --- | --- | --- |
| Scope incele | `git status --short --branch` | İlgisiz source, üretilmiş artifact, lokal secret, build output, database, certificate, installer, ZIP veya hesap durumu dosyası public docs değişimine karışmış. |
| Dokümanları doğrula | `npm run validate` | Bozuk lokal link, EN/TR parity kayması, eksik gerekli asset, stale release ifadesi, forbidden public-site kalıntısı, encoding kalıntısı, release binary veya secret benzeri örüntü raporlanır. |
| Whitespace kontrolü | `git diff --check` | Trailing whitespace, conflict marker veya patch formatting hatası raporlanır. |
| Secret scan | `gitleaks detect --no-git --redact --verbose --source .` | Leak raporlanır. Secret-like kanıtı private inceleme tamamlanana kadar compromised kabul edin. |
| Diff incele | `git diff --stat` ve hedefli `git diff -- <path>` | Diff accidental deletion, raw release asset, müşteri verisi, local path veya hedef public docs scope dışı dosya içerir. |
| Dosyaları açıkça stage et | Yalnız açık `git add <file>` komutları | Görünen her değişiklik bilinçli dahil edilmedikçe directory bazlı stage veya `git add .` kullanmayın. |
| Index doğrula | `npm run validate:staged` ve `git diff --cached --check` | Staged tree doğrulanan working tree'den farklıdır veya index-only validation fail eder. |
| Staged diff incele | `git diff --cached --stat` ve hedefli `git diff --cached -- <path>` | Staged dosyalar ilgisiz iş, secret, release binary, generated scratch dosyası veya incelenmemiş account talimatı içerir. |

## Ne Commit Edilmeli

Yalnız incelenmiş ve herkese açık paylaşım için güvenli dosyaları commit edin:

- Markdown docs, KB makaleleri, lokalize README'ler, release notes ve policy dosyaları.
- Public validation script'leri ve GitHub workflow tanımları.
- `scripts/validate-docs.mjs` tarafından listelenen herkese açık paylaşım için güvenli screenshot ve görseller.
- GitHub issue template'leri, pull request template'i ve dokümantasyon amaçlı repo metadata dosyaları.

Commit etmeyin:

- MSI, EXE, ZIP, PFX, P12, DB, SQLite, backup, dump, log, coverage, cache, temp veya lokal tarayıcı artifact'leri.
- GitHub Releases içinde kalması gereken update manifest, component manifest, PowerShell destek script'i ve release package dosyaları.
- Private product source code, signing material, müşteri kanıtı, redakte edilmemiş screenshot, account export veya Chrome Web Store dashboard screenshot'ı.
- Repository owner onaylı root `LICENSE` veya `LICENSE.md` olmadan lisans şartı.

## Hesap Tarafı Gate'leri

Bu işler git commit ile tamamlanmaz:

| Yüzey | Gerekli owner aksiyonu |
| --- | --- |
| GitHub repository açıklaması, homepage, topics, social preview, Issues, Discussions, security policy ayarları | Owner onayından sonra GitHub repository settings içinde değiştirilir. |
| GitHub Release title, notes ve asset upload | Release-owner onayıyla GitHub Release kaydı üzerinde değiştirilir. |
| Chrome Web Store listing, screenshot, privacy practices ve publication | Chrome Web Store publisher hesabında değiştirilir. |
| Lisans yayını | Owner onaylı root `LICENSE` veya `LICENSE.md` eklenir; ardından şu an lisans şartı yayınlanmadığını söyleyen docs güncellenir. |
| Search Console, analytics, verified publisher status | Hesap tarafı doğrulama gerektirir; token veya verification secret bu repoda saklanmaz. |

## Kaydedilecek Son Kanıt

Review veya publication istemeden önce şunları kaydedin:

- `git status --short --branch` ile branch ve remote durumu.
- Validation komutları ve sonuçları.
- `validate:staged` çalıştırılıp çalıştırılmadığı.
- Bilinçli stage edilen veya bilinçli untracked bırakılan dosyalar.
- Kalan owner/account-side gated aksiyonlar.
- [Public external surface drift](public-external-surface-drift.md) sayfasının latest GitHub Release ve Chrome Web Store gözlemleriyle güncellenip güncellenmediği.
- Çalıştırılamayan kontroller ve exact command/failure reason.

## Validation Fail Ederse

[Public validation failure KB](../../kb/tr/public-validation-fails.md) sayfasını kullanın. Validator'ı zayıflatmak yerine sebebi düzeltin. Validator meşru yeni public asset'i blokluyorsa manifest'i güncelleyin ve aynı değişiklikte kısa gerekçe ekleyin.

İlgili:

- [Public repo sınırı](public-repository-boundary.md)
- [Public keşfedilebilirlik](public-discoverability.md)
- [Public external surface drift](public-external-surface-drift.md)
- [GitHub repo profili](github-repository-profile.md)
- [Chrome Web Store listeleme ve privacy](chrome-web-store-listing.md)
- [Katkı kuralları](../../CONTRIBUTING.md)
