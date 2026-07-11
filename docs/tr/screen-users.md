# Kullanıcılar Ekranı

Üst çubuktaki `?` bu sayfayı Kullanıcılar ekranından açar. Bu ekran; yerel ve Active Directory kaynaklı kullanıcıları, genel rolleri, hesap ve 2FA durumunu ve kasa erişimi sayısını birlikte incelemek için kullanılır.

Yalnızca **Owner** ve **Admin** bu ekranı açabilir. Auditor ile User kullanıcı listesini göremez. Lisans salt okunur durumdaysa liste ve detaylar incelenebilir, fakat kullanıcıyı değiştiren işlemler kapalıdır.

## Burada Ne Yapılır

- Yerel kullanıcı oluşturulur; geçici ana parola ve ilk rol atanır.
- Kullanıcı adı ile görünen ad düzenlenir.
- Owner olmayan kullanıcıya Admin, Auditor veya User rolü verilir.
- Kullanıcı kapatılır, kapasite uygunsa tekrar açılır veya kapalı kullanıcı kalıcı silinir.
- Yalnız kurucu Owner, başka bir Owner olmayan kullanıcı için geçici parola belirleyebilir veya 2FA kaydını sıfırlayabilir.

Bu ekran yeni bir Owner oluşturmaz. Normal oluşturma ve rol değiştirme seçeneklerinde yalnız **Admin**, **Auditor** ve **User** vardır.

## Listeyi ve Detayı Okuma

Kullanıcılar oluşturulma sırasıyla listelenir. Her satırda rol ve kaynak rozeti, görünen ad/kullanıcı adı, kasa erişimi sayısı, kısa public key izi, 2FA ve `ACTIVE`/`DISABLED` durumu görünür.

**Detayı gör** çekmecesi aynı bilgileri düzenli biçimde sunar. Oturumları, kullanıcıya ait audit zaman çizelgesini, oluşturulma tarihini, Active Directory DN bilgisini veya tam public key'i göstermez.

Kaynak rozetleri:

- **Lokal:** VaultPilot içinde oluşturulan `LOCAL` kullanıcı.
- **Eşitleme:** `DIRECTORY` kullanıcısı; sağlayıcı bulunursa adı açıklamada görünür.
- **Active Directory:** Şifreli bir AD credential kaydına bağlı `CREDENTIAL` kullanıcı.

Bir `LOCAL` kullanıcının adı seçili bir directory nesnesiyle eşleşirse arayüz onu sezgisel olarak **Eşitleme** etiketiyle gösterebilir. Bu rozet tek başına kesin login source kanıtı değildir.

`ACTIVE` kullanıcı oturum açabilir ve aktif lisans sayımına dahildir. `DISABLED` kullanıcı oturum açamaz ve aktif kapasiteyi tüketmez; kaydı henüz silinmemiştir. Yüklemede iskelet satırlar, hiç kullanıcı yoksa boş durum görünür.

## Yerel Kullanıcı Oluşturma

1. **Yeni kullanıcı oluştur** panelini açın.
2. En az iki karakterli, benzersiz kullanıcı adı girin.
3. İsteğe bağlı görünen adı girin.
4. Admin, Auditor veya User rolünü seçin.
5. En az 14 karakterli geçici ana parolayı iki alana aynı yazın.
6. **Kullanıcı oluştur** ile kaydedin.

Owner veya Admin rolü, yazılabilir lisans ve boş aktif kullanıcı kapasitesi gerekir. Kapasite doluysa lisansı yükseltin veya artık giriş yapmaması gereken kullanıcıyı kapatın.

Tarayıcı geçici ana paroladan auth doğrulayıcısı, kullanıcı anahtar çifti ve kişisel kasa anahtar malzemesi türetir; sunucuya düz metin parola gönderilmez. Sunucu kullanıcıyı `ACTIVE` ve `LOCAL` olarak oluşturur, kişisel kasayı açar ve kullanıcıya bu kasada Manager erişimi verir.

Geçici parolayı audit notuna, destek kaydına veya ekran görüntüsüne yazmayın. Yalnız güvenilir ve ayrı bir kanaldan iletin.

## Kullanıcı Bilgisi ve Roller

Owner ve Admin etkin kullanıcıların kullanıcı adı ile görünen adını düzenleyebilir. Owner kullanıcı adı değiştirilemez; Admin bir Owner kaydını düzenleyemez. Owner kendi görünen adını değiştirebilir.

| Rol | Konsoldaki kapsam |
| --- | --- |
| Admin | Kullanıcıları ve kasaları yönetir; lisansı yönetemez. |
| Auditor | Audit ve sistem durumunu görür; gizli değerlere veya kasa anahtarlarına erişemez. |
| User | Yalnız atanan kasaları, o kasadaki Manager/Editor/Viewer rolüne göre kullanır. |

Kullanıcı kendi genel rolünü değiştiremez ve Owner rolü değiştirilemez. Arayüz kapalı kullanıcıda düzenleme ve rol seçimini devre dışı bırakır; konsoldan değiştirmek için önce tekrar açın.

