# Denetim Kaydı Ekranı

Üst çubuktaki `?` bu sayfayı Denetim kaydı ekranından açar. Olay geçmişini, aktör bağlamını, hedef değişikliklerini ve denetim zinciri kanıtını incelemek için kullanın.

## Burada Ne Yapılır

- Export öncesi aksiyon, aktör, hedef ve risk filtresi kullanın.
- Kısmi zincir durumunu inceleme maddesi olarak ele alın.
- Private support kanıtı hazırlarken event hash ve zaman damgası bilgisini koruyun.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Tam | Filtreyi ve dışa aktarma kapsamını dar tutun. |
| Kısmi | Event listesine güvenmeden önce audit-chain KB'yi kullanın. |
| Bağlam eksik | Private support için filtre state ve yakın zaman damgalarını kaydedin. |

## İşlemden Önce

- Dışa aktarma öncesi actor, action, target ve zaman filtresi alanlarını ayarlayın.
- Chain gap incelerken event hash'lerini ve yakın timestamp'leri koruyun.
- Audit integrity belirsizse ve incident aktifse kritik olmayan değişiklikleri durdurun.

## Güvenli Kanıt

- Paylaşılabilir: event kategorisi, dar zaman aralığı, redakte actor rolü, event hash ve filter özeti.
- Gizli kalmalı: username, object ID, raw audit export, internal IP ve müşteri bağlamı içeren incident materyali.
- Audit-chain integrity partial ise kanıtı koruyun ve kayıt değiştirmeden önce audit-chain KB'yi kullanın.

## Operatör Notları

Audit evidence username, internal object ID ve operasyon zamanı gösterebilir. Public issue'larda redakte edin, gerçek incident materyali için private support kullanın.

## İlgili

- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Audit chain partial KB](../../kb/tr/audit-chain-partial.md)
- [Destek kanıt paketi](support-evidence-pack.md)
