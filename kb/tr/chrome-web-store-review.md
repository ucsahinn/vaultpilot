# Chrome Web Store İncelemesi Veya Gizlilik Uyumsuzluğu

Chrome Web Store güncellemesi bloklanırsa, privacy practices sayfası eklentiyle uyumsuz kalırsa veya reviewer permission, data-use, screenshot ya da uzaktan kod kanıtını daha net isterse bu makaleyi kullanın.

## İlk Kontroller

1. Gönderilen extension ID değerinin `hjkbedlaieikhkoplgpiohlaakgebobi` olduğunu doğrulayın.
2. Gönderilen package version değerinin release notes ve [Chrome Web Store listeleme rehberi](../../docs/tr/chrome-web-store-listing.md) ile eşleştiğini doğrulayın.
3. Developer Dashboard privacy practices alanını [PRIVACY.md](../../PRIVACY.md) ile karşılaştırın. Güncel disclosure kategorileri personally identifiable information, authentication information ve web history olmalıdır.
4. Paketlenmiş `manifest.json` içindeki permissions ve host permissions değerlerini inceleyin.
5. Yüklemeden önce paketlenmiş eklentide uzaktan çalıştırılabilir kod örüntüsü arayın.
6. Tüm screenshot'ların sentetik veri kullandığını ve gönderilen VaultPilot release UI ile eşleştiğini doğrulayın.

Reviewer paket kanıtı isterse [Chrome Web Store listeleme rehberindeki](../../docs/tr/chrome-web-store-listing.md#paket-audit-komutları) Paket Audit Komutları'nı çalıştırın ve çıktıyı redakte edilmiş submission notlarıyla birlikte saklayın.

## Sık Görülen İnceleme Sebepleri

| Belirti | Olası sebep | Düzeltme |
| --- | --- | --- |
| Privacy practices uyumsuz | Dashboard kategorileri, privacy policy ve eklenti davranışı aynı data handling modelini anlatmıyor. | Yeniden göndermeden önce üçünü aynı hizaya getirin. |
| Permission gerekçesi reddedildi | Permission açıklanan özellik setinden daha broad veya özellik kullanıcıya görünür değil. | Kullanılmayan permission'ı kaldırın ya da permission gerektiren kullanıcıya dönük özelliği dokümante edin. |
| Uzaktan barındırılan kod şüphesi | Paketlenmiş eklenti, extension dosyaları dışından çalıştırılabilir JavaScript veya WASM yüklüyor. | Çalıştırılabilir kodu eklenti paketinin içine alın; API yanıtlarını yalnız data olarak tutun. |
| Screenshot reddedildi veya güvensiz | Screenshot gerçek hostname, kullanıcı, secret başlığı, log, token veya support context içeriyor. | Sentetik veri kullanan, yayıma uygun hale getirilmiş VaultPilot screenshot'larıyla değiştirin. |
| Mağaza metni bayat görünüyor | Listing hâlâ PassMan'ı güncel ürün gibi veya ZIP'i normal kurulum yolu gibi anlatıyor. | Listeleme rehberindeki yayıncı paneli aktarım notunu kullanın, VaultPilot'u ürün adı olarak tutun ve normal kurulum/güncelleme kanalı Chrome Web Store olarak kalsın. |

## Güvenli Kanıt

Yalnız şunları paylaşın:

- Extension ID ve sürüm.
- Redakte edilmiş red gerekçesi veya inceleme mesajı.
- Paketlenmiş `manifest.json` permission listesi.
- Screenshot dosya adları ve yayıma uygun önizleme durumu.
- [PRIVACY.md](../../PRIVACY.md) ve Developer Dashboard kategorilerinin eşleşip eşleşmediği.

Public olarak paylaşmayın:

- Geliştirici hesabından özel hesap verisi içeren screenshot'lar.
- Gerçek müşteri URL'leri, kullanıcı adları, kasa kayıt adları, token'lar, loglar, database, backup, sertifika veya support ticket içerikleri.

## Eskalasyon

Review sorunu ürün davranışıyla ilgiliyse store resubmission öncesinde eklenti paketini düzeltin. Sorun yalnız public wording ise [Chrome Web Store listeleme ve privacy](../../docs/tr/chrome-web-store-listing.md), [PRIVACY.md](../../PRIVACY.md), [tarayıcı eklentisi dokümanı](../../docs/tr/browser-extension.md) ve release notes birlikte güncellenmelidir.

## İlgili

- [Chrome Web Store mağaza kaydı ve gizlilik](../../docs/tr/chrome-web-store-listing.md)
- [Tarayıcı eklentisi](../../docs/tr/browser-extension.md)
- [Dış public yüzey farkları](../../docs/tr/public-external-surface-drift.md)
- [Public ekran görüntüsü standartları](../../docs/tr/public-screenshot-standards.md)