Genel kullanıcı rolü ile kasa rolünü karıştırmayın. Satırdaki kasa sayısı, her kasadaki yetki seviyesini göstermez.

## Active Directory Giriş Erişimi

AD giriş erişimi Kullanıcılar satırından verilmez. İlgili Active Directory kaydının menüsündeki **VaultPilot girişine al** veya **VaultPilot girişinden çıkar** eylemi kullanılır.

Bu akış yalnız Owner rolüne açıktır ve yazılabilir lisans ister. Directory kaynağı için sağlayıcı ile DN, credential kaynağı için kaynak secret kaydı gerekir. Yeni yönetilen kullanıcı User rolüyle açılır; mevcut Admin veya Auditor rolü korunabilir.

VaultPilot her girişte LDAP bind yapmaz. Erişim verildiğinde mevcut şifreli AD credential parolasından yerel VaultPilot doğrulayıcısı ve anahtar malzemesi türetilir. AD parolası dışarıda değişirse otomatik eşitlenmez. Seçili OU veya kullanıcılar da yalnız seçim yapıldığı için otomatik oluşturulmaz.

Mevcut yönetilen kullanıcının ortak kasa erişimi varsa giriş malzemesini bu akışla yenileme reddedilir. Giriş erişimini kapatmak kullanıcıyı `DISABLED` yapar ve oturumlarını iptal eder.

Kullanıcı durumu ile directory sağlayıcı seçimi ayrı isteklerde kaydedilir. İlk işlem başarılı, ikinci işlem başarısız olabilir. Hata sonrası Kullanıcılar listesini ve AD seçim ekranını ayrı ayrı yenileyin.

## Parola Belirleme ve 2FA Sıfırlama

Bu işlemler yalnız kurucu Owner hesabına açıktır. Yeni kurulumda kullanıcı adı `VpAdm`'dir; eski `administrator` kurucu hesabı uyumluluk için tanınır. İşlemler kendi hesabına veya herhangi bir Owner'a uygulanamaz.

### Geçici parola belirleme

- Yeni parola en az 14 karakter olmalı ve onayı eşleşmelidir.
- Auth doğrulayıcısı ile kullanıcı anahtar çifti yenilenir.
- 2FA kaydı sıfırlanır ve açık oturumlar iptal edilir.
- `USER_PASSWORD_SET` yazılır; düz metin parola audit'e yazılmaz.

> **Durma koşulu:** Bu eylemi kayıpsız kasa kurtarma veya sıradan parola rotasyonu olarak kullanmayın. Uygulama yeni kişisel kasa anahtarı üretir ve yalnız kurucu Owner'ın o anda açabildiği ortak kasalardaki eşleşen erişimleri yeni anahtara sarabilir. Mevcut kişisel kasa içeriği veya yeniden sarılmayan ortak kasa erişimleri okunamaz hale gelebilir. İçerik ve kasa erişim envanteri doğrulanmadan devam etmeyin.

### 2FA kaydını sıfırlama

Mevcut authenticator bağı kaldırılır, `TWO_FACTOR_DISABLE` yazılır ve açık oturumlar iptal edilir. Kullanıcı sonraki başarılı girişinden sonra 2FA'yı yeni cihazla yeniden kurabilir. Aktif 2FA yoksa işlem yapılmaz.

## Kapatma, Tekrar Açma ve Kalıcı Silme

### Kullanıcıyı kapatma

Owner veya Admin, kendi hesabı ve Owner dışındaki etkin kullanıcıyı kapatabilir. Durum `DISABLED` olur, oturumlar iptal edilir, aktif lisans sayımı azalır ve `USER_DISABLE` yazılır. Arayüz hiçbir Owner'ı kapatmaya izin vermez.

### Kullanıcıyı tekrar açma

**Tekrar aç** yalnız kapalı kullanıcıda görünür. Yazılabilir lisans ve boş aktif kullanıcı kapasitesi gerekir. Başarı kullanıcıyı `ACTIVE` yapar ve `USER_UPDATE` yazar.

### Kullanıcıyı kalıcı silme

Yalnız önceden kapatılmış, kendi hesabınız olmayan ve Owner rolünde olmayan kullanıcı silinebilir. İşlem geri alınamaz.

> **Durma koşulu:** Kişisel kasa, ortak kasa erişimleri ve kullanıcıya bağlı operasyon kayıtları için sahiplik devri tamamlanmadan silmeyin. Veritabanı ilişkileri; kullanıcı tarafından oluşturulan audit satırları, extension cihazları, API istemcileri, directory sağlayıcıları/işlemleri, discovery kayıtları, dosya parçaları ve gönderilen/alınan paylaşım paketleri gibi bağlı kayıtları da kaldırabilir.

Silmeden hemen önce `USER_DELETE` oluşturulur. Metadata hedef kullanıcı kimliği ve rolü, kişisel kasa sayısı ve silinecek kullanıcı audit geçmişinin sayı/son hash özetini taşır. Bu, kullanıcının bütün eski audit satırlarının korunduğu anlamına gelmez.

