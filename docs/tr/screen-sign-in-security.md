# Giriş Güvenliği Ekranı

Üst çubuktaki `?`, **Sunucu ayarları > Giriş güvenliği** sekmesine ait bu rehberi açar. Bu sekme, açık olan kişisel profilin ana parola değişimini, TOTP tabanlı 2FA bağını ve Sahip rolünde etkin sunucu oturumlarını yönetir. VaultPilot girişi kullanıcı adı, ana parola ve 2FA açıksa authenticator koduyla yapılır; bu ekranda e-posta bağlantısı, e-postayla parola sıfırlama, harici kimlik sağlayıcısı/SSO veya kurtarma kodu akışı yoktur.

## Erişim, Rol ve Sunucu Ayarları Bağlamı

Giriş güvenliği ayrı bir lisans özelliğine bağlı değildir ve bütün sistem rolleri sekmeyi görebilir. Sahip, Yönetici ve Denetçi diğer Sunucu ayarları sekmelerini de görür; yalnız Kullanıcı rolünde sekme kümesi **Giriş güvenliği** ile sınırlandırılır. Bundan ayrı olarak, Sahip olmayan herhangi bir rolün Lisans veya Entegrasyonlar görünümüne gitme girişimi bu kişisel güvenlik sekmesine yönlendirilir.

Kendi ana parolasını veya 2FA bağını değiştiren sunucu API'leri Sahip, Yönetici ve Kullanıcı rollerini kabul eder; Denetçi bu formları görse bile sunucu değişikliği reddeder. Bu işlemler lisans yazılabilirken yapılabilir; salt okunur lisans profil değişikliğini engeller. Etkin oturum listesini görme ve başka bir oturumu kapatma yalnız Sahip içindir.

Bu sekme kişisel profil bağlamındadır. Sahip burada başka kullanıcının parolasını veya 2FA bağını sıfırlamaz. İlk sahip hesabının, uygun Sahip dışı kullanıcılar için parola belirleme ve 2FA sıfırlama araçları **Kullanıcılar** ekranındadır ve farklı yetki/onay sınırlarına sahiptir.

## Burada Ne Yapılır

- Mevcut ana parolayı doğrulayıp en az 14 karakterlik yeni ana parola ve onayını girin.
- 2FA kapalıysa yeni bir TOTP sırrı ve QR kodu oluşturup ilk altı haneli authenticator koduyla bağı etkinleştirin.
- 2FA açıksa bağın hem tarayıcı tarafındaki şifreli kopyasının hem sunucu doğrulama materyalinin hazır olup olmadığını okuyun.
- Kayıp telefon veya uygulama değişiminde, profil hâlâ açıksa mevcut 2FA bağını onayla iptal edip yeni kurulum başlatın.
- Sahip rolünde etkin oturumları kullanıcı, rol, son temas, bitiş ve geçerli oturum durumuyla inceleyin; geçerli olmayan bir oturumu kapatın.
- Üst çubuktaki **Kasayı kilitle ve oturumu kapat** ile açık tarayıcı profilini elle kilitleyin.

Bu sekmede kilit süresi ayarı, başarısız giriş kilitleme politikası veya güvenilir cihaz listesi yoktur. Otomatik kilit süresi sabit 15 dakikadır ve buradan değiştirilemez.

## Ana Parolayı Değiştirme

**Ana parolayı değiştir** formu açık olan kullanıcının kendi profilini değiştirir. Profil kilidi açık olmalı; mevcut ana parola girilmeli; yeni parola en az 14 karakter olmalı ve onayıyla eşleşmelidir. İstekler on dakikada en fazla altı parola değişimiyle sınırlandırılır.

Tarayıcı mevcut paroladan anahtar türetir, profil özel anahtarını yeni anahtarla yeniden şifreler ve 2FA açıksa ana parolayla şifreli TOTP kopyasını da yeniden şifreler. Sunucu mevcut doğrulayıcıyı kontrol eder, yeni doğrulayıcıyı ve şifreli materyali kaydeder. Düz metin ana parola sunucu profilinde saklanmaz.

