# Lisans Ekranı

Üst çubuktaki `?` bu sayfayı Lisans ekranından açar. Aktif planı, deneme durumunu, salt okunur davranışı ve özellik erişimlerini anlamak için kullanın.

## Burada Ne Yapılır

- Eksik özellik teşhisi yapmadan önce lisans status değerinin `active`, `trial`, `expired` veya `read-only` olup olmadığını doğrulayın.
- Paylaşım, eklenti, entegrasyon, discovery ve güncellemeler için özellik erişimlerini inceleyin.
- Lisans değiştirme veya temizleme işlemlerini yalnız onaylı owner prosedürüyle yapın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Aktif | Açık özelliklerin satın alınan planla eşleştiğini doğrulayın. |
| Salt okunur | Kurtarma erişimini koruyun ve değişiklikten önce salt okunur KB'yi izleyin. |
| İmza geçersiz | Private eskalasyon yapın; lisans materyalini public kanala yapıştırmayın. |

## İşlemden Önce

- Eksik özellik teşhisi öncesi status, plan, expiry, kapasite ve açık modülleri doğrulayın.
- Lisans değişimi denemeden önce owner ve yedek dışa aktarma erişimini koruyun.
- Lisans kodlarını, imzalı payload'ları ve müşteri entitlement detaylarını public support dışında tutun.

## Güvenli Kanıt

- Paylaşılabilir: lisans state, plan family, expiry window, açık feature kategorisi ve redakte hata kodu.
- Gizli kalmalı: lisans kodu, signed payload, issuer materyali, müşteri entitlement detayları ve müşteri adı gösteren screenshot'lar.
- Invalid signature, kapasite anlaşmazlığı veya recovery-access sorunu için private support kullanın.

## Operatör Notları

Lisans kodu, private lisans materyali, imzalı payload veya müşteri entitlement bilgisi gösteren ekran görüntüsü yayınlamayın.

## İlgili

- [Lisans yaşam döngüsü](license-lifecycle.md)
- [Lisans salt okunur bilgi bankası](../../kb/tr/license-read-only.md)
- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
