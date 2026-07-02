# Integration API Client'ları

Onaylı bir sistem VaultPilot public API üzerinden read-only veri okuyacaksa integration API client kullanın. Client'ı dar tutun: yalnız gerekli scope'ları ve kasaları verin, sahibini kaydedin, entegrasyon bittiğinde revoke edin.

## Secrets API Ne Döndürür

`GET /api/public/v1/secrets`, API client'a atanmış kasalar için encrypted snapshot döndürür. Yanıtta vault metadata, encrypted vault name, secret ID, secret type, encrypted payload, timestamp ve `ENCRYPTED_SNAPSHOT` mode bulunur. Plaintext parola veya decrypted vault data dönmez.

`GET /api/public/v1/secrets/{secretId}`, aynı izinli snapshot içinden tek encrypted secret döndürür. ID formatı hatalıysa, client'ın izinli vault listesi dışındaysa veya kayıt yoksa API not found döner.

## Client Oluşturma

1. Owner olarak giriş yapın.
2. Integrations veya API client yüzeyini açın.
3. Net isimli, `SECRETS_READ` scope'lu ve minimum vault listesine sahip client oluşturun.
4. Client secret değerini yalnız bir kez kopyalayın ve tüketen sistemin onaylı secret store'una koyun.
5. Sahip, amaç, izinli vault'lar, scope'lar ve review tarihini kaydedin.

Client secret sunucuda hashlenmiş olarak saklanır. Kaybedilirse yeni client oluşturun ve eskisini revoke edin.

## Authentication

VaultPilot yeni entegrasyonlar için HTTP Basic auth kabul eder. Legacy client'lar için compatibility header'ları da korunur.

```http
Authorization: Basic base64(<CLIENT_ID>:<CLIENT_SECRET>)
```

Compatibility header'ları:

```http
x-passman-client-id: <CLIENT_ID>
x-passman-client-secret: <CLIENT_SECRET>
```

Bu header'ları loglamayın. Gerçek client ID veya secret değerini public issue, ekran görüntüsü, doküman veya support thread içine koymayın.

## Örnek İstek

```powershell
$pair = "<CLIENT_ID>:<CLIENT_SECRET>"
$basic = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($pair))
Invoke-RestMethod -Headers @{ Authorization = "Basic $basic" } -Uri "https://<SERVER_HOST>:1903/api/public/v1/secrets"
```

Public örneklerde placeholder kullanın. Gerçek değerler yalnız tüketen sistemin onaylı secret store'unda kalmalıdır.

## Beklenen Hatalar

| Belirti | Anlamı | Operatör aksiyonu |
| --- | --- | --- |
| 401 veya auth failure | Client ID/secret eksik, formatı hatalı, yanlış veya revoke edilmiş. | Yeni client oluşturup tüketen sistemi güncelleyin, sonra eski client'ı revoke edin. |
| Scope denied | Client'ta `SECRETS_READ` yok. | Amaçlanan scope'u ekleyin veya yeni least-privilege client oluşturun. |
| Boş vault listesi | Secret snapshot erişimi için client'a vault atanmamış. | Yalnız entegrasyonun ihtiyaç duyduğu vault'ları atayın. |
| Secret not found | Secret ID hatalı formatta, silinmiş veya izinli vault dışındadır. | Secret ID'yi izinli snapshot içinden doğrulayın. |

İlgili:

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Bilgi bankası: API client erişimi](../../kb/tr/api-client-401.md)
- [Destek kanıt paketi](support-evidence-pack.md)
