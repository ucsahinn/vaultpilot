# Giriş Güvenliği Ekranı

Üst çubuktaki `?` bu sayfayı Giriş güvenliği ekranından açar. Kilit davranışı, 2FA duruşu ve oturum güvenliği incelenirken kullanın.

## Burada Ne Yapılır

- Geniş kullanım öncesi privileged kullanıcılar için 2FA etkinliğini doğrulayın.
- Kilit ve timeout ayarlarının operatör ortamıyla uyumlu olduğunu kontrol edin.
- Tekrarlayan login hatalarını veya beklenmeyen oturum gürültüsünü authentication zayıflatma sebebi değil, support kanıtı olarak ele alın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Güçlü | Kurtarma ve owner erişiminin hâlâ çalıştığını doğrulayın. |
| Zayıf | Her seferinde tek kontrolü sıkılaştırın ve sonrasında sign-in doğrulaması yapın. |
| Kilitlendi | Owner recovery prosedürünü kullanın; master password istemeyin. |

## İşlemden Önce

- Policy sıkılaştırmadan önce en az bir owner için çalışan recovery yolu olduğunu doğrulayın.
- Operatörleri kilitlememek için lockout, 2FA ve session kontrollerini birlikte inceleyin.
- Authentication sorunlarını eskale ederken identity evidence bilgisini redakte tutun.

## Güvenli Kanıt

- Paylaşılabilir: policy özeti, kilitlenme durumu, 2FA enrollment kategorisi ve yaklaşık timestamp.
- Gizli kalmalı: username, recovery code, TOTP seed, master password, session token ve cihaz fingerprint'i.
- Identity proof veya owner recovery kanıtı gerekiyorsa private support kullanın.

## Operatör Notları

Master password, recovery code, TOTP seed, auth hash, cookie veya one-time code gösteren ekran görüntüsü yayınlamayın.

## İlgili

- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Login sonrası 401 KB](../../kb/tr/session-401-after-login.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
