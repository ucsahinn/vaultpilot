# Sertifika Paneli Ekranı

Üst çubuktaki `?` bu sayfayı Sertifika Paneli ekranından açar. Certificate age, expiry window, trusted-host hizası ve kayıtlı sertifika riskini incelemek için kullanın.

## Burada Ne Yapılır

- Expired, expiring ve hostname-mismatch sertifikalara öncelik verin.
- Uyarının browser HTTPS erişiminden mi, vault sertifika kaydından mı, yoksa Discovery bulgusundan mı geldiğini ayırın.
- Production HTTPS paketlerini public doküman veya issue eki üzerinden değil, Sunucu ayarları içinden değiştirin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Güncel | Owner ve yenileme penceresi bilgisinin hâlâ kayıtlı olduğunu doğrulayın. |
| Süresi yaklaşıyor | Materyal yükleme veya değiştirme öncesi yenileme sahibini atayın. |
| Geçersiz | Package, passphrase veya trust chain net değilse private support'a taşıyın. |

## İşlemden Önce

- Sertifikanın tarayıcı erişimi, envanter kaydı veya ikisi için mi kullanıldığını netleştirin.
- Yeni paket yüklemeden önce expiry, issuer, host binding ve renewal owner bilgisini kontrol edin.
- PFX/P12 işlemlerini onaylı sunucu akışı içinde tutun; public dokümanda yalnız redakte metadata kullanın.

## Güvenli Kanıt

- Paylaşılabilir: sertifika durumu, expiry penceresi, issuer family, redakte subject/SAN özeti ve renewal owner durumu.
- Gizli kalmalı: `.pfx` ve `.p12` dosyaları, private key, passphrase, tam sertifika zinciri ve host'a özel paket ekran görüntüleri.
- Trust chain, passphrase veya production HTTPS değişim kanıtı tam redakte edilemiyorsa private support kullanın.

## Operatör Notları

`.pfx`, `.p12`, private key veya sertifika parolası support evidence içine eklenmez. Yalnız redakte subject/SAN özeti ve expiry tarihi paylaşılabilir.

## İlgili

- [Public host ve HTTPS](public-host-https-certificate.md)
- [Sertifikalar ekranı](screen-certificates.md)
- [HTTPS sertifika uyarısı KB](../../kb/tr/certificate-warning.md)
