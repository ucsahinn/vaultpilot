# API Anahtarları Ekranı

Üst çubuktaki `?` bu sayfayı API anahtarları ekranından açar. Servis token'larını, entegrasyon secret'larını ve makineden makineye kimlik bilgilerini diskte şifreli tutmak için kullanın.

## Burada Ne Yapılır

- Token değerini yalnız şifreli secret alanında saklayın.
- Sahip, sistem, kapsam, süre sonu ve rotasyon tarihi bilgisini meta veri içinde tutun.
- Sızıntı şüphesi varsa anahtarı kaynak sistemde iptal edip yeniden üretin; yalnız kasa kaydını düzenlemek yeterli değildir.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Sahip yok | Anahtara güvenmeden önce sahiplik atayın. |
| Süresi yaklaşıyor | Değeri değiştirmeden önce rotasyon ve tüketen sistem güncelleme sırasını planlayın. |
| Sızmış | Private olarak döndürün; public görünümü compromised kabul edin. |

## İşlemden Önce

- Kopyalama veya rotasyon öncesi tüketen sistemi, sahibi ve izin verilen kapsamı belirleyin.
- Tüketen taraftaki değişiklik planlanabilsin diye anahtarın otomasyon tarafından kullanılıp kullanılmadığını kontrol edin.
- Kısmi anahtar adlarını, prefix'leri ve entegrasyon URL'lerini public kanallarda hassas bağlam olarak ele alın.

## Güvenli Kanıt

- Paylaşılabilir: endpoint adı, gerekli kapsam, hata kodu, rotasyon durumu ve redakte client identifier prefix'i.
- Gizli kalmalı: API key değerleri, bearer token'lar, OAuth client secret'ları, tam client ID'leri ve request header'ları.
- Exposure ihtimali varsa public konuşmadan önce kaynak sistemde rotate veya revoke edin.

## Operatör Notları

Public örneklerde gerçek görünümlü API key, bearer token, OAuth client secret veya entegrasyon kimlik bilgisi bulunmamalıdır.

## İlgili

- [Public API referansı](public-api-reference.md)
- [Entegrasyon API client'ları](api-clients.md)
- [API client erişimi KB](../../kb/tr/api-client-401.md)
