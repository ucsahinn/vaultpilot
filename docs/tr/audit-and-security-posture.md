# Denetim ve Güvenlik Duruşu

VaultPilot Genel Bakış ekranı sistem sağlığı, güvenlik skoru ve aksiyon gereken riskleri gösterir.

## Skor Sinyalleri

- 2FA durumu.
- Denetim zinciri doğrulaması.
- Lisans sağlığı.
- Extension eşleşme durumu.
- Update ve paket sağlığı.

## Audit Chain

Audit olayları zincirlenmiş hash alanlarıyla takip edilir. Zincir kısmi veya tutarsız görünüyorsa ilgili olaylar gelişmiş filtreyle incelenmelidir.

## Önerilen Aksiyonlar

- Owner/Admin hesaplarında 2FA'yı etkinleştirin.
- Kısmi veya kırık audit zincirini inceleyin.
- Eski extension cihazlarını revoke edin.
- Güncelleme manifest ve MSI imza durumunu kontrol edin.

## Kurtarma İpuçları

Skor lisans süresi, başarısız update, kısmi audit-chain kontrolü veya kayıp 2FA cihazı yüzünden düşerse kanıtı redakte edin ve kayıt değiştirmeden önce ilgili kurtarma rehberini izleyin.

## İlgili

- [Security Command Center ekranı](screen-security-command-center.md)
- [Güvenlik dashboard ekranı](screen-security-dashboard.md)
- [Giriş güvenliği ekranı](screen-sign-in-security.md)
- [Audit chain partial bilgi bankası](../../kb/tr/audit-chain-partial.md)
- [License read-only bilgi bankası](../../kb/tr/license-read-only.md)
