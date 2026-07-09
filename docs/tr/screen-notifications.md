# Bildirimler Ekranı

Üst çubuktaki `?` bu sayfayı Bildirimler ekranından açar. Hangi event'lerin operatöre bildirilmesi ve hangi recipient'ların alması gerektiğine karar verirken kullanın.

## Burada Ne Yapılır

- Yalnız aksiyon alınabilir event'leri yönlendirin.
- Recipient listelerini güncel ve role uygun tutun.
- SMTP teslimat testini parola veya mesaj gövdesi public kanıta düşmeden yapın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Configured | Kontrollü test gönderin ve doğru rolün aldığını doğrulayın. |
| Teslim edilemedi | SMTP ayarlarını parola göstermeden private kontrol edin. |
| Çok gürültülü | Non-actionable event'leri kapatın veya recipient kapsamını daraltın. |

## İşlemden Önce

- Hangi event class değerlerinin insana gitmesi, hangilerinin yalnız audit içinde kalması gerektiğini doğrulayın.
- Template değiştirmeden önce recipient group, SMTP sağlığı ve alert frekansını kontrol edin.
- Sample alert içeriklerini redakte edin; mesajlar host, kullanıcı, vault adı veya incident timing gösterebilir.

## Güvenli Kanıt

- Paylaşılabilir: event class, teslim durumu, alıcı rol kategorisi, timestamp aralığı ve redakte SMTP hata kodu.
- Gizli kalmalı: SMTP credential, gerçek e-posta adresi, müşteri hostname'i, mesaj gövdesi ve olaya özel alert payload.
- Teslimat hatası logları transport header veya internal routing detayı içeriyorsa private tutun.

## Operatör Notları

Bildirim örnekleri SMTP parolası, gerçek adres, müşteri hostname'i veya olaya özel gizli değer içermemelidir.

## İlgili

- [Sunucu ayarları ekranı](screen-server-settings.md)
- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Server settings restart ve bakım bilgi bankası](../../kb/tr/server-settings-restart-maintenance.md)
