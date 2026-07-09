# Sertifikalar Ekranı

Üst çubuktaki `?` bu sayfayı Sertifikalar ekranından açar. Bu ekran, Sunucu ayarları içindeki server HTTPS paketinden ayrı olarak kasada saklanan sertifika kayıtları içindir.

## Burada Ne Yapılır

- Subject, issuer, SAN özeti, süre sonu ve sahip bilgisini kaydedin.
- Paket parolası ve private key materyalini başlık veya public not içinde değil, şifreli alanda tutun.
- Tarayıcı veya servis uyarıları başlamadan yenilemeyi planlamak için expiry filtrelerini kullanın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Geçerli | Sahip, expiry ve sistem ilişkisi bilgisinin bulunduğunu doğrulayın. |
| Süresi yaklaşıyor | Yeni materyal yüklemeden önce yenileme planlayın. |
| Upload sorunu | Tekrar denemeden önce dosya türü, boyut ve passphrase bilgisini private doğrulayın. |

## İşlemden Önce

- Sertifika kaydının yalnız envanter mi yoksa kurulu sunucu paketiyle ilişkili mi olduğunu doğrulayın.
- Metadata yüklemeden veya değiştirmeden önce sahip, expiry ve host kapsamını inceleyin.
- Private key işlemlerini public support dışında tutun; yalnız redakte parmak izi veya expiry penceresi yazın.

## Güvenli Kanıt

- Paylaşılabilir: sertifika kayıt türü, expiry penceresi, redakte parmak izi prefix'i ve sahip/review durumu.
- Gizli kalmalı: private key, paket parolası, tam SAN listesi, müşteri hostname'i, içe aktarılan sertifika dosyası ve redakte edilmemiş ekran görüntüsü.
- Açığa çıkan private key veya paket parolasını, private inceleme tamamlanana kadar compromised kabul edin.

## Operatör Notları

Kasa sertifika kayıtlarını server'ın public HTTPS sertifika yükleme akışıyla karıştırmayın. Production HTTPS değişimi Sunucu ayarları içinde yapılır.

## İlgili

- [Sertifika Paneli ekranı](screen-certificate-dashboard.md)
- [Sunucu ayarları ekranı](screen-server-settings.md)
- [Public host ve HTTPS](public-host-https-certificate.md)