Başarılı değişiklik `PASSWORD_CHANGE` denetim olayı üretir ve aynı kullanıcıya ait diğer kalıcı sunucu oturumlarını kapatır; işlemi yapan mevcut oturum açık kalır. Formun başarılı mesajı **profil anahtarları yeniden sarıldı** ifadesini kullanır. Bu işlem başka kullanıcının geçici parolasını belirlemek, profili sıfırlamak veya unutulmuş ana parolayı kurtarmak değildir.

## 2FA Durumları ve Kurulum

### 2FA kapalı / Kurulum bekliyor

**2FA kurulumunu başlat**, tarayıcıda yeni bir TOTP sırrı üretir. **Yeni QR oluştur**, henüz kaydedilmemiş sırrı yenisiyle değiştirir; eski QR bu aşamada etkin bir bağ değildir. Kurulum kartında QR kodu, biçimlendirilmiş manuel anahtar ve altı haneli kod alanı görünür.

QR oluşturulurken iskelet gösterilir. QR üretilemezse hata görünür; manuel anahtar ekranda kalabilir. QR veya manuel anahtar çok hassastır. Kodu authenticator uygulamasına ekledikten sonra güncel altı haneli kodu girip **2FA etkinleştir** kullanın. Kod önce tarayıcıda, sonra sunucuda zaman toleransıyla doğrulanır; on dakikada en fazla 12 2FA güncelleme isteği kabul edilir.

Başarılı kurulumda TOTP sırrının bir kopyası kurtarma/yeniden şifreleme için ana paroladan türetilen anahtarla, ikinci kopyası giriş doğrulaması için sunucu anahtarıyla şifrelenir. Diğer kalıcı oturumlar kapatılır ve `TWO_FACTOR_ENABLE` denetim olayı yazılır. Bir sonraki normal kilit açmada authenticator kodu gerekir.

### 2FA aktif / Hazır veya Kontrol

**Aktif** bağda **Kilit ekranında kod istenir** görünür. Hem `serverTotpReady` hem ana parolayla şifreli TOTP kopyası varsa durum **Hazır / Çift şifreli kayıt** olur. Bunlardan biri eksikse **Kontrol / Kayıt kontrol ediliyor** görünür; bunu sağlıklı bağ saymayın.

2FA etkin olduğu hâlde sunucu doğrulama materyali eksik eski bir profil kilit ekranında reddedilir. Ekran, yönetici yedeğine dönmeyi veya profili sıfırlamayı söyler; e-posta, kurtarma kodu veya TOTP atlama seçeneği sunmaz.

### Kaydı iptal etme ve sıfırlama sınırı

**Kaydı iptal et**, onaydan sonra açık profilin authenticator bağını kaldırır, diğer kalıcı oturumlarını kapatır ve `TWO_FACTOR_DISABLE` denetim olayı yazar. Geçerli oturum açık kalır. Bu, yeni cihaz için 2FA kurulumunu yeniden başlatmaya izin verir; mevcut TOTP sırrını göstermez veya kurtarma kodu üretmez.

Kullanıcı kilitliyken ve authenticator cihazına erişemiyorken bu kendi kendine iptal kullanılamaz; profilin zaten açık ve sunucu oturumunun doğrulanmış olması gerekir. İlk Sahip, **Kullanıcılar** ekranında yalnız başka ve Sahip olmayan bir kullanıcının 2FA bağını sıfırlayabilir. Kendi hesabı veya Sahip hesabı için bu yönetim işlemi kullanılamaz.

## Etkin Oturumlar

**Aktif oturumlar** yalnız Sahip için yüklenir ve güvenlik sekmesi açıkken yaklaşık 15 saniyede bir yenilenir. **Yenile** ile anlık sorgu yapılabilir. Liste yalnız kuruluşun etkin kullanıcılarına ait süresi dolmamış sunucu oturumlarını gösterir; süresi dolan kayıtlar sorgu sırasında temizlenir.

