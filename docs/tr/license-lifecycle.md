# Lisans Yaşam Döngüsü

VaultPilot offline lisans doğrulaması kullanır. Sunucu lisans kodunu public doğrulama materyaliyle doğrular; issuer-side private imza materyali müşteri sunucusuna kurulmaz.

## Normal Yaşam Döngüsü

| Aşama | Operatörün gördüğü | Aksiyon |
| --- | --- | --- |
| Trial | VaultPilot trial limitleri ve expiry tarihiyle çalışır. | Production kullanımdan önce deployment, backup, HTTPS ve owner erişimini doğrulayın. |
| Aktif lisans | License ekranı plan, kapasite, expiry, imza durumu ve açık modülleri gösterir. | Aylık operasyonda kapasite ve expiry tarihini kontrol edin. |
| Yenileme penceresi | Expiry yaklaşmıştır ve replacement planlanır. | Onaylı support kanalı üzerinden yeni offline lisans kodunu isteyin. |
| Değişim | Yeni kod License ekranına girilir. | İmza doğrulama, kapasite, expiry ve modül durumunu kontrol edin. |
| Süre bitimi veya kapasite aşımı | VaultPilot güvenli okuma ve backup-export yollarını korurken write aksiyonlarını kısıtlayabilir. | Kullanımı düşürün, geçerli lisans uygulayın veya yeni kullanıcı/workflow açmadan support ile ilerleyin. |

## Read-only Davranışı

Trial veya lisans süresi bittiğinde VaultPilot login, secret viewing, audit review ve backup export erişimini koruyabilir; yazma, kullanıcı ekleme, paylaşım, eklenti pairing ve update install aksiyonlarını engelleyebilir. Amaç encrypted dataya erişimi kesmeden lisanssız genişlemeyi durdurmaktır.

## Ne Kaydedilir

- Lisans durumu, plan ve expiry tarihi.
- Aktif kullanıcı sayısı ve kapasite.
- İmza doğrulama durumu.
- Açık veya unavailable modüller.
- Replacement tarihi ve onaylayan kişi.

Lisans kodlarını, issuer private materyalini veya müşteri verisi içeren ekran görüntülerini public ticket içine koymayın.

İlgili:

- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Operasyon runbook](operator-runbook.md)
- [Bilgi bankası: lisans read-only](../../kb/tr/license-read-only.md)
- [Destek kanıt paketi](support-evidence-pack.md)
