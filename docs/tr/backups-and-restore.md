# Yedekleme ve Geri Yükleme

VaultPilot yedeği encrypted payload, wrapped key, audit metadata ve integrity manifest içerir. Plaintext secret veya master password içermez.

## Önerilen İş Akışı

1. Güncelleme öncesi yedek alın.
2. Yedeği VaultPilot sunucu diski dışında saklayın.
3. Erişimi sınırlayın; yedek metadata açısından hassastır.
4. Geri yüklemeyi kontrollü ortamda test edin.

## VaultPilot Backup Tool

Backup toplama işlemini Windows sunucuda Administrator olarak çalıştırın. Primary paketlenen executable `VaultPilotBackupTool.exe` adını taşır; `PassManBackupTool.exe` yalnız legacy upgrade/support alias olarak korunur.

Çıktı yolunu kaydedin ve arşivi private tutun. Arşiv encrypted vault data, config ve sertifika materyali içerebilir. Public issue, public support thread veya bu repository içine eklemeyin.

Mevcut konsol, server-backup import panelinden VaultPilot Backup Tool ZIP arşivi veya encrypted JSON export içe aktarabilir. Import, sunucu profilini yedekten yeniden kurar ve açık oturumları kapatır. Bu yüzden yalnız admin recovery aksiyonu olarak, dosya kaynağı ve recovery amacı doğrulandıktan sonra çalıştırılmalıdır.

ZIP içinde Backup Tool database archive varsa VaultPilot, server database'i encrypted local backup şekline çevirmeden önce Backup Tool manifest ister. Raw database dosyaları, WAL/SHM companion dosyaları, müşteri backup'ları ve support arşivleri bu public repoya veya public issue metnine girmez.

Import `PAYLOAD_TOO_LARGE`, `CONTENT_LENGTH_REQUIRED`, `BACKUP_ARCHIVE_INVALID` veya `BACKUP_ARCHIVE_UNSUPPORTED` ile başarısız olursa yeniden denemeden önce [Backup import başarısız veya oturumları kapatıyor](../../kb/tr/backup-import-fails.md) makalesini kullanın.

Uninstall, veri saklama, rollback ve purge sınırları için [Kaldırma, veri saklama ve rollback](uninstall-rollback-data-retention.md) sayfasını kullanın. Normal uninstall, açık private purge onayı yoksa data dizinini korumalıdır.

## Integrity

Encrypted JSON import sırasında SHA-256 integrity manifest ve item count doğrulanır. ZIP archive handling bozuk arşivleri, güvensiz entry name'leri ve desteklenmeyen payload'ları restore öncesi reddeder. Bir değer uyuşmuyorsa veya kaynak net değilse import'u durdurun ve private support kanalını kullanın.
