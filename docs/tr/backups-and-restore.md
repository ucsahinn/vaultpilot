# Yedekleme ve Geri Yükleme

VaultPilot yedeği encrypted payload, wrapped key, audit metadata ve integrity manifest içerir. Plaintext secret veya master password içermez.

## Önerilen İş Akışı

1. Güncelleme öncesi yedek alın.
2. Yedeği VaultPilot sunucu diski dışında saklayın.
3. Erişimi sınırlayın; yedek metadata açısından hassastır.
4. Geri yüklemeyi kontrollü ortamda test edin.

## VaultPilot Backup Tool

Backup toplama işlemini Windows sunucuda Administrator olarak çalıştırın. Paketlenen executable şu anda `PassManBackupTool.exe` adını taşır, ancak 2.0 hattında araç kendini VaultPilot Backup Tool olarak tanıtır.

Çıktı yolunu kaydedin ve arşivi private tutun. Arşiv encrypted vault data, config ve sertifika materyali içerebilir. Public issue, public support thread veya bu repository içine eklemeyin.

Restore ve import admin/support prosedürü olarak kalır. Tam desteklenen restore yolu release-verified olmadan public restore komutu dokümante etmeyin veya çalıştırmayın.

Uninstall, veri saklama, rollback ve purge sınırları için [Kaldırma, veri saklama ve rollback](uninstall-rollback-data-retention.md) sayfasını kullanın. Normal uninstall, açık private purge onayı yoksa data dizinini korumalıdır.

## Integrity

Import sırasında SHA-256 integrity manifest ve item count doğrulanır. Uyuşmazlık varsa import durdurulmalıdır.
