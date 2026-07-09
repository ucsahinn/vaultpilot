# İşlemler Ekranı

Üst çubuktaki `?` bu sayfayı İşlemler ekranından açar. Update, Discovery run, bakım operasyonu ve arka plan görevi gibi aktif işleri izlemek için kullanın.

## Burada Ne Yapılır

- İşi yeniden denemeden önce mevcut durum değerini kontrol edin.
- Private support için hata adı, timestamp ve bileşen adı bilgisini koruyun.
- Görev zaten çalışıyorsa tekrarlı manuel yeniden deneme yapmayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Running | Çalışan işi bekleyin veya onaylı akışla iptal edin. |
| Failed | Yeniden deneme öncesi hata adı, bileşen ve timestamp bilgisini koruyun. |
| Stale | Manuel müdahale öncesi servis sağlığını ve ilgili iş ekranını kontrol edin. |

## İşlemden Önce

- Yeni iş başlatmadan önce mevcut job'ın hâlâ ilerleyip ilerlemediğini kontrol edin.
- Support için job ID, component, başlangıç zamanı ve son log özetini kaydedin.
- Update, discovery veya maintenance incident incelemesi sürerken job evidence silmeyin.

## Güvenli Kanıt

- Paylaşılabilir: job ID yer tutucusu, bileşen adı, durum, timestamp aralığı ve redakte hata kategorisi.
- Gizli kalmalı: local path, hostname, paket indirme konumu, ham log, müşteri dosya adı ve makineye özel trace.
- Update, discovery veya maintenance işi hâlâ inceleniyorsa job kanıtını private olarak koruyun.

## Operatör Notları

İş ayrıntıları local path, host, dosya adı veya paket durumu içerebilir. Public paylaşmadan önce redakte edin.

## İlgili

- [Operasyon runbook](operator-runbook.md)
- [Güncelleme Merkezi](update-center.md)
- [Discovery ekranı](screen-discovery.md)
