# &#128274; VaultPilot Enterprise Vault Console - Türkçe giriş README'si

<p align="center">
  &#127760; <strong>Dok&#252;man dilleri:</strong>
  <a href="README.de.md"><img src="https://flagcdn.com/w20/de.png" alt="Deutsch" width="20"></a> |
  <a href="README.es.md"><img src="https://flagcdn.com/w20/es.png" alt="Espa&#241;ol" width="20"></a> |
  <a href="README.md"><img src="https://flagcdn.com/w20/gb.png" alt="English" width="20"></a> |
  <a href="README.pt-BR.md"><img src="https://flagcdn.com/w20/br.png" alt="Portugu&#234;s (Brasil)" width="20"></a> |
  <a href="README.tr.md"><img src="https://flagcdn.com/w20/tr.png" alt="T&#252;rk&#231;e" width="20"></a> |
  <a href="README.fr.md"><img src="https://flagcdn.com/w20/fr.png" alt="Fran&#231;ais" width="20"></a>
</p>

> Bu dosya Türkçe giriş sayfasıdır. Amaç, sınır, kullanım, doğrulama, güvenlik ve yayın akışını tek yerde anlatır.
>
> Kanonik İngilizce README: [README.md](README.md)

VaultPilot password and secrets manager için public dokümantasyon ve release merkezi.

En güncel İngilizce anlatım için kanonik README ile başlayın. Aynı operasyonel sözleşmeyi Türkçe okumak için bu sayfayı kullanın.

## Durum ve güven sinyalleri

|Alan | Detay|
|--- | ---|
|Durum | Public repository: ucsahinn/vaultpilot|
|Güncel public release | VaultPilot 2.0.0, 30 Haziran 2026'da GitHub Release `v2.0.0` olarak yayınlandı.|
|Compatibility notu | PassMan adı eski servisler, data path'ler, env var'lar, cookie/header/protocol string'leri, update alias'ları ve rollback kararları için korunur.|
|Doğru kaynak | [Kanonik İngilizce README](README.md)|
|Kullanıcılar | VaultPilot kuran veya inceleyen enterprise operatörleri; update, backup, AD ve tarayıcı eklentisi akışlarını kontrol eden adminler.|
|Doğrulama | İngilizce ve Türkçe doküman indeksleri erişilebilir kalır; README'de referans verilen screenshot ve görsel assetler vardır.|
|Güvenlik | Enterprise operasyon sözleşmesini ve release trust path'i belgeler; İngilizce/Türkçe dokümantasyon ağaçları ve KB makaleleri sağlar.|

## Bu repo nedir

- VaultPilot Enterprise Vault Console için public dokümantasyon merkezi.
- Public assetleri kontrol eden kullanıcılar için release ve doğrulama geçidi.
- Admin quickstart, Windows Server kurulumu, AD agent, backup, tarayıcı eklentisi, paylaşım, update center ve troubleshooting için doküman haritası.
- Private source veya müşteri kasa verisi yayınlamadan ürünü anlatan güvenli public yüzey.
- Güncel VaultPilot release assetleri için GitHub Releases sayfasına yönlendirir; eski PassMan buildlerini yeni kurulum yolu gibi sunmaz.

## Ne değildir

- Private uygulama source repository değildir.
- Kasa, credential store veya müşteri tenant'ı değildir.
- Signing key, license secret, update key veya private support bundle saklama yeri değildir.
- İndirilen release assetlerini doğrulamanın yerine geçmez.

## Kimler için

- VaultPilot kuran veya inceleyen enterprise operatörleri.
- Update, backup, AD ve tarayıcı eklentisi akışlarını kontrol eden adminler.
- Trust model ve release doğrulamasını inceleyen güvenlik ekipleri.
- Public troubleshooting ve evidence-pack rehberi arayan support kullanıcıları.

## Hızlı başlangıç

1. Repoyu klonla veya güncelle.
2. README, güvenlik ve doküman haritasını oku.
3. Uygun doğrulamaları çalıştır.
4. Sadece bilinçli değişen dosyaları stage et.
5. Push veya release öncesi remote, secret ve link kontrollerini tekrar yap.

## Karar rehberi

- Genel bakış gerekiyorsa -> docs/en/overview.md veya docs/tr/overview.md.
- Kurulum gerekiyorsa -> docs/en/install-windows-server.md veya docs/tr/install-windows-server.md.
- Release doğrulaması gerekiyorsa -> docs/tr/release-asset-verification.md veya docs/en/release-asset-verification.md.
- Sorun giderme gerekiyorsa -> docs/tr/troubleshooting.md, docs/en/troubleshooting.md veya KB makaleleri.
- Public güvenlik duruşu gerekiyorsa -> docs/tr/security-and-trust-model.md, docs/en/security-and-trust-model.md ve SECURITY.md.