Özet; toplam etkin, **bu tarayıcı** ve **kapatılabilir** sayısını verir. Her satırda 18 karakterlik genel oturum kimliği, kullanıcı/görünen ad, rol, son temas, bitiş, durum ve işlem bulunur. IP adresi, tarayıcı adı veya cihaz parmak izi gösterilmez; yalnız bu tabloya bakarak fiziksel cihazı kesin tanımlamayın.

Geçerli satır **Bu oturum** olarak işaretlenir ve **Kapat** düğmesi devre dışıdır. Başka bir satırdaki **Kapat** doğrudan iptal isteği gönderir; ikinci bir onay penceresi yoktur. Başarılı işlem oturumu siler, listeyi ve denetimi yeniler ve `SESSION_REVOKE` olayı üretir. Oturum kimliğini veya kullanıcı adını herkese açık kanıta koymayın.

Liste yüklenirken üç iskelet satırı görünür. Ayrı bir sorgu hata kartı yoktur; liste isteği başarısız olup veri yoksa **Listelenebilir aktif oturum yok** boş durumu görülebilir. Bu mesajı kesin olarak oturum olmadığı kanıtı saymadan önce **Yenile**, sunucu bağlantısı ve Sahip oturumunu doğrulayın.

## Elle Kilitleme, Otomatik Kilit ve Hızlı Yeniden Açma

Üst çubuktaki **Kasayı kilitle ve oturumu kapat**; açık/kopyalanmış kayıt durumunu, oluşturulan paylaşım paketini, kilit açma TOTP alanını, geçici 2FA kurulum sırrı/QR/kodunu, hızlı açma durumunu ve sorgu önbelleğini temizler. Tarayıcı anahtarlarını uygulama belleğinden kaldırır ve sunucu çıkışını en iyi çabayla çağırır. Paylaşım parolası, seçili paylaşım kayıtları ve paylaşım paketi meta verisi (`sharePackageMeta`) ise açıkça sıfırlanmaz; arayüz kilitlense de bu React durumu bellekte kalabilir.

Kasa 15 dakika tarayıcı etkinliği olmadığında otomatik kilitlenir. İşaretçi, klavye, kaydırma, odak ve görünürlük değişimleri sayacı yeniler. Süre dolduğunda açık/kopyalanmış durum, paylaşım paketi/parolası ve seçili paylaşım kayıtları, hızlı açma durumu, sunucu oturumu, sorgu önbelleği ve açık anahtarlar temizlenir. Elle kilitten farklı olarak paylaşım paketi meta verisi (`sharePackageMeta`) ile kilit açma ve geçici TOTP kurulum durumları açıkça sıfırlanmaz; kilit ekranı bunları gizler, ancak hassas paylaşım meta verisini, QR kodunu veya manuel anahtarı gösterdikten sonra otomatik kilidi temizlik adımı saymayın.

Görünür bir paylaşım veya TOTP akışını yarıda bıraktıysanız yalnız kilide güvenmeyin; tam sayfa yeniden yükleme yapın.

Normal kilit açmadan sonra 15 dakikalık hızlı yeniden açma kopyası SharedWorker/Service Worker çalışma zamanı belleğinde tutulabilir; geri yükleme belirteci tarayıcı geçmiş durumunda bulunur. Eski IndexedDB hızlı açma kalıntıları yalnız silinir. Bu hat, ana parolayı veya ana paroladan türetilmiş anahtarı kalıcı tarayıcı depolamasına yazmaz. Elle veya otomatik kilit hızlı açma kopyasını temizler.

## Parola, Profil Sıfırlama ve Kurtarma Sınırları

