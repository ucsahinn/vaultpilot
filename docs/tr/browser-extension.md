# Chrome Web Store Eklentisi

VaultPilot Browser Vault Extension; eşleştirilmiş cihazlarda kullanıcı aksiyonuyla autofill, login kaydetme, login güncelleme ve aktif site kayıt sayısı rozeti sağlar.

![VaultPilot tarayıcı eklentisi yönetimi](../../assets/screenshots/browser-extension-management-vaultpilot-2.png)

Bu yayıma uygun hale getirilmiş UI görseli yalnızca sentetik veri içerir. Chrome Web Store dağıtımını, onaylı cihaz sayısını, eşleştirme adımlarını ve cihaz onay kontrollerini gösterir. Görünen cihaz adları, sayılar, kodlar ve zaman damgaları dokümantasyon örneğidir; production rehberi değildir.

## Chrome Web Store'dan Kurulum

Desteklenen müşteri kurulum yolu Chrome Web Store listelemesidir:

`https://chromewebstore.google.com/detail/vaultpilot-browser-vault/hjkbedlaieikhkoplgpiohlaakgebobi?hl=tr`

Eski mağaza URL'leri tarihsel slug üzerinden yönlenebilir. Desteklenen eklenti kimliği yayınlanmış extension ID değeridir: `hjkbedlaieikhkoplgpiohlaakgebobi`.

Merkezi yönetilen cihazlarda bu Web Store eklenti ID'sini Chrome veya Edge policy ile dağıtın. Chrome eklenti güncellemelerini Web Store üzerinden otomatik kontrol eder. Eklentinin Hakkında ekranı Web Store güncelleme kontrolü isteyebilir; ancak Chromium kontrolleri sınırlayabilir ve güncelleme yalnızca tarayıcı tarafından hazır bildirildiğinde uygulanır.

Release ZIP yalnızca release arşivi, lab doğrulama, lokal geliştirme ve acil fallback için tutulur. ZIP'i normal müşteri kurulum yolu olarak kullanmayın.

Store listing metni, privacy practice cevapları, permission gerekçeleri ve screenshot kuralları [Chrome Web Store listeleme ve privacy](chrome-web-store-listing.md) sayfasında tutulur.

## Eşleştirme Akışı

1. VaultPilot Browser Vault Extension'ı Chrome Web Store'dan kurun.
2. Eklenti popup'ını açın.
3. VaultPilot server origin değerini girin.
4. Kullanıcı adı, cihaz adı ve eklenti PIN'i girin.
5. Eklenti kısa ömürlü bir pairing code üretir.
6. Cihazı VaultPilot -> Tarayıcı eklentisi ekranından onaylayın.
7. VaultPilot vault erişimini eklenti public key'i için wrap eder.

## Kullanıcı Deneyimi

| Özellik | Davranış |
| --- | --- |
| Rozet sayısı | Eklenti ikonu mevcut site için eşleşen kayıt sayısını gösterir. |
| Autofill | Kullanıcı aksiyonu seçili kaydı mevcut sayfaya doldurur. |
| Login kaydetme | Yeni login tespit edilirse kullanıcıya kayıt oluşturma önerilir. |
| Login güncelleme | Kullanıcı adı/parola değişikliği tespit edilirse mevcut kaydı güncelleme önerilir. |
| Bildirimler | Eşleştirme, iptal, autofill ve kaydet/güncelle durumları popup ve desteklenen tarayıcı bildirim yüzeylerinde gösterilir. |

## Güvenlik Modeli

- Eklenti private materyali, eklenti PIN'i ve tarayıcı profil storage'ı ile korunur.
- Kalıcı eklenti storage'ı plaintext secret içermez.
- Autofill snapshot'ları encrypted payload ve eklentiye wrap edilmiş key içerir.
- Plaintext yalnızca kullanıcı aksiyonundan sonra aktif eklenti oturumunda çözülür.
- Kaybolan veya güvenilmeyen cihazlar VaultPilot panelinden iptal edilmelidir.

## Operasyon Kontrol Listesi

- Yalnızca isimlendirilmiş cihazları eşleştirin.
- Kullanıcı kurulumları ve güncellemeler için Chrome Web Store listelemesini kullanın.
- Merkezi yönetilen cihazlarda Web Store eklenti ID'sini browser policy ile dağıtın.
- Update sonrası Tarayıcı eklentisi ekranını kontrol edin.
- Kullanılmayan, bilinmeyen veya uyumsuz cihazları iptal edin.
