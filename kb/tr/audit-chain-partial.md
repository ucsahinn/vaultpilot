# Denetim zinciri kısmi veya tutarsız

Audit Log ekranı kısmi zincir, tutarsız hash sırası, restore sonrası eksik satır veya filtrelerle açıklanamayan zincir uyarısı gösteriyorsa bu makaleyi kullanın. Olay onaylı restore, backup import, update, retention policy veya maintenance işiyle açıklanana kadar güvenlik açısından önemli kabul edilmelidir.

## İlk Müdahale

1. Workspace içinden [Denetim kaydı](../../docs/tr/screen-audit-log.md) ekranını açın ve üst bardaki `?` ile güncel prosedürü kontrol edin.
2. Hiçbir şeyi değiştirmeden önce aktif filtreleri, tarih aralığını ve görünen chain durumunu not edin.
3. İlk tutarsız event'i ve ondan önceki son sağlam event'i bulun.
4. Aynı zaman aralığında restore, backup import, update, retention cleanup veya maintenance job çalışıp çalışmadığını kontrol edin.
5. Zincir kırık görünüyorsa ve bunu açıklayan onaylı bakım olayı yoksa kritik olmayan yazma işlemlerini durdurun.

## Neyi Kontrol Etmeli

| Alan | Kontrol | Beklenen sonuç |
| --- | --- | --- |
| Filtreler | User, category, tarih ve severity filtreleri | Filtre kaynaklı kısmi görünüm ile bozuk chain ayrılabiliyor. |
| Bakım işleri | Backup import, restore, update ve retention olayları | Chain geçişinin karşılığı olan admin olayı var. |
| Depolama | Servis restart, disk doluluğu, database replacement veya manuel copy | VaultPilot prosedürü dışında database taşınmamış. |
| Kanıt | Son sağlam export veya backup metadata | Operatör secret payload göstermeden ne değiştiğini açıklayabiliyor. |

## Güvenli Kanıt

- VaultPilot server versiyonu ve yaklaşık olay zamanı.
- İlk uyarı çevresindeki redakte filtre seti, event id ve event kategorileri.
- Restore, import, update, retention cleanup veya maintenance çalışıp çalışmadığı.
- Raw database satırı değil, chain status metni ve sayı özeti.
- Gerekliyse Windows servis restart zamanları.

## Private Eskalasyon

Filtre incelemesine rağmen uyarı sürüyorsa, ilk tutarsız satır onaylı bakım işiyle eşleşmiyorsa veya aynı aralıkta birden fazla admin aktifse private support kanalına taşıyın. Chain durumu anlaşılmadan normal rotation, sharing veya user-administration işlerine devam etmeyin.

## Göndermeyin

Public support kanalına database dosyası, backup, secret payload, ana parola, credential içeren raw log, vault kaydı görünen screenshot veya müşteri/kullanıcı kimliği göndermeyin.

İlgili: [Denetim kaydı ekranı](../../docs/tr/screen-audit-log.md), [Operatör runbook](../../docs/tr/operator-runbook.md), [Support evidence pack](../../docs/tr/support-evidence-pack.md), [Public issue redaction](public-issue-redaction.md).
