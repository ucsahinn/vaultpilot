# HTTPS sertifika uyarısı

HTTPS etkinleştiğinde kullanıcılar tarayıcı uyarısı görüyorsa bunu kullanın.

## Kontroller

1. Kullanıcıların açtığı host adı sertifika SAN içinde yer almalı.
2. PFX/P12 paketi VaultPilot servisi tarafından okunabilir olmalı.
3. Yapılandırılan port açık olmalı.
4. Sertifika süresi dolmamış olmalı.
5. Private sertifika materyali doküman, log veya ticket içine konmamalı.

## Upload Hataları

Sertifika yükleme Owner-only bir işlemdir. Tam olarak bir `.pfx` veya `.p12` paketi kullanın; dosya 0 byte'tan büyük ve en fazla 2 MB olmalıdır. Upload denemeleri 10 dakikada 6 deneme ile rate-limit edilir. Paketi, parolayı veya private key materyalini public ticket'a eklemeyin.

| Kod | Anlamı | Sonraki kontrol |
| --- | --- | --- |
| `UNSUPPORTED_CERTIFICATE_FILE` | Yüklenen dosya `.pfx` veya `.p12` değil. | Sertifika ve private key'i PFX/P12 paketi olarak export edin. |
| `CERTIFICATE_FILE_SIZE` | Paket boş veya 2 MB üstünde. | Export edilen paket boyutunu doğrulayın ve yeniden deneyin. |
| `CONTENT_LENGTH_REQUIRED` | Upload request içinde `Content-Length` yok. | UI üzerinden yeniden deneyin veya header gönderen bir client kullanın. |
| `PAYLOAD_TOO_LARGE` | Multipart upload server limitini aşıyor. | Tek sertifika paketi yükleyin ve 2 MB altında tutun. |
| Rate limit response | Mevcut 10 dakikalık pencerede çok fazla upload denemesi var. | Yeniden denemeden önce bekleyin; tekrar eden hatalar genelde yanlış dosya tipi, boş paket, oversized paket veya yanlış upload client anlamına gelir. |

## Support için önerilen veri

- Public host adı.
- Port.
- Sertifika subject/SAN özeti.
- Son geçerlilik tarihi.
- Tarayıcı hata kodu.

## İlgili

- [Public host ve HTTPS](../../docs/tr/public-host-https-certificate.md)
- [Sunucu ayarları ekranı](../../docs/tr/screen-server-settings.md)
- [Server System ayarları](../../docs/tr/server-system.md)
- [Public screenshot redaction](public-screenshot-redaction.md)
