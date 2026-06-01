# PassMan Genel Bakış

PassMan Enterprise Vault Console, Windows Server üzerine MSI ile kurulan self-hosted ve zero-knowledge bir kurumsal kasa konsoludur. Kullanıcılar PassMan'a sunucu IP adresi veya DNS adı üzerinden tarayıcıyla erişir. İlk profil oluşturma ve kasa kilidi açma için HTTPS veya `localhost` gerekir; düz HTTP sunucu IP erişimi HTTPS yapılandırılana kadar yalnızca erişilebilirlik kontrolüdür.

## Temel İlkeler

- Ana parola sunucuya gönderilmez.
- Kasa anahtarları tarayıcı oturumunda RAM içinde çözülür.
- Secret payload'ları sunucuya gitmeden önce tarayıcıda şifrelenir.
- Sunucu yerel SQLite veritabanında ciphertext, sarmalanmış anahtarlar ve metadata tutar.
- Güncelleme paketi, imzalı manifest ve SHA-256 doğrulamasıyla kontrol edilir.

## Bileşenler

| Bileşen | Açıklama |
| --- | --- |
| PassMan Server | Windows servisi olarak çalışan ana uygulama. |
| Chromium Extension | Eşleşmiş cihazlarda autofill, save/update login ve site badge deneyimi sağlar. |
| Offline Share Decrypter | Dış paylaşım paketlerini tamamen tarayıcı içinde açar. |
| PassMan DC Agent Service | Active Directory objelerini PassMan'a güvenli şekilde senkronlar. |

## İlk Okunacaklar

- [Windows Server kurulumu](install-windows-server.md)
- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Public host, HTTPS ve sertifika](public-host-https-certificate.md)
- [Güncelleme merkezi](update-center.md)
- [Sorun giderme](troubleshooting.md)