## Audit ve İşlem Sınırı

| İşlem | Audit olayı |
| --- | --- |
| Kullanıcı oluşturma | `USER_CREATE` |
| Bilgi düzenleme | `USER_UPDATE` |
| Rol değiştirme | `USER_ROLE_UPDATE` |
| Kapatma / AD girişinden çıkarma | `USER_DISABLE` |
| Tekrar açma / yönetilen erişimi yenileme | `USER_UPDATE` |
| Kurucu Owner'ın parola belirlemesi | `USER_PASSWORD_SET` |
| 2FA sıfırlama | `TWO_FACTOR_DISABLE` |
| Kalıcı silme | `USER_DELETE` |

Her olay etkilenen kullanıcıya aynı ayrıntıyla bağlanmaz. Oluşturma, bilgi/rol değişikliği, kapatma, tekrar açma ve parola olaylarının çoğu ayrı hedef kullanıcı kimliği taşımaz. Aktör, zaman, eylem ve varsa target/metadata birlikte incelenmelidir.

Kullanıcı değişikliği, audit yazımı ve oturum iptali tek atomik işlem değildir. Geç bir audit veya oturum temizleme hatası, kullanıcı değiştikten sonra görülebilir. Hata sonrası listeyi, hesap durumunu, oturumları ve Audit ekranını yenileyin; işlemi körlemesine tekrarlamayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Yükleniyor | İskelet satırlar kaybolana kadar işlem başlatmayın. |
| Liste boş | Sunucu profili ve oturumu doğrulayın; kurucu Owner'ın görünmemesi normal değildir. |
| Lisans salt okunur | Yalnız inceleyin; kullanıcı değiştiren işlem başlatmayın. |
| Kapasite dolu | Kullanıcı oluşturmayın/tekrar açmayın; kapasite açın veya lisansı yükseltin. |
| Kaynak rozeti beklenmedik | Gerçek login source ile AD seçimini ayrı kontrol edin. |
| İşlem sonrası hata | Kullanıcı, lisans, oturum ve audit durumunu yenileyip doğrulayın. |
| Parola kurtarma | İçerik ve anahtar erişim envanteri yoksa durun. |
| Kalıcı silme | Sahiplik devri ve bağımlılık envanteri tamamlanmadıysa durun. |

## İşlemden Önce

- Doğru sunucu profili ve kullanıcı satırında olduğunuzu doğrulayın.
- Genel rol ile kasa rolünü ayrı inceleyin.
- AD kullanıcısında AD kayıt durumunu ve VaultPilot hesap durumunu ayrı kontrol edin.
- Parola/2FA hedefinin kendi hesabınız veya Owner olmadığını doğrulayın.
- Kapatma öncesi açık iş ve entegrasyon sahipliğini devredin.
- Silme öncesi kasa, paylaşım, API istemcisi, directory/discovery ve audit bağımlılıklarını çıkarın.
- Oluşturma veya tekrar açma öncesi aktif kullanıcı kapasitesini kontrol edin.
- Onay penceresindeki kullanıcı adını son kez doğrulayın.

## Güvenli Kanıt

- Paylaşılabilir: rol kategorisi, `ACTIVE`/`DISABLED`, 2FA açık/kapalı özeti ve redakte kasa erişim sayısı.
- Audit olay türü, zaman damgası ve kısaltılmış bütünlük hash'i kullanılabilir.
- Lisans kanıtında yalnız aktif kullanıcı toplamı ve limiti gösterin.
- Gizli kalmalı: gerçek kullanıcı adı, görünen ad, e-posta/UPN, DN, public key, kişisel kasa adı ve kullanıcı listesi ekran görüntüleri.
- Geçici ana parola, TOTP secret, authenticator QR/kurtarma bilgisi veya kasa anahtarı kanıta eklenmemelidir.
- Private support ekran görüntüsünde kullanıcı adlarını ve anahtar izlerini redakte edin; dolu parola alanını çekmeyin.

## Operatör Notları

- Ekran son giriş veya son aktivite göstermez; burada incelenmiş gibi raporlamayın.
- **Parola belirle** dış sağlayıcı parolasını değiştirmez ve otomatik rotasyon değildir.
- AD giriş erişimi gerçek zamanlı LDAP doğrulaması değildir; seçili AD nesneleri otomatik kullanıcı üretmez.
- Kapatma veriyi silmez; kalıcı silme geri alınamaz ve geniş bağlı-kayıt etkisine sahiptir.
- Kullanıcı değişikliği ile audit/oturum temizliği aynı atomik sınırda değildir.
- Yeni Owner oluşturma veya Owner rolünü devretme kontrolü bu ekranda yoktur.

## İlgili

- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Denetim kaydı ekranı](screen-audit-log.md)
- [Active Directory kayıtları ekranı](screen-active-directory-records.md)
- [Paylaşım ekranı](screen-sharing.md)
- [Lisans ekranı](screen-license.md)
