# Sunucu Ayarları Ekranı

Üst çubuktaki `?` bu sayfayı Sunucu ayarları ekranından açar. Public host, HTTPS, SMTP, bakım, saklama ve yerel sunucu yapılandırması için kullanın.

## Burada Ne Yapılır

- Host ve HTTPS ayarlarını bilinçli değiştirin; uzaktan tarayıcı erişimi bu değerlere bağlıdır.
- Yalnız onaylı `.pfx` veya `.p12` sertifika paketlerini arayüz üzerinden yükleyin.
- Restore veya temizlik akışı öncesi gerekli bakım yedeğini dışa aktarın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Yeniden başlatma bekliyor | Yeniden başlatma penceresi planlayın ve bakım kanıtını doğrulayın. |
| Doğrulama hatası | Kaydetmeden önce host, sertifika, SMTP veya saklama girdisini düzeltin. |
| Bakım gerekli | Yıkıcı bakım öncesi gerekli yedeği dışa aktarın. |

## İşlemden Önce

- Değişikliğin tarayıcı erişimi, bildirim, saklama, yedek veya servis yeniden başlatma etkisi olup olmadığını doğrulayın.
- Ayar değiştirmeden önce mevcut host, port, HTTPS ve SMTP durumunu kaydedin.
- Yeniden başlatma etkisi olan değişiklikleri yedek kanıtı ve geri dönüş yolu ile planlayın.

## Güvenli Kanıt

- Paylaşılabilir: etkilenen ayar alanı, timestamp, `<SERVER_HOST>` gibi redakte host biçimi ve görünen doğrulama hatası.
- Gizli kalmalı: PFX/P12 dosyaları, sertifika parolaları, SMTP kimlik bilgileri, yerel path'ler, veritabanı dosyaları ve ham loglar.
- Restart logları veya bakım kanıtı müşteri path'i, hostname veya hesap bağlamı içeriyorsa private support kullanın.

## Operatör Notları

Yerel path, PFX/P12 paketi, sertifika parolası, SMTP kimlik bilgisi, veritabanı dosyası veya ham log yayınlamayın.

## İlgili

- [Server System](server-system.md)
- [Public host ve HTTPS](public-host-https-certificate.md)
- [Server settings restart ve bakım bilgi bankası](../../kb/tr/server-settings-restart-maintenance.md)
