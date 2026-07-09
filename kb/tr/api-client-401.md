# Entegrasyon API client'ı 401 alıyor, kapsam reddediliyor veya boş veri dönüyor

Bir entegrasyon API client'ı `/api/public/v1/secrets`, `/api/public/v1/server/status`, `/api/public/v1/directory/status` veya `/api/public/v1/updates/status` endpoint'ini okuyamıyor, 401 alıyor, kapsam reddi görüyor veya boş şifreli snapshot dönüyorsa bu makaleyi kullanın.

## İlk Kontroller

1. İsteğin doğru endpoint'e gittiğini doğrulayın: `https://<SERVER_HOST>:1903/api/public/v1/...`.
2. Client'ın aktif olduğunu, revoke edilmediğini kontrol edin.
3. Üretilen client ID'nin `pmc_`, üretilen client secret'ın `pms_` ile başladığını doğrulayın.
4. Client kaydında endpoint'in istediği kapsam olduğunu doğrulayın: `SECRETS_READ`, `SERVER_STATUS_READ`, `DIRECTORY_STATUS_READ` veya `UPDATE_STATUS_READ`.
5. Endpoint secret snapshot endpoint'i ise client'a en az bir kasa atandığını doğrulayın.
6. Tüketen sistemin Basic auth veya iki uyumluluk header'ını birlikte gönderdiğini kontrol edin.
7. Tüketen sistemin body içermeyen GET isteği gönderdiğini doğrulayın.
8. Tüketen sistemin authorization header'ını loglamadığını doğrulayın.

Public v1 endpoint'leri yalnız GET ile çalışan okuma yüzeyleridir, `Cache-Control: no-store` döndürür ve dakikada 120 istekle rate-limit edilir. 512 karakterden uzun Basic auth header'ları veya 256 karakterden uzun uyumluluk credential header'ları invalid credential sayılır.

## Hatalar Genelde Ne Anlama Gelir

| Belirti | En olası sebep |
| --- | --- |
| 401 veya auth failure | Client credential eksik, formatı hatalı, yanlış veya revoke edilmiş. |
| Kapsam reddedildi | Client mevcut ama endpoint'in istediği kapsam yok. |
| GET ile body gönderiliyor | Public v1 endpoint'leri read-only çalışır ve request body kabul etmez. |
| Çok fazla istek | Route/client public API rate limit üstünde. |
| Boş `vaults` array | İzinli kasa atanmamış veya atanmış kasa içinde kayıt yok. |
| Gizli veya geçersiz secret ID | ID formatı hatalı, kayıt silinmiş veya client'ın izinli kasaları dışında; endpoint `403 Integration authorization failed.` döndürür. |

## Güvenli Kanıt

Redakte edildikten sonra private support kanalında paylaşılabilir:

- Endpoint path ve timestamp.
- Client görünen adı, secret değil.
- Kapsam listesi ve kasa sayısı.
- Credential içermeyen endpoint path, örnek: `/api/public/v1/server/status`.
- Redakte status code ve error name.

Gerçek client secret, authorization header, vault payload, database, credential içeren log veya secret görünen ekran görüntüsü göndermeyin.

İlgili:

- [Entegrasyon API client'ları](../../docs/tr/api-clients.md)
- [Public API referansı](../../docs/tr/public-api-reference.md)
- [Destek kanıt paketi](../../docs/tr/support-evidence-pack.md)
