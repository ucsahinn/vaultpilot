# Entegrasyon API Client'ları

Onaylı bir sistem VaultPilot public API üzerinden sadece okuma amaçlı veri alacaksa entegrasyon API client'ı kullanın. Client'ı dar tutun: yalnız gerekli endpoint kapsamlarını ve gerekiyorsa gerekli kasaları verin, sahibini kaydedin, entegrasyon bittiğinde erişimini iptal edin.

## Public API Yüzeyi

Endpoint, credential formatı, cache ve status-code sözleşmesi için bu operatör rehberinin yanında [Public API referansı](public-api-reference.md) sayfasını açık tutun.

`GET /api/public/v1/secrets`, API client'a atanmış kasalar için şifreli snapshot döndürür. Yanıtta vault metadata, encrypted vault name, secret ID, secret type, encrypted payload, timestamp ve `ENCRYPTED_SNAPSHOT` mode bulunur. Plaintext parola veya decrypted vault data dönmez.

`GET /api/public/v1/secrets/{secretId}`, aynı izinli snapshot içinden tek şifreli secret döndürür. ID formatı hatalıysa, kayıt yoksa, silinmişse veya client'ın izinli vault listesi dışındaysa VaultPilot bilerek `403 Integration authorization failed.` döndürür; yetkisiz client'lar gizli kayıt ile hatalı ID'yi ayırt edemez.

Aynı client modeli sadece okuma yapan operasyon status endpoint'lerini de destekler. Bu endpoint'ler kasa datasını decrypt etmez ve client'ta `SECRETS_READ` yoksa vault assignment gerektirmez.

| Scope | Endpoint | Dönen bilgi |
| --- | --- | --- |
| `SECRETS_READ` | `GET /api/public/v1/secrets` ve `GET /api/public/v1/secrets/{secretId}` | Atanmış kasalar için şifreli vault ve secret snapshot. |
| `SERVER_STATUS_READ` | `GET /api/public/v1/server/status` | App version, uptime, vault count, active API client count ve directory provider count. |
| `DIRECTORY_STATUS_READ` | `GET /api/public/v1/directory/status` | Directory provider health, obje sayıları, seçili login/credential sayıları ve last seen/sync zamanları. |
| `UPDATE_STATUS_READ` | `GET /api/public/v1/updates/status` | Konsolda görülen Update Center status bilgisinin read-only monitoring çıktısı. |

## Client Oluşturma

1. Owner olarak giriş yapın.
2. Integrations veya API client yüzeyini açın.
3. Tüketen sistemin gerçekten ihtiyaç duyduğu endpoint kapsamlarını seçin.
4. `SECRETS_READ` seçildiyse minimum vault listesini atayın. Status-only client için vault scope gerekmez.
5. Client'ı net bir isimle oluşturun.
6. Client secret değerini yalnız bir kez kopyalayın ve tüketen sistemin onaylı secret store'una koyun.
7. Sahip, amaç, izinli vault'lar, kapsamlar ve review tarihini kaydedin.

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

Status-only örnek:

```powershell
$pair = "<CLIENT_ID>:<CLIENT_SECRET>"
$basic = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($pair))
Invoke-RestMethod -Headers @{ Authorization = "Basic $basic" } -Uri "https://<SERVER_HOST>:1903/api/public/v1/server/status"
```

Public örneklerde yer tutucu kullanın. Gerçek değerler yalnız tüketen sistemin onaylı secret store'unda kalmalıdır.

Gerçek `$pair` veya `$basic` içeren komutları yalnız private operator shell içinde çalıştırın. Bu değerleri public issue, ekran görüntüsü, transcript veya dokümana yapıştırmayın.

## Beklenen Hatalar

| Belirti | Anlamı | Operatör aksiyonu |
| --- | --- | --- |
| 401 veya auth failure | Client ID/secret eksik, formatı hatalı, yanlış veya revoke edilmiş. | Yeni client oluşturup tüketen sistemi güncelleyin, sonra eski client'ı revoke edin. |
| Kapsam reddedildi | Client kaydında endpoint'in istediği kapsam yok. | Amaçlanan kapsamı ekleyin veya yalnız gereken yetkiye sahip yeni bir client oluşturun. |
| Boş vault listesi | Secret snapshot erişimi için client'a vault atanmamış. Bu yalnız `SECRETS_READ` için önemlidir. | Yalnız entegrasyonun ihtiyaç duyduğu vault'ları atayın veya status-only client'tan `SECRETS_READ` kapsamını kaldırın. |
| Gizli veya geçersiz secret ID | Secret ID hatalı formatta, silinmiş veya client'ın izinli vault'ları dışındadır; VaultPilot `403 Integration authorization failed.` döndürür. | ID'yi izinli encrypted snapshot içinden doğrulayın, sonra `SECRETS_READ`, vault assignment ve client kapsamını kontrol edin. |

İlgili:

- [Public API referansı](public-api-reference.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Bilgi bankası: API client erişimi](../../kb/tr/api-client-401.md)
- [Destek kanıt paketi](support-evidence-pack.md)
