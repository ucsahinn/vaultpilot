# Public Doğrulama Başarısız Oluyor

`npm run validate`, `npm run validate:staged`, `git diff --check` veya Gitleaks public dokümantasyon değişikliğini blokluyorsa bu makaleyi kullanın.

## İlk Kontroller

1. Public repository root içinde olduğunuzu doğrulayın.
2. `git status --short --branch` çalıştırın ve başarısız olan dosyaların hedef public docs değişimine ait olduğunu doğrulayın.
3. Edit yapmadan önce exact validator mesajını okuyun. Yalnız dosya adına bakarak tahmin yürütmeyin.
4. Hata yalnız staged tree içindeyse `git diff` ve `git diff --cached` karşılaştırın.
5. Gitleaks secret-like değer raporlarsa durun ve kanıtı private review'a taşıyın. Değeri public issue içine yapıştırmayın.

## Sık Görülen Hata Türleri

| Hata | Anlamı | Düzeltme |
| --- | --- | --- |
| Paired EN/TR dosyası eksik | Bir doc veya KB sayfası yalnız tek language directory içinde var. | Paired dosyayı ekleyin veya accidental unpaired dosyayı publication öncesi kaldırın. |
| Broken local link | Markdown link public tree içinde olmayan bir dosyaya gidiyor. | Relative path'i düzeltin veya hedef dosyayı ekleyin. |
| Required file missing | Core public surface, screenshot, visual, workflow, template veya policy dosyası yok. | Gerekli herkese açık paylaşım için güvenli dosyayı restore edin veya oluşturun. Required list'i bypass etmeyin. |
| Forbidden stale wording | Release, ürün adı, screenshot, static-site veya compatibility ifadesi misleading olarak biliniyor. | Kanonik VaultPilot wording veya net legacy compatibility açıklamasıyla değiştirin. |
| Encoding artifact | Metin mojibake veya replacement character içeriyor. | Kırık console output'u korumak yerine etkilenen metni UTF-8 olarak yeniden yazın. |
| Release binary git içinde | Installer, archive, manifest, support script, database veya certificate package git tree içinde. | Release delivery artifact'lerini GitHub Releases'a taşıyın; commit etmeyin. |
| Secret-like pattern | Dosya token-like, key-like, local-path veya customer-like kanıt içeriyor. | Placeholder kullanın ve gerçek credential exposed ise private support üzerinden rotate/revoke edin. |
| Whitespace check failure | `git diff --check` patch formatting, conflict marker veya trailing whitespace buldu. | Stage etmeden önce exact satırları düzeltin. |

## Güvenli Recovery

- Broad rewrite yerine küçük ve hedefli editleri tercih edin.
- Validator strict kalsın. Yeni public asset meşruysa aynı değişiklikte `scripts/validate-docs.mjs` güncelleyin ve asset'in neden safe olduğunu açıklayın.
- Açık owner onayı olmadan dosya silmeyin veya generated artifact purge etmeyin.
- `validate:staged` geçsin diye ilgisiz dirty dosyaları stage etmeyin.
- Her fix sonrası başarısız olan komutu tekrar çalıştırın; sonra [Public repo yayın runbook'u](../../docs/tr/publication-runbook.md) içindeki tam publication sırasını çalıştırın.

## Paylaşılabilecek Kanıt

Public review için paylaşılabilir kanıt şunları içerebilir:

- Başarısız olan komut.
- Redakte edilmiş hata mesajı.
- Etkilenen public file path.
- Hatanın working-tree-only mi staged-only mi olduğu.
- Check'in geçtiğini gösteren final command output.

Raw secret value, müşteri path'i, account screenshot'ı, database, backup, certificate, release binary veya redakte edilmemiş log paylaşmayın.

## İlgili

- [Public repo yayın runbook'u](../../docs/tr/publication-runbook.md)
- [Public repo sınırı](../../docs/tr/public-repository-boundary.md)
- [Public ekran görüntüsü standartları](../../docs/tr/public-screenshot-standards.md)
- [Public issue redaction](public-issue-redaction.md)
