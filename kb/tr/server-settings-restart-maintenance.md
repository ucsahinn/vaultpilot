# Server Settings Restart Veya Bakım İncelemesi İstiyor

Server System ayarları kaydedildiği halde tarayıcı erişimi, HTTPS, bildirimler, loglar veya servis restart durumu hâlâ incelenmeliyse bu makaleyi kullanın.

## İlk Kontroller

| Kontrol | Sağlıklı sonuç |
| --- | --- |
| Erişim URL'si | Operatörler tek canonical `https://<SERVER_HOST>:<PORT>` URL'sini kullanır. |
| Servis durumu | `VaultPilotServer` çalışır; upgraded host'larda legacy `PassManServer` compatibility kanıtı da görülebilir. |
| HTTPS durumu | Sertifika subject/SAN değeri kullanıcıların tarayıcıda açtığı host ile eşleşir. |
| Bildirim testi | Test e-postası success döner veya secret içermeyen provider hatası verir. |
| Bakım durumu | Retention değerleri görünür; cleanup Owner-only, backup-first ve normal operasyon için zorunlu değildir. |

## Yaygın Nedenler

- Host veya port değişmiştir, fakat DNS, firewall veya client bookmark hâlâ eski route'a gider.
- Sertifika paketi kaydedilmiştir, fakat tarayıcı SAN içinde olmayan bir hostname açıyordur.
- SMTP credential veya relay policy VaultPilot dışında değişmiştir.
- Yapılandırma değişikliği UI'ın istediği service restart'ı bekliyordur.
- Operatör bakımın geniş data purge etmesini bekliyordur, fakat VaultPilot cleanup yalnız `AUDIT`, `DISCOVERY` veya `EXECUTIONS` kayıtlarıyla sınırlıdır ve backup-clear mode gerektirir.

## Maintenance Cleanup Sınırı

Maintenance cleanup yalnız Owner tarafından çalıştırılır. Rutin troubleshooting değildir; sadece private support veya retention kararı açıkça gerektiriyorsa kullanılmalıdır.

VaultPilot cleanup'ı yalnız backup-clear mode ile kabul eder. Düz clear isteği `MAINTENANCE_BACKUP_REQUIRED` ile reddedilir. Seçilen kategori temizlenmeden önce VaultPilot `vaultpilot-maintenance-<scope>-<timestamp>-<id>.json` adlı maintenance backup dosyası yazar.

Restore yalnız o backup içindeki kategoriyi etkiler. Backup sonrasında oluşan kayıtlar restore sırasında değişebilir veya kaybolabilir; restore uyarısı `RESTORE_REPLACES_NEWER_CATEGORY_RECORDS` değeridir. Cleanup ve restore vault secret'larını, source file'ları, service loglarını, database'i, backup dosyalarını, sertifikaları veya müşteri datasını hedeflemez.

## Toplanacak Güvenli Kanıt

- VaultPilot version ve kurulu servis adı.
- Gerçek host yerine `<SERVER_HOST>` kullanılan host biçimi.
- Yapılandırılmış port ve kayıttan sonra servisin restart edilip edilmediği.
- Sertifika subject/SAN özeti ve son geçerlilik tarihi.
- Bildirim test zamanı ve secret içermeyen hata adı.
- Log retention ve audit retention değerleri.
- Cleanup açıkça onaylandıysa maintenance cleanup scope'u, backup dosya adı ve redakte digest bilgisi.

Sertifika dosyası, private key, sertifika parolası, SMTP secret, cookie, API token, secret içerebilecek ham log, database, yedek veya maintenance backup JSON dosyasını public kanallardan göndermeyin.

## Çözüm Yolu

1. VaultPilot'ı tek canonical URL üzerinden yeniden açın.
2. Windows servisinin çalıştığını doğrulayın.
3. DNS ve firewall yönünün yapılandırılan host ve porta ulaştığını doğrulayın.
4. HTTPS değiştiyse yalnızca UI isterse restart yapın, sonra bir client tarayıcıdan test edin.
5. Bildirim testi başarısızsa relay host, port, TLS modu ve sender policy değerlerini mail administrator ile doğrulayın.
6. Maintenance cleanup açıkça onaylandıysa scope'un `AUDIT`, `DISCOVERY` veya `EXECUTIONS` olduğunu, backup-clear mode kullanıldığını ve maintenance backup JSON dosyasının private saklandığını doğrulayın.
7. Sorun devam ederse güvenli kanıt paketini private support kanalıyla gönderin.

İlgili:

- [Server System ayarları](../../docs/tr/server-system.md)
- [Public host ve HTTPS](../../docs/tr/public-host-https-certificate.md)
- [HTTPS sertifika uyarısı](certificate-warning.md)
- [Destek kanıt paketi](../../docs/tr/support-evidence-pack.md)
