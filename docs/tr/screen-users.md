# Kullanıcılar Ekranı

Üst çubuktaki `?` bu sayfayı Kullanıcılar ekranından açar. Hesap durumu, rol, 2FA durumu ve kasa erişimi incelemesi için kullanın.

## Burada Ne Yapılır

- En az bir korumalı Owner hesabını koruyun.
- Minimum rol ve minimum kasa erişimi verin.
- Ayrıcalıklı rol değişikliklerinin nedenini kayda bağlayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Normal | Owner kapsamını, pasif hesapları ve 2FA durumunu gözden geçirin. |
| Ayrıcalıklı değişiklik | Kaydetmeden önce iş gerekçesini ve denetim bağlamını doğrulayın. |
| Son Owner riski | Erişimi kapatmadan önce durun ve kurtarmayı güvenli tutan Owner kurtarma planı oluşturun. |

## İşlemden Önce

- Kullanıcı değiştirmeden önce rol, kasa erişimi, 2FA durumu ve son aktiviteyi kontrol edin.
- Ayrıcalıklı erişimi devre dışı bırakmadan veya silmeden önce en az iki sorumlu Owner yolu koruyun.
- Erişim değişikliği gerekçesini public ortamda kimlik dokümanı veya kişisel veri göstermeden kaydedin.

## Güvenli Kanıt

- Paylaşılabilir: rol kategorisi, hesap durumu, 2FA kapsam özeti ve redakte değişiklik gerekçesi.
- Gizli kalmalı: isimler, e-posta adresleri, kurtarma durumu, kimlik dokümanı ve gerçek kullanıcı listesi ekran görüntüleri.
- Owner kurtarma, tartışmalı erişim kaldırma veya hesap ele geçirme şüphesi için private support kullanın.

## Operatör Notları

Gerçek tenant'tan kullanıcı adı, public key, rol değişikliği ekran görüntüsü veya kullanıcı listesi yayınlamayın. Redakte edilmiş private support kanıtı kullanın.

## İlgili

- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Denetim kaydı ekranı](screen-audit-log.md)