## Repo haritası

|Yol | Neden önemli|
|--- | ---|
|`docs/en/` ve `docs/tr/` | ana ürün dokümantasyonu|
|`kb/en/` ve `kb/tr/` | troubleshooting bilgi bankası makaleleri|
|[assets/screenshots/](assets/screenshots/) | public screenshotlar|
|[assets/visuals/](assets/visuals/) | public SVG diyagramlar|
|[RELEASES.md](RELEASES.md) | release ve asset notları|
|[PRIVACY.md](PRIVACY.md) | privacy policy|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | dokümantasyon validator'ı|
|[SECURITY.md](SECURITY.md) | güvenlik bildirim politikası|

## Çalışma akışı

1. Ürün sözleşmesi değiştiğinde iki dil ağacındaki dokümanları güncelle.
2. Release notes ve doğrulama rehberini gerçek public assetlerle uyumlu tut.
3. Commit öncesi dokümanları ve linkleri doğrula.
4. Push öncesi secret scan çalıştır.
5. Yayın sonrası remote HEAD ve GitHub release/page rendering durumunu doğrula.

## Komutlar ve doğrulama

Bu komutları sadece repoyu yerelde klonladıktan ve neyi kontrol ettiklerini anladıktan sonra çalıştırın.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Doğrulama listesi

- İngilizce ve Türkçe doküman indeksleri erişilebilir.
- README'de referans verilen screenshot ve görsel assetler mevcut.
- Private vault verisi, müşteri adı, lisans, signing key veya update secret yok.
- Release doğrulama dili RELEASES.md ile uyumlu.
- Push sonrası remote HEAD doğrulanmış.

## Güvenlik sınırı

- Enterprise operasyon sözleşmesini ve release trust path'i belgeler.
- İngilizce ve Türkçe dokümantasyon ağaçları ile KB makaleleri sağlar.
- Release assetlerini ve update trust chain'i belgeli tutar.
- Public docs için screenshot, görsel asset ve validation scriptleri içerir.

Public-safe kural: kanonik README açıkça public repo kapsamına aldığını söylemediği sürece secret, token, cookie, private key, private prompt, müşteri verisi, local-only auth dosyası, üretilmiş log, arşiv veya build output ekleme.

## Release ve yayın hijyeni

- Installer ve arşivleri source commit ile değil GitHub Releases üzerinden yayınla.
- Build output, private support pack veya signing material commit etme.
- Public release status duyurmadan önce dokümantasyonu güncelle.
- Push/release sonrası asset adlarını, versiyonları ve remote HEAD'i kontrol et.

## Bakım

- Repo sözleşmesi değiştiğinde bu lokalize README'yi README.md ile hizala.
- Marketing iddiası yerine somut repo linklerini tercih et.
- Install komutu, metrik, kullanıcı, release veya support vaadi uydurma.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Katkı yolu

- En küçük dosya setine odaklanan bir değişiklik aç.
- Düzenleme öncesi varsa AGENTS.md veya CONTRIBUTING.md dosyasını oku.
- Yukarıda listelenen repo doğrulama komutlarını çalıştır.
- Commit öncesi staged diff'leri açıkça incele.
- Hassas bildirimler için public issue yerine security disclosure yolunu kullan.

## Bitti tanımı

Bitti demek: içerik tam, linkler doğru, güvenlik sınırı net, doğrulama çalışmış, Git temiz ve push sonrası remote HEAD kontrol edilmiş demektir.

|Öneri | Neden önemli|
|--- | ---|
|İçerik | VaultPilot password and secrets manager için public dokümantasyon ve release merkezi.|
|Linkler | Referans verilen tüm lokal dosyalar var olmalı ve repository root üzerinden çözülmeli.|
|Güvenlik | Private vault verisi, müşteri adı, lisans, signing key veya update secret görünmemeli.|
|Verification | Public bir iddia vermeden önce yapıyı, linkleri, Markdown’u, secret taramasını, ilgili scriptleri ve remote HEAD’i doğrula.|
|Remote | Push sonrası local HEAD'i origin/main ve GitHub remote HEAD ile karşılaştır.|

## Önemli bağlantılar

|Yol | Neden önemli|
|--- | ---|
|[Kanonik README](README.md) | README.md|
|[İngilizce dokümanlar](docs/en/README.md) | docs/en/README.md|
|[Türkçe dokümanlar](docs/tr/README.md) | docs/tr/README.md|
|[İngilizce bilgi bankası](kb/en/README.md) | kb/en/README.md|
|[Türkçe bilgi bankası](kb/tr/README.md) | kb/tr/README.md|
|[Release notları](RELEASES.md) | RELEASES.md|
|[Privacy](PRIVACY.md) | PRIVACY.md|
|[Security policy](SECURITY.md) | SECURITY.md|
