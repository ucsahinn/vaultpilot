# Güncellemeler Ekranı

Üst çubuktaki `?` bu sayfayı Güncellemeler ekranından açar. Sunucu, tarayıcı eklentisi ve destek bileşeni güncelleme durumlarını güncelleme başlatmadan önce doğrulamak için kullanın.

## Burada Ne Yapılır

- Başlatmadan önce manifest, paket URL'si, SHA-256, imzacı ve sürüm bilgisini inceleyin.
- Paket kanıtı bayat görünüyorsa canlı kontrol kullanın.
- Güncelleme hatasını doğrulamayı atlama sebebi değil, kanıta dayalı olay olarak ele alın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Güncelleme var | Başlatmadan önce manifest, hash ve imzacı bilgisini doğrulayın. |
| Kurulum sürüyor | Servis yeniden başlatma penceresini bekleyin ve iş detayını izleyin. |
| Takıldı | Paket değişimi veya yeniden deneme öncesi yüzde 76 KB'yi kullanın. |

## İşlemden Önce

- Kurulumdan önce yayın etiketi, manifest imzası, SHA-256 ve imzacı bilgisini doğrulayın.
- Servis yeniden başlatmaya izin vermeden önce yedek ve bakım penceresinin hazır olduğunu kontrol edin.
- Doğrulama hatasını kontrol atlama sebebi değil, durma koşulu olarak ele alın.

## Güvenli Kanıt

- Paylaşılabilir: yayın etiketi, bileşen adı, iş ID'si, hash eşleşme veya uyuşmazlık durumu ve imzacı özeti.
- Gizli kalmalı: kopyalanmış kurulum dosyaları, yerel indirme yolları, private support bundle'ları ve makineye özel loglar.
- İmza, hash veya manifest doğrulama hatasını support kanıtı incelenene kadar durma koşulu olarak ele alın.

## Operatör Notları

Yayın binary'si, ZIP paketi ve manifest dosyaları public docs repo içine commit edilmez; GitHub Releases veya onaylı eklenti kanalı üzerinden dağıtılır.

## İlgili

- [Güncelleme Merkezi](update-center.md)
- [Yayın dosyası doğrulama](release-asset-verification.md)
- [Update yüzde 76 civarında takılıyor KB](../../kb/tr/update-stuck-76.md)
