# Uygulama İçi Ekran Yardımı

VaultPilot içinde her workspace ekranının üst barında bir `?` butonu vardır. Bu buton, operatörü o an açık olan ekranın herkese açık paylaşım için güvenli Markdown sayfasına ve seçili dile götürür; böylece işlem akışı bozulmadan doğru prosedür okunabilir.

Uygulama kabuğu ile herkese açık dokümantasyonun hizalı kalıp kalmadığını denetlerken bu indeksi kullanın.

İki sekme düzeyindeki yönlendirme özellikle daha nettir. Entegrasyonlar ekranı tarayıcı eklentisi sekmesindeyken `?` butonu [screen-browser-extension.md](screen-browser-extension.md) sayfasını açar. Sunucu ayarları ekranı giriş ve oturum güvenliği sekmesindeyken `?` butonu [screen-sign-in-security.md](screen-sign-in-security.md) sayfasını açar.

| Ekran | Yardım sayfası | Temel karar |
| --- | --- | --- |
| Güvenlik Komuta Merkezi | [screen-security-command-center.md](screen-security-command-center.md) | Önce hangi operasyon sinyalinin aksiyon istediğini seçin. |
| Güvenlik dashboard'u | [screen-security-dashboard.md](screen-security-dashboard.md) | Güvenlik duruşunu, 2FA'yı, lisansı ve audit riskini birlikte okuyun. |
| Etki Alanı dashboard'u | [screen-domain-dashboard.md](screen-domain-dashboard.md) | Kimlik bilgisi işinden önce dizin eşitleme sağlığını kontrol edin. |
| Sertifika Paneli | [screen-certificate-dashboard.md](screen-certificate-dashboard.md) | TLS ve kayıtlı sertifika riskini takip edin. |
| Rotasyon | [screen-rotation-dashboard.md](screen-rotation-dashboard.md) | Kimlik bilgisi rotasyon planını sahiplik kanıtını kaybetmeden yapın. |
| Yeni kayıt | [screen-new-item.md](screen-new-item.md) | Kaydetmeden önce doğru gizli değer türünü seçin. |
| Parolalar | [screen-passwords.md](screen-passwords.md) | Login kayıtlarıyla güvenli çalışın. |
| API anahtarları | [screen-api-keys.md](screen-api-keys.md) | API kimlik bilgilerini loglamadan ve yayınlamadan saklayın. |
| Güvenli notlar | [screen-secure-notes.md](screen-secure-notes.md) | Hassas metni yapılandırılmış ve aranabilir tutun. |
| Sertifikalar | [screen-certificates.md](screen-certificates.md) | Sertifika meta verisini ve şifreli paket notlarını yönetin. |
| Dosyalar | [screen-files.md](screen-files.md) | Onaylı dosyaları kasayı çöp kutusuna çevirmeden ekleyin. |
| Active Directory kayıtları | [screen-active-directory-records.md](screen-active-directory-records.md) | Dizin kaynaklı kimlik bilgisini ve sahiplik durumunu inceleyin. |
| Paylaşım | [screen-sharing.md](screen-sharing.md) | Sadece gereken kayıtları limit ve süre sonu ile paylaşın. |
| Giriş güvenliği | [screen-sign-in-security.md](screen-sign-in-security.md) | Kilit, 2FA ve oturum kontrollerini inceleyin. |
| Discovery | [screen-discovery.md](screen-discovery.md) | Onaylı maruziyet kontrollerini çalıştırın ve yalnız doğrulanmış bulguları içe aktarın. |
| Kullanıcılar | [screen-users.md](screen-users.md) | Hesap, rol ve erişim değişikliklerini yönetin. |
| Lisans | [screen-license.md](screen-license.md) | Özellik erişimini, deneme durumunu ve salt okunur sınırı anlayın. |
| Denetim kaydı | [screen-audit-log.md](screen-audit-log.md) | Kimin ne yaptığını ve audit chain'i kanıtlayın. |
| Entegrasyonlar | [screen-integrations.md](screen-integrations.md) | API istemcisi, eklenti durumu ve dizin connector sağlığını yönetin. |
| Bildirimler | [screen-notifications.md](screen-notifications.md) | Önemli olayları secret sızdırmadan yönlendirin. |
| İşlemler | [screen-executions.md](screen-executions.md) | Aktif işleri izleyin ve takılan işleri kanıtla toparlayın. |
| Güncellemeler | [screen-updates.md](screen-updates.md) | Güncelleme çalıştırmadan önce release paketlerini doğrulayın. |
| Sunucu ayarları | [screen-server-settings.md](screen-server-settings.md) | Host, HTTPS, SMTP, bakım ve saklama ayarlarını değiştirin. |
| Tarayıcı eklentisi | [screen-browser-extension.md](screen-browser-extension.md) | Tarayıcı cihaz eşleştirme, onay ve erişim iptali akışını yönetin. |

Herkese açık güvenlik kuralı: yardım sayfaları yalnız yer tutucu ve sentetik örnek kullanır. Gerçek vault içeriği, PFX/P12 dosyası, private key, credential içeren log, API client secret, lisans private materyali veya müşteri ekran görüntüsü eklemeyin.

İlgili: [Dokümantasyon gateway](../README.md), [Public repo sınırı](public-repository-boundary.md), [Public dil sözlüğü](public-language-glossary.md).
