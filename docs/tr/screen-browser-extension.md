# Tarayıcı Eklentisi Ekranı

Üst çubuktaki `?` bu sayfayı Tarayıcı eklentisi ekranından açar. Eşleştirme durumunu, onaylı cihazları, eklenti sağlığını ve Chrome Web Store güncelleme beklentilerini yönetmek için kullanın.

## Burada Ne Yapılır

- Yalnız bilinen tarayıcı profillerini onaylayın.
- Kayıp, bayat veya beklenmeyen cihazların erişimini iptal edin.
- Normal kurulum ve güncelleme yolu olarak Chrome Web Store'u kullanın; ZIP dosyaları arşiv, geliştirme veya acil geri dönüş içindir.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Beklemede | Onaydan önce origin, hesap ve tarayıcı profilini doğrulayın. |
| Onaylı | Son eşitleme zamanını kontrol edin ve kullanılmayan cihazların erişimini iptal edin. |
| Hatalı | Yeniden kurulum veya public kanıt hazırlamadan önce eklenti eşleştirme KB'sini kullanın. |

## İşlemden Önce

- Onay öncesi eşleştirme kodu, kullanıcı talebi, cihaz adı ve tarayıcı bilgisinin eşleştiğini doğrulayın.
- Eşitleme sorununu araştırmadan önce cihazın managed, bayat veya iptal edilmiş durumda olup olmadığını kontrol edin.
- Eklenti kimliği ve sürüm bilgisini public paylaşım için güvenli tutun; eşleştirme materyali gizli kalır.

## Güvenli Kanıt

- Paylaşılabilir: eklenti kimliği, eklenti sürümü, tarayıcı ailesi, redakte cihaz durumu ve Chrome Web Store durumu.
- Gizli kalmalı: eşleştirme kodu, cihaz anahtarı, host'a özel ekran görüntüsü, kasa sayısı ve autofill sırasında görünen kayıt değerleri.
- Normal kurulum/güncelleme referansı olarak Chrome Web Store listing kullanılır; ZIP paketleri yalnız fallback veya lab kanıtıdır.

## Operatör Notları

Eşleştirme kodu, eklenti cihaz ID'si, host'a özel ekran görüntüsü veya otomatik doldurma sırasında görünen kasa kayıt değeri yayınlamayın.

## İlgili

- [Tarayıcı eklentisi](browser-extension.md)
- [Chrome Web Store mağaza kaydı ve gizlilik](chrome-web-store-listing.md)
- [Eklenti eşleştirme KB](../../kb/tr/extension-pairing.md)
