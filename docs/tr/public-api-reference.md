# Public API Referansı

VaultPilot public entegrasyon API client'ları onaylı sistemler için sadece okuma amaçlı kimliklerdir. Yalnızca şifreli kasa snapshot'ları ve operasyonel status metadata'sı sunar. Public API plaintext parola, master password, decrypted vault payload veya private server materyali döndürmez.

Client'lar Owner-only Integrations/API client yüzeyinden oluşturulur. Her client `pmc_[A-Za-z0-9_-]{24}` formatında üretilen bir client ID ve yalnız bir kez görünen `pms_[A-Za-z0-9_-]{43}` formatında client secret alır. Secret sunucuda keyed digest olarak saklanır; kaybolursa yeni client oluşturup eskisini revoke edin.

Public v1 endpoint'leri GET-only read yüzeylerdir. Request body göndermeyin. Body içeren istekler route integration credential'larını okumadan önce reddedilir.

## Authentication

Yeni entegrasyonlar için HTTP Basic auth tercih edin:

```http
Authorization: Basic base64(<CLIENT_ID>:<CLIENT_SECRET>)
```

Eski client'lar için compatibility header'ları korunur:

```http
x-passman-client-id: <CLIENT_ID>
x-passman-client-secret: <CLIENT_SECRET>
```

Bu header'ları loglamayın. Gerçek client ID, client secret, encrypted payload, vault ID veya secret ID değerlerini public issue, ekran görüntüsü, doküman veya support thread içine koymayın.

Formatı hatalı credential'lar database lookup öncesi reddedilir. Basic auth header'ları 512 karakterle; compatibility credential header'ları ise her biri 256 karakterle sınırlıdır.

## Kapsamlar Ve Endpoint'ler

| Kapsam | Endpoint | Yanıt |
| --- | --- | --- |
| `SECRETS_READ` | `GET /api/public/v1/secrets` | API client'a atanmış kasalar için encrypted vault ve secret snapshot. |
| `SECRETS_READ` | `GET /api/public/v1/secrets/{secretId}` | Atanmış kasa snapshot'ından tek encrypted secret. Route ID değeri UUID olmalıdır. |
| `SERVER_STATUS_READ` | `GET /api/public/v1/server/status` | App version, uptime, vault count, active API client count ve directory provider count. |
| `DIRECTORY_STATUS_READ` | `GET /api/public/v1/directory/status` | Directory provider health, obje sayıları, seçili login ve credential sayıları, last-seen timestamp'leri ve sync timestamp'leri. |
| `UPDATE_STATUS_READ` | `GET /api/public/v1/updates/status` | Read-only monitoring için Update Center status bilgisi. |

`SECRETS_READ` en az bir atanmış vault gerektirir. Status-only client'lar vault assignment olmadan oluşturulabilir.

## İstek Örnekleri

PowerShell Basic auth örneği:

```powershell
$pair = "<CLIENT_ID>:<CLIENT_SECRET>"
$basic = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($pair))
Invoke-RestMethod -Headers @{ Authorization = "Basic $basic" } -Uri "https://<SERVER_HOST>:1903/api/public/v1/server/status"
```

Compatibility-header örneği:

```powershell
Invoke-RestMethod `
  -Headers @{
    "x-passman-client-id" = "<CLIENT_ID>"
    "x-passman-client-secret" = "<CLIENT_SECRET>"
  } `
  -Uri "https://<SERVER_HOST>:1903/api/public/v1/secrets"
```

Public örneklerde yer tutucu kullanın. Gerçek değerler yalnızca tüketen sistemin onaylı secret store'unda kalmalıdır.

Gerçek `$pair` veya `$basic` içeren komutları yalnız private operator shell içinde çalıştırın. Bu değerleri public issue, ekran görüntüsü, transcript veya dokümana yapıştırmayın.

## Yanıt Şekli

Secret snapshot yanıtları decrypted kayıt değil, şifreli data paketidir:

```json
{
  "mode": "ENCRYPTED_SNAPSHOT",
  "vaults": [
    {
      "id": "<VAULT_ID>",
      "nameEncrypted": "<ENCRYPTED_VAULT_NAME>",
      "secrets": [
        {
          "id": "<SECRET_ID>",
          "type": "LOGIN",
          "payloadEncrypted": "<ENCRYPTED_PAYLOAD>",
          "updatedAt": "<ISO_TIMESTAMP>"
        }
      ]
    }
  ]
}
```

Status endpoint'leri yalnız operasyonel metadata döndürür. Kasa içeriğini decrypt etmez.

## Status ve Hata Sözleşmesi

Public API yanıtları `Cache-Control: no-store` içerir; böylece API snapshot'ları browser veya aracı katmanlarda cache'lenmez. Public v1 route'ları dynamic read endpoint'tir ve dakikada 120 request ile rate-limit edilir.

| Status | Anlamı | Operatör aksiyonu |
| --- | --- | --- |
| `200` | Client istenen read-only endpoint için authenticated ve authorized durumda. | Encrypted snapshot veya status metadata'sını tüketin. |
| `401` | Client ID veya secret eksik, formatı hatalı, yanlış ya da revoke edilmiş. | Yeni client oluşturun, tüketen sistemi güncelleyin ve eski client'ı revoke edin. |
| `403` | Client kaydında gerekli kapsam, vault assignment veya secret yetkisi yok. | Kapsamı, vault assignment değerini ve hedef endpoint'i doğrulayın. Hatalı formatta, silinmiş veya izinli vault listesi dışındaki secret lookup'ları `403 Integration authorization failed.` döndürür. |

İlgili:

- [Entegrasyon API client'ları](api-clients.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Bilgi bankası: API client erişimi](../../kb/tr/api-client-401.md)
