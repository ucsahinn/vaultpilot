# Güvenlik Dashboard Ekranı

Üst çubuktaki `?` bu sayfayı Güvenlik dashboard ekranından açar. Giriş güvenliği, denetim bütünlüğü, lisans durumu, güncelleme hazırlığı ve eklenti duruşu sinyallerini birlikte yorumlamak için kullanın.

## Burada Ne Yapılır

- Zayıf duruş sebebinin eksik 2FA, read-only lisans, audit-chain sorunu, bayat update veya eksik tarayıcı onayı olup olmadığını doğrulayın.
- Uyarıları gizlemek yerine root control'ü düzeltin.
- Audit integrity partial ise veya privileged account beklenmeyen şekilde değiştiyse olayı yükseltin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Sağlıklı | Skor zaman aralığını not edin ve rutin incelemeye devam edin. |
| Zayıf | En düşük sinyali açıp sebebin config, lisans veya audit kaynaklı olup olmadığını doğrulayın. |
| Bilinmiyor | Diagnostics'i bir kez yenileyin, sonra tahmin etmek yerine unavailable component adını koruyun. |

## İşlemden Önce

- Hesap güvenliği bulgularını sunucu veya güncelleme bulgularından ayırın.
- Görülen skorun son kullanıcı, lisans veya güncelleme değişikliğinden sonra yenilendiğini doğrulayın.
- Destek için yalnız redakte edilmiş duruş özetleri hazırlayın; kullanıcı adı ve iç host bilgisini public notlara koymayın.

## Güvenli Kanıt

- Paylaşılabilir: duruş bandı, sinyal kategorisi, refresh penceresi, redakte skor değişimi ve etkilenen control family.
- Gizli kalmalı: gerçek kullanıcı adı, hostname, vault adı, tenant identifier, internal count ve müşteri bağlamı gösteren ekran görüntüsü.
- Security posture özetini public paylaşmadan önce kullanıcı, host ve vault identifier'larını çıkarın.

## Operatör Notları

Security dashboard datası özetlenebilir; ancak gerçek kullanıcı adı, host, vault adı veya iç müşteri bağlamı görünen ekran görüntüsü public paylaşılmaz.

## İlgili

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Giriş güvenliği ekranı](screen-sign-in-security.md)
