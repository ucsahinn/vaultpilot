# Public Repo Sınırı

Bu repo VaultPilot için herkese açık operatör dokümanı ve destek yüzeyidir. Ürün kaynak ağacı, release binary deposu, imza materyali arşivi veya müşteri kanıt kasası değildir.

Issue, pull request veya doküman değişikliği açmadan önce bu sayfayı kullanın.

## Git İçinde Ne Olmalı

- `docs/`, `kb/`, yerelleştirilmiş README'ler ve politika dosyaları altındaki public dokümanlar.
- Sentetik tenant, host, kullanıcı ve kasa verisi kullanan, herkese açık paylaşım için güvenli ekran görüntüleri.
- Doküman hijyenini koruyan public doğrulama script'leri ve GitHub workflow tanımları.
- Yayınlanmış public GitHub Release asset'lerini anlatan release notları.
- Public operatör yolunu güncel tutan link ve ifade düzeltmeleri.

## Lisans Şartları

Bu repo, repository owner tarafından `LICENSE` veya `LICENSE.md` dosyası eklenmediği sürece lisans şartı yayınlamaz. Owner onayı olmadan issue, pull request veya release notlarında doküman, asset, binary ya da ürün kaynak kodu lisansı eklemeyin, varsaymayın veya taahhüt etmeyin.

## GitHub Releases İçinde Ne Olmalı

Release dağıtım artifact'leri git ağacına değil imzalı GitHub Release sayfasına aittir:

- MSI installer dosyaları.
- Browser extension ZIP arşivleri.
- Offline share decrypter arşivleri.
- DC Agent PowerShell script'leri.
- Update manifest'leri ve component manifest'leri.
- Operatörlerin yayınlanmış release ile karşılaştırması gereken checksum, imza ve release kanıtı.

Herkese açık dokümanlar release'e link verebilir ve public asset adlarını, boyutlarını ve SHA-256 değerlerini listeleyebilir. Bu asset'lerin kopyalarını commit etmeyin.

## Neler Private Kalmalı

Aşağıdaki materyalleri issue, pull request, yorum veya commit edilmiş dosyalara eklemeyin:

- Plaintext kasa kayıtları, parolalar, ana parola, share passphrase veya recovery phrase.
- API key, agent token, session cookie, private key, PFX/P12 dosyası veya imza materyali.
- AD bind parolası, Kerberos ticket, hash, database dosyası, yedek veya ham müşteri logu.
- Gerçek kullanıcı, tenant, hostname, internal URL, altyapı adresi veya secret kaydı gösteren ekran görüntüsü.
- Redakte edilmemiş local path, müşteri adı veya support-ticket export'u içeren installer kanıt paketleri.

Örneklerde `<VAULTPILOT_URL>`, `<SERVER_HOST>`, `<AGENT_ID>`, `<AGENT_TOKEN>`, `<LICENSE_CODE>` ve `<REDACTED>` gibi yer tutucu kullanın.

## Public Issue Kuralı

Yalnızca kanıt setinin tamamı public olarak yayınlanmaya uygunsa herkese açık issue açın. Konu redakte edilmemiş log, ekran görüntüsü, database dosyası, sertifika materyali, lisans materyali veya müşteriye özel operasyon verisi gerektiriyorsa private support kanalını kullanın.

İlgili: [Destek politikası](../../SUPPORT.md), [Güvenlik politikası](../../SECURITY.md), [Katkı kuralları](../../CONTRIBUTING.md), [public issue redaction KB](../../kb/tr/public-issue-redaction.md).
