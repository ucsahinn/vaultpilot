# VaultPilot Genel Bakış

VaultPilot Enterprise Vault Console, Windows Server üzerine MSI ile kurulan self-hosted ve zero-knowledge bir kurumsal kasa konsoludur. Kullanıcılar VaultPilot'a sunucu IP adresi veya DNS adı üzerinden HTTPS ile erişir. İlk profil oluşturma ve kasa kilidi açma tarayıcı Web Crypto desteği ister; kurulu server trusted PFX/P12 sertifika yapılandırılana kadar managed self-signed HTTPS sunar.

## Temel İlkeler

- Ana parola sunucuya gönderilmez.
- Kasa anahtarları tarayıcı oturumunda RAM içinde çözülür.
- Secret payload'ları sunucuya gitmeden önce tarayıcıda şifrelenir.
- Sunucu yerel SQLite veritabanında ciphertext, sarmalanmış anahtarlar ve metadata tutar.
- Güncelleme paketi, imzalı manifest ve SHA-256 doğrulamasıyla kontrol edilir.

## Bileşenler

| Bileşen | Açıklama |
| --- | --- |
| VaultPilot Server | Windows servisi olarak çalışan ana uygulama. |
| Chromium Extension | Eşleşmiş cihazlarda autofill, save/update login ve site badge deneyimi sağlar. |
| Offline Share Decrypter | Dış paylaşım paketlerini tamamen tarayıcı içinde açar. |
| VaultPilot DC Agent Service | Active Directory objelerini VaultPilot'a güvenli şekilde senkronlar. |

## İlk Okunacaklar

- [Windows Server kurulumu](install-windows-server.md)
- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Public host, HTTPS ve sertifika](public-host-https-certificate.md)
- [Güncelleme merkezi](update-center.md)
- [Sorun giderme](troubleshooting.md)

## Uygulama İçi Dokümantasyon Butonu

VaultPilot 2.0 topbar alanına soru işareti ikonlu bir yardım butonu ekler. Bu buton, açık olan ekranla eşleşen GitHub dokümantasyon sayfasını açar. Konsol dili İngilizce ise `docs/en/...`, Türkçe ise `docs/tr/...` hedeflenir.
