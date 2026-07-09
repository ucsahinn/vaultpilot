# Entegrasyonlar Ekranı

Üst çubuktaki `?` bu sayfayı Entegrasyonlar ekranından açar. Salt okunur API istemcileri, tarayıcı eklentisi durumu ve dizin entegrasyonu sağlığı için kullanın.

## Burada Ne Yapılır

- API client'ları yalnız gereken scope ve kasa atamasıyla oluşturun.
- Üretilen secret'ı yalnız bir kez kopyalayıp tüketen sistemin onaylı secret deposuna koyun.
- Atıl erişim bırakmak yerine kullanılmayan istemcileri ve tarayıcı cihazlarını iptal edin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Sağlıklı | Kapsam, sahip ve son kullanım durumunun hâlâ gerekçeli olduğunu doğrulayın. |
| Unauthorized | Kimlik bilgisi veya token'ları ilgili entegrasyon yolundan döndürün. |
| Over-scoped | Yeni client material vermeden önce yetkiyi azaltın. |

## İşlemden Önce

- Değişikliğin API client, browser extension cihazı veya directory connector etkisi olup olmadığını belirleyin.
- Revoke veya rotation öncesi sahip, scope, son kullanım ve tüketen sistemi kontrol edin.
- Otomasyonun kullandığı credential'ı kaldırmadan önce dar kapsamlı yeni kayıt oluşturmayı tercih edin.

## Güvenli Kanıt

- Paylaşılabilir: entegrasyon türü, gerekli kapsam, endpoint yolu, status code ve redakte client identifier.
- Gizli kalmalı: client secret, agent token, pairing code, tenant verisi içeren callback URL ve request header'ları.
- Herhangi bir değer exposed olabilir ise public konuşmadan önce private credential'ı rotate veya revoke edin.

## Operatör Notları

Gerçek bağlamla birlikte `pmc_` client ID, `pms_` client secret, eklenti eşleştirme kodu, agent token veya internal host içeren bağlayıcı ekran görüntüsü yayınlamayın.

## İlgili

- [Entegrasyon API client'ları](api-clients.md)
- [Public API referansı](public-api-reference.md)
- [Tarayıcı eklentisi ekranı](screen-browser-extension.md)
