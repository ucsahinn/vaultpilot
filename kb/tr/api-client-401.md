# Integration API client 401 alıyor veya secret göremiyor

Bir integration API client `/api/public/v1/secrets` okuyamıyor, 401 alıyor, scope denied görüyor veya boş encrypted snapshot dönüyorsa bu makaleyi kullanın.

## İlk Kontroller

1. İsteğin `https://<SERVER_HOST>:1903/api/public/v1/secrets` adresine gittiğini doğrulayın.
2. Client'ın active olduğunu, revoke edilmediğini kontrol edin.
3. Client'ta `SECRETS_READ` scope'u olduğunu doğrulayın.
4. Client'a en az bir vault atandığını doğrulayın.
5. Tüketen sistemin Basic auth veya iki compatibility header'ını birlikte gönderdiğini kontrol edin.
6. Tüketen sistemin authorization header'ını loglamadığını doğrulayın.

## Hatalar Genelde Ne Anlama Gelir

| Belirti | En olası sebep |
| --- | --- |
| 401 veya auth failure | Client credential eksik, formatı hatalı, yanlış veya revoke edilmiş. |
| Scope denied | Client var ama `SECRETS_READ` scope'u yok. |
| Boş `vaults` array | İzinli vault atanmamış veya atanmış vault içinde kayıt yok. |
| Secret endpoint not found diyor | ID formatı hatalı, kayıt silinmiş veya client'ın izinli vault'ları dışında. |

## Güvenli Kanıt

Redakte edildikten sonra private support kanalında paylaşılabilir:

- Endpoint path ve timestamp.
- Client display name, secret değil.
- Scope listesi ve vault sayısı.
- Redakte status code ve error name.

Gerçek client secret, authorization header, vault payload, database, credential içeren log veya secret görünen screenshot göndermeyin.

İlgili:

- [Integration API client'ları](../../docs/tr/api-clients.md)
- [Destek kanıt paketi](../../docs/tr/support-evidence-pack.md)
