# Lisans read-only durumu

VaultPilot login, vault viewing, audit review veya backup export izni veriyor ama yazma, kullanıcı değişikliği, sharing, pairing, discovery import veya update install aksiyonlarını engelliyorsa bu makaleyi kullanın. Read-only mode kontrollü bir güvenlik durumudur; database edit veya desteklenmeyen config değişikliğiyle aşılmamalıdır.

## İlk Müdahale

1. [Lisans](../../docs/tr/screen-license.md) ekranını açın ve üst bardaki `?` ile beklenen durumu kontrol edin.
2. Status değerinin trial, active, expired, over capacity, invalid signature veya read-only olup olmadığını not edin.
3. Aktif kullanıcı sayısını lisans kapasitesiyle karşılaştırın.
4. Sharing, browser extension, integrations, discovery ve updates için hangi özellik kapılarının açık veya kapalı olduğunu inceleyin.
5. Offline license code yalnız owner veya support onaylı kanaldan geldiyse yapıştırın.
6. Signature fail veriyorsa rastgele license material denemeyin; private eskalasyona geçin.

## Beklenen Davranış

| Capability | Read-only beklentisi |
| --- | --- |
| Login ve unlock | Account geçerliyse açık kalır. |
| Secret viewing | Yetkili kayıtlar için recover güvenliği amacıyla açık kalır. |
| Audit review | State change araştırılabilsin diye açık kalır. |
| Backup export | Owner-led recovery için genellikle açık kalır. |
| Writes, sharing, pairing, discovery import ve update install | Lisans durumu tekrar valid olana kadar engellenir. |

## Güvenli Kanıt

- License state label ve plan adı.
- Aktif kullanıcı sayısı ve capacity.
- Expiry tarihi veya trial state.
- Açık/kapalı özellik kapıları listesi.
- License payload değil, signature validation state.

## Göndermeyin

Public kanalda license code, signed payload, private license material, müşteri entitlement ekran görüntüsü, internal billing record veya raw database row paylaşmayın.

İlgili: [Lisans ekranı](../../docs/tr/screen-license.md), [Lisans lifecycle](../../docs/tr/license-lifecycle.md), [First run, owner ve lisans](../../docs/tr/first-run-owner-license.md), [Public issue redaction](public-issue-redaction.md).
