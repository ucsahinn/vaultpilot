# Dosyalar Ekranı

Üst çubuktaki `?` bu sayfayı Dosyalar ekranından açar. Yalnız net sahibi ve saklama gerekçesi olan onaylı şifreli ekler için kullanın.

## Burada Ne Yapılır

- Upload öncesi dosyanın vault'a ait olduğunu doğrulayın.
- Geniş arşiv yerine küçük, incelenebilir destek veya kurtarma kanıtı tercih edin.
- Dosya adında gizli değer değil, amaç ve sahip bilgisini kullanın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Boş | Sahip ve saklama sebebi net değilse dosya eklemeyin. |
| Büyük dosya | VaultPilot yerine onaylı document store'a ait olup olmadığını doğrulayın. |
| Upload blocked | Tekrar denemeden önce role, license ve file policy kontrol edin. |

## İşlemden Önce

- Dosyanın gerçekten kasada tutulması gerektiğini ve daha küçük bir typed record ile temsil edilemeyeceğini doğrulayın.
- Upload öncesi dosya adını, sahibi, review tarihini ve saklama beklentisini kontrol edin.
- Onaylı sanitization yolundan geçmemiş log, dump ve screenshot dosyalarını reddedin.

## Güvenli Kanıt

- Paylaşılabilir: dosya kategorisi, boyut aralığı, sahip/review durumu, saklama gerekçesi ve redakte validation hatası.
- Gizli kalmalı: dosya içeriği, müşteri bağlamı taşıyan dosya adı, database dump, log, installer, release archive, private key ve ham ekran görüntüsü.
- Secret veya müşteri kanıtı içeren dosyayı public konuşmadan önce private support incelemesine taşıyın.

## Operatör Notları

Onaylı internal süreç açıkça gerektirmedikçe database dump, ham log, installer, release archive, private key veya redakte edilmemiş ekran görüntüsü saklamayın.

## İlgili

- [Yedekleme ve geri yükleme](backups-and-restore.md)
- [Public repo sınırı](public-repository-boundary.md)
- [Destek kanıt paketi](support-evidence-pack.md)
