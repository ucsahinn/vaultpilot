# Integration API client 401, scope denied veya boş veri dönüyor

Bir integration API client `/api/public/v1/secrets`, `/api/public/v1/server/status`, `/api/public/v1/directory/status` veya `/api/public/v1/updates/status` endpoint'ini okuyamıyor, 401 alıyor, scope denied görüyor veya boş encrypted snapshot dönüyorsa bu makaleyi kullanın.

## İlk Kontroller

1. İsteğin doğru endpoint'e gittiğini doğrulayın: `https://<SERVER_HOST>:1903/api/public/v1/...`.
2. Client'ın active olduğunu, revoke edilmediğini kontrol edin.
3. Client'ta endpoint'in istediği scope olduğunu doğrulayın: `SECRETS_READ`, `SERVER_STATUS_READ`, `DIRECTORY_STATUS_READ` veya `UPDATE_STATUS_READ`.
4. Endpoint secret snapshot endpoint'i ise client'a en az bir vault atandığını doğrulayın.
5. Tüketen sistemin Basic auth veya iki compatibility header'ını birlikte gönderdiğini kontrol edin.
6. Tüketen sistemin authorization header'ını loglamadığını doğrulayın.

## Hatalar Genelde Ne Anlama Gelir

| Belirti | En olası sebep |
| --- | --- |
| 401 veya auth failure | Client credential eksik, formatı hatalı, yanlış veya revoke edilmiş. |
| Scope denied | Client var ama endpoint'in istediği scope yok. |
| Boş `vaults` array | İzinli vault atanmamış veya atanmış vault içinde kayıt yok. |
| Secret endpoint not found diyor | ID formatı hatalı, kayıt silinmiş veya client'ın izinli vault'ları dışında. |

## Güvenli Kanıt

Redakte edildikten sonra private support kanalında paylaşılabilir:

- Endpoint path ve timestamp.
- Client display name, secret değil.
- Scope listesi ve vault sayısı.
- Credential içermeyen endpoint path, örnek: `/api/public/v1/server/status`.
- Redakte status code ve error name.

Gerçek client secret, authorization header, vault payload, database, credential içeren log veya secret görünen screenshot göndermeyin.

İlgili:

- [Integration API client'ları](../../docs/tr/api-clients.md)
- [Destek kanıt paketi](../../docs/tr/support-evidence-pack.md)