- **Ana parolayı değiştir**, açık kullanıcının mevcut profil anahtarlarını yeni parolaya yeniden sarar; veriyi silmez.
- **Kullanıcılar > Parola belirle**, yalnız ilk Sahip tarafından başka, Sahip olmayan bir kullanıcı için yürütülen ayrı işlemdir. Hedefin oturumlarını kapatır, 2FA'sını sıfırlar ve kişisel kasa anahtarını yeni geçici parolaya göre yeniden sarar.
- **Sunucu profilini sıfırla**, Giriş güvenliği sekmesindeki bir kontrol değildir. Ayrı ve yıkıcı Sahip API ucu, doğrulanmış Sahip oturumu ile tam `DELETE_LOCAL_PROFILE` ifadesini ister; kuruluşu, kullanıcıları, kasaları, sırları, paylaşım/entegrasyon/dizin kayıtlarını, denetimi ve bütün sunucu oturumlarını siler. Bu işlem unutulmuş parola için hafif bir sıfırlama değildir.
- Kilit ekranındaki kurtarma mesajı önce ana parola, Caps Lock ve TOTP kodunu kontrol etmeyi; sunucu/profil sorunu sürerse VaultPilot Backup Tool yedeğine dönmeyi söyler. Destek ana parolayı, TOTP sırrını veya oturum çerezini bilmez ve istememelidir.

Geçerli tarayıcı akışında e-posta ile parola sıfırlama, kurtarma kodu, SMS, IdP yönlendirmesi veya destek tarafından kimlik doğrulama atlama yoktur.

## Önerilen İş Akışları

### İlk 2FA bağını kurma

1. Profil kilidinin açık, sunucu oturumunun doğrulanmış ve lisansın yazılabilir olduğunu doğrulayın.
2. **2FA kurulumunu başlat** seçeneğini kullanın.
3. QR kodu authenticator uygulamasıyla tarayın veya manuel anahtarı doğrudan uygulamaya girin; ekran görüntüsü almayın.
4. Uygulamadaki güncel altı haneli kodu girip **2FA etkinleştir** kullanın.
5. Durumun **Aktif** ve **Hazır / Çift şifreli kayıt** olduğunu doğrulayın.
6. Kontrollü bir kilitlemeden sonra kullanıcı adı, ana parola ve yeni TOTP koduyla kilidi açmayı doğrulayın.

### Şüpheli eski bir oturumu kapatma

1. Sahip rolüyle **Aktif oturumlar** listesini yenileyin.
2. Kullanıcı, rol, son temas ve bitiş zamanını karşılaştırın; cihaz/IP bilgisi olmadığını unutmayın.
3. **Bu oturum** satırını değil, kapatılması onaylanan diğer satırı seçin.
4. **Kapat** seçeneğinin ikinci onay istemeden işlem yaptığını dikkate alıp düğmeyi bir kez kullanın.
5. Listenin ve `SESSION_REVOKE` denetim kaydının yenilendiğini doğrulayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| 2FA kapalı / Kurulum bekliyor | Yeni bağ oluşturun; QR veya manuel anahtarı gizli tutun. |
| QR oluşturuluyor | İskeletin tamamlanmasını bekleyin; yeniden tekrar tekrar QR üretmeyin. |
| QR oluşturulamadı | Manuel anahtar varsa authenticator uygulamasına doğrudan girin; yoksa kurulumu yeniden başlatın. |
| Authenticator kodu doğrulanamadı | Altı hane, cihaz saati ve doğru hesabı kontrol edin; doğrulamayı atlamayın. |
| 2FA aktif / Hazır | Bağın çift şifreli materyali mevcut; kontrollü kilit açma testi yapın. |
| 2FA aktif / Kontrol | Eksik bağ materyalini sağlıklı saymayın; kilitlemeden önce özel kurtarma/yedek planını doğrulayın. |
| Ana parola değiştiriliyor | İkinci gönderim yapmayın; sonuç veya hata mesajını bekleyin. |
| Mevcut parola doğrulanamadı | Doğru profil/parola ve Caps Lock durumunu kontrol edin; profil sıfırlamaya acele etmeyin. |
| Oturumlar yükleniyor | Üç iskelet satırının tamamlanmasını bekleyin. |
| Listelenebilir aktif oturum yok | Sorgu hatası için ayrı kart olmadığından bağlantıyı ve Sahip rolünü doğrulayıp yenileyin. |
| Oturum kapatılamadı | Geçerli satırı seçmediğinizi, Sahip rolünü ve sunucu bağlantısını doğrulayın. |
| Kasa otomatik kilitlendi | Ana parola ve gerekiyorsa TOTP ile yeniden açın; hızlı açmanın temizlendiğini varsayın. |
| Sunucu oturumu doğrulanamadı | Hızlı açma bellekte 15 dakika korunabilir; bağlantı gelince otomatik yeniden denemeyi bekleyin. |
| Eski 2FA profili | Sunucu doğrulama materyali yoksa kodu atlamayın; yönetici yedeği veya onaylı profil kurtarma yolunu kullanın. |

