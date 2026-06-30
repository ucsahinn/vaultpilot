# Public Host, HTTPS ve Sertifikalar

VaultPilot public tarayıcı erişimi yapılandırılan public port üzerinde HTTPS kullanır. Kurulu server ilk erişim için managed self-signed HTTPS sertifikası üretebilir; operatörler geniş üretim kullanımı öncesinde bunu trusted PFX/P12 paketiyle değiştirmelidir. Düz HTTP yalnızca internal upstream veya local development konusudur, public operatör giriş yolu değildir.

## Operatörün Girdiği Alanlar

| Alan | Zorunlu | Amaç |
| --- | --- | --- |
| Public host | Evet | Kullanıcıların tarayıcıda açacağı DNS adı veya server host'u. |
| Public port | Evet | Varsayılan public HTTPS portu `1903`; onaylı gelen portu kullanın. |
| HTTPS sertifika paketi | Üretim için önerilir | Sertifika ve private key içeren PFX/P12 paketi. Bu yapılandırılana kadar VaultPilot managed self-signed sertifika ile başlayabilir. |
| Sertifika parolası | Paket parola korumalıysa zorunlu | Server'ın paketi yüklemesi için kullanılır. |

VaultPilot ayrı bir "sertifika kaynağı" seçimi istemez. Operatör doğrudan sertifika dosyasını seçer.

## Desteklenen Sertifika Paketi

Tek paket kullanılır:

```text
PFX / P12
```

Sertifika, kullanıcıların tarayıcıda açtığı host ile eşleşmelidir. Subject veya SAN içinde yapılandırılan host adı bulunmalıdır.

## Üretim Kontrol Listesi

1. İlk erişimi `https://<SERVER_HOST>:1903` veya yapılandırdığınız public HTTPS portu üzerinden doğrulayın.
2. Managed self-signed sertifika aktifken tarayıcı uyarısı bekleyin.
3. Trusted sertifika paketini VaultPilot dışında oluşturun veya temin edin.
4. Host adının VaultPilot sunucusuna çözümlendiğini doğrulayın.
5. Sunucu sistemi ekranında public host ve port değerlerini girin.
6. PFX/P12 paketini yükleyin.
7. Gerekiyorsa paket parolasını girin.
8. HTTPS yapılandırmasını kaydedin.
9. UI isterse servisi yeniden başlatın veya VaultPilot'ın yeniden yüklemesini bekleyin.
10. Şu adresi açın:

```text
https://<HOST>:<PORT>
```

## Güvenlik Notları

- PFX/P12 dosyalarını, private key'leri veya sertifika parolalarını bu public repoya yüklemeyin.
- Sertifika paketlerini sunucuda kısıtlı ACL ile saklayın.
- Tarayıcı uyarıları başlamadan önce süresi dolan sertifikaları değiştirin.
- Private network için internal PKI, internet-facing DNS için trusted public certificate kullanın.

## Sorun Giderme

| Belirti | Kontrol |
| --- | --- |
| Tarayıcı hostname uyarısı veriyor | Sertifika SAN değeri `<HOST>` ile eşleşmiyor. |
| HTTPS başlamıyor | PFX/P12 parolası yanlış veya paket okunamıyor. |
| İlk erişimde uyarı görünüyor | Managed self-signed HTTPS hâlâ aktif; trusted PFX/P12 paketi kurun veya iç politika gereği issuing CA'yı güvenilir yapın. |
| Lokalde çalışıyor, uzaktan çalışmıyor | DNS, firewall veya reverse proxy yolu host/port ile hizalı değil. |
| Sertifika yalnızca sunucuda kabul ediliyor | İstemci cihazlar sertifikayı veren CA'ya güvenmiyor. |
