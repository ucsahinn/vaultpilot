# VaultPilot Türkçe Bilgi Bankası

VaultPilot kurulu olduğu halde operatör hızlı ve güvenli bir teşhis yolu arıyorsa bu sayfadan başlayın. Her makale belirtiyi, ilk kontrolleri, güvenli kanıtları ve public olarak gönderilmemesi gerekenleri ayırır.

## Olay İndeksi

| Belirti | Makale | İlk kontrol |
| --- | --- | --- |
| MSI kurulumu başarısız | [MSI kurulumu başarısız](msi-installation-fails.md) | MSI dosya adı, admin context ve Windows servis durumu. |
| Update yüzde 76 civarında kalıyor | [Update yüzde 76 civarında kalıyor](update-stuck-76.md) | Update job JSON, MSI imza satırı ve Windows Installer event log. |
| DC Agent servisi bağlanmıyor veya 401 dönüyor | [DC Agent servis sorunları](dc-agent-service.md) | Servis durumu, agent logu, VaultPilot URL erişimi ve redakte server auth sebebi. |
| Eklenti eşleşmesi beklemede kalıyor | [Eklenti eşleşmesi beklemede kalıyor](extension-pairing.md) | Eşleştirme kodu durumu, cihaz satırı ve tarayıcı profil modu. |
| Chrome Web Store incelemesi veya gizlilik uyumsuzluğu | [Chrome Web Store incelemesi veya gizlilik uyumsuzluğu](chrome-web-store-review.md) | Extension ID, paket sürümü, gizlilik kategorileri, izinler ve yayına uygun hale getirilmiş ekran görüntüleri. |
| Girişten sonra 401 veya 403 log gürültüsü oluşuyor | [Login session 401/403 gürültüsü](session-401-after-login.md) | Login zamanı, etkilenen endpoint listesi ve `/api/auth/me` sonucunun 200 olup olmadığı. |
| Entegrasyon API client'ı 401 alıyor, kapsam reddediliyor veya boş veri dönüyor | [Entegrasyon API client erişimi](api-client-401.md) | Client durumu, endpoint kapsamı ve `SECRETS_READ` kullanılıyorsa atanmış vault sayısı. |
| HTTPS sertifika uyarısı | [HTTPS sertifika uyarısı](certificate-warning.md) | Hostname, SAN ve yüklenen sertifika paketi. |
| Server settings restart veya bakım incelemesi istiyor | [Server settings restart ve bakım](server-settings-restart-maintenance.md) | Servis durumu, canonical URL, HTTPS durumu, bildirim testi ve retention değerleri. |
| Backup import başarısız veya oturumları kapatıyor | [Backup import başarısız veya oturumları kapatıyor](backup-import-fails.md) | Dosya tipi, boyut, archive şekli, hata kodu ve oturumların kapanıp kapanmadığı. |
| Denetim zinciri kısmi | [Denetim zinciri kısmi veya tutarsız](audit-chain-partial.md) | Audit filtreleri, zincir durumu ve son restore/update olayları. |
| Lisans salt okunur | [Lisans salt okunur durumu](license-read-only.md) | Lisans durumu, plan limitleri, aktif kullanıcılar ve bitiş tarihi. |
| Discovery bulgusu inceleme istiyor veya import kapalı | [Discovery bulgu inceleme](discovery-finding-review.md) | Scope onayı, bulgu durumu, evidence hash ve kasa unlock durumu. |
| Public issue redaksiyon incelemesi gerekiyor | [Public issue redaction](public-issue-redaction.md) | Sürüm, component, redakte hata durumu ve yer tutucu host biçimi. |
| Public ekran görüntüsü hassas veri içerebilir | [Public screenshot redaction](public-screenshot-redaction.md) | Full-size görsel kontrolü, hassas veri kategorisi, replacement yolu ve rotation sınırı. |
| Public doğrulama başarısız oluyor | [Public doğrulama başarısız oluyor](public-validation-fails.md) | Başarısız olan komut, doğrulama mesajı, staged-vs-working-tree durumu ve güvenli kurtarma yolu. |
| Dış paylaşım açılmıyor | [Dış paylaşım paketi açılamıyor](external-share-fails.md) | Paket metadata, süre sonu, maksimum açma ve decrypter hata durumu. |

## Güvenli Kanıt

Yalnızca redakte edilmiş kanıt gönderin:

- Bileşen sürümleri ve Windows sürümü.
- Servis durumu ve redakte edilmiş zaman damgaları.
- Secret değeri değil, hata durumu.
- Gerçek host yerine `<SERVER_HOST>` kullanılmış public host biçimi.
- Gerçek agent id/token yerine yer tutucu.

## Eskalasyon Yolu

Makale sorunu çözmezse güvenli kanıtları toplayın, [Destek](../../SUPPORT.md) sayfasını inceleyin ve private support kanalı açın. Database, yedek, sertifika, key, token değeri, gerçek kasa verisi içeren ekran görüntüsü veya secret içerebilen ham log eklemeyin.

İlgili: [Türkçe dokümanlar](../../docs/tr/README.md), [Repo ana sayfası](../../README.md), [Güvenlik politikası](../../SECURITY.md), [Public repo sınırı](../../docs/tr/public-repository-boundary.md), [Public repo yayın runbook'u](../../docs/tr/publication-runbook.md), [Public ekran görüntüsü standartları](../../docs/tr/public-screenshot-standards.md).
