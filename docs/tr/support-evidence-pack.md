# Destek Kanıt Paketi

Bu kontrol listesi, destek ekibine temiz ve herkese açık paylaşım için güvenli bir vaka aktarımı hazırlamak için kullanılır. Amaç, vakayı teknik olarak faydalı hale getirirken secret veya müşteri ortamı sızdırmamaktır.

## Zorunlu Vaka Başlığı

| Alan | Örnek format |
| --- | --- |
| VaultPilot sürümü | `2.0.0` veya konsolda görünen kesin yayınlı sürüm. |
| Yüzey | Login, installer, update, extension, AD sync, sharing, backup, license, HTTPS veya audit. |
| Ortam | Windows Server sürümü ve tarayıcı ailesi. |
| Etki | Tek kullanıcı, tüm kullanıcılar, tek kasa, tek eklenti cihazı, tek AD sağlayıcısı veya tek update job. |
| Son sağlıklı durum | Biliniyorsa tarih/saat ve önceki sürüm. |
| Mevcut engel | Kullanıcının gördüğü hatayı tek cümleyle anlat. |

## Yüzeye Göre Kanıt

| Yüzey | Topla | Toplama |
| --- | --- | --- |
| Installer | MSI dosya adı, imza durumu, servis durumu, redakte edilmiş installer hatası. | Redakte edilmemiş müşteri yolu veya credential içeren MSI logları. |
| Login | Tarayıcı ailesi, oturum durumu, `/api/auth/me` status değeri, redakte edilmiş zaman damgası. | Ana parola, TOTP secret, kurtarma materyali. |
| Update | Manifest sürümü, hash, signer durumu, update job durumu. | İmzalama private key'i veya internal download credential. |
| Extension | Eklenti sürümü, eşleştirme durumu, cihaz satırı durumu, tarayıcı profil modu. | Plaintext credential veya extension PIN. |
| AD sync | Servis durumu, redakte edilmiş agent logu, sağlayıcı sağlığı. | AD bind parolası, agent token, tam directory dump. |
| Sharing | Paket süre sonu, maksimum açma sayısı, decrypter hata adı. | Share passphrase, plaintext package içeriği. |
| Backup | Export/import durumu ve bütünlük sonucu. | Private kanal açıkça istemedikçe backup dosyasının kendisi. |

## Redaksiyon Kuralları

Gerçek değerleri yer tutucu ile değiştir:

- `<VAULTPILOT_URL>`
- `<SERVER_HOST>`
- `<USER>`
- `<VAULT>`
- `<AGENT_ID>`
- `<AGENT_TOKEN>`
- `<LICENSE_CODE>`
- `<REDACTED>`

## Eskalasyon Kalite Eşiği

İyi bir vaka şunları içerir:

- Tek net belirti.
- Etkilenen yüzey.
- Sürüm ve bileşen sürümleri.
- Kısa zaman çizelgesi.
- Eşleşen KB makalesinden redakte edilmiş kanıt.
- Hata öncesi değişiklik.
- Backup, login ve audit hâlâ erişilebilir mi bilgisi.

İlgili sayfalar:

- [Bilgi bankası](../../kb/tr/README.md)
- [Sorun giderme](troubleshooting.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