## İşlemden Önce

- İşlemin kendi profilinize mi, başka kullanıcıya mı, yoksa bütün sunucu profiline mi etki ettiğini ayırın.
- Rolü ve lisansın yazılabilir durumunu doğrulayın; Denetçi formu görse bile profil yazamaz.
- 2FA QR kodu veya manuel anahtar görünürken ekran paylaşımını ve kaydı kapatın.
- Ana parola veya 2FA değişikliğinin diğer kalıcı oturumları kapatacağını planlayın.
- Oturum kapatma düğmesinde ikinci onay olmadığını ve geçerli oturumun tablodan kapatılamadığını unutmayın.
- 2FA bağını iptal etmeden veya profili sıfırlamadan önce onaylı yedek ve yeniden giriş yolunu doğrulayın.

## Güvenli Kanıt

- Paylaşılabilir: sistem rolü sınıfı, 2FA **kapalı/aktif/hazır/kontrol** durumu, toplam ve kapatılabilir oturum sayısı, yaklaşık son temas/bitiş aralığı, genel hata kategorisi ve geniş zaman aralığı.
- Gizli kalmalı: kullanıcı/görünen ad, ana parola ve türetilmiş doğrulayıcı, TOTP sırrı, QR kodu, altı haneli kod, şifreli TOTP/özel anahtar verisi, oturum kimliği/belirteci/çerezi, profil sıfırlama kimliği, yedek dosyası ve tam zaman damgası.
- Oturum tablosu cihaz parmak izi veya IP göstermez; kanıta bu alanları tahmin ederek eklemeyin.
- Ekran görüntüsünde manuel TOTP anahtarını yalnız bulanıklaştırmayın; tamamen maskeleyin ve görüntünün kopyalarında kalmadığını doğrulayın.

## Ne Zaman Durmalı ve Destek İstemelisiniz

2FA etkin ama bağ **Kontrol** durumundaysa, sunucu doğrulama materyali eksikse, yeni ana parolayla profil özel anahtarı açılamıyorsa, başka oturumlar değişiklik sonrası etkin kalıyorsa, oturum listesi beklenmedik kullanıcı gösteriyorsa veya otomatik kilit hassas ekran durumunu temizlemiyorsa yeni güvenlik değişikliği yapmayı bırakın. Gizli değer eklemeden rol sınıfı, genel durum, geniş zaman aralığı, hata kodu ve son güvenli adımla özel destek kaydı açın.

## Operatör Notları

Giriş güvenliği bir kimlik sağlayıcısı veya e-posta hesabı yönetim ekranı değildir. Ana parola, TOTP ve oturum yönetimi VaultPilot sunucusundaki profil ve tarayıcı belleği sınırlarında çalışır. Kurtarma kodu, TOTP sırrı, ana parola, kimlik doğrulama karması, çerez veya tek kullanımlık kod gösteren kanıt yayımlamayın.

## İlgili

- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Kullanıcılar ekranı](screen-users.md)
- [Sunucu ayarları ekranı](screen-server-settings.md)
- [Giriş sonrası 401 KB](../../kb/tr/session-401-after-login.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
