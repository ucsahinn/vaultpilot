# Güncellemeler Ekranı

Üst çubuktaki `?`, Güncellemeler ekranına ait bu rehberi açar. Bu ekran VaultPilot sunucu MSI paketinin yerel veya imzalı uzak kanıtını denetler, uygun pakette kurulum işi başlatır ve Windows Installer ile servis yeniden başlatma ilerlemesini izler. Bir yayın oluşturma, etiketleme, dosya yükleme veya yayımlama aracı değildir.

## Erişim, Rol ve Lisans Sınırı

**Otomatik güncelleme** özelliği, Güncellemeler görünümü için istemci arayüzündeki gezinme kapısıdır. Özellik açıksa Sahip, Yönetici ve Denetçi ekranı ve mevcut sunucu durumunu görebilir; Kullanıcı sistem görünümüne erişemez. Salt okunur lisans özellik görünümünü açmadığı için bu modda normal gezinme de engellenir. Mevcut durum, iş, kontrol ve başlatma API uçları `auto-update` özelliğini ayrıca sunucu tarafında denetlemez; bu uygulama ayrıntısı erişim kapısını aşma yetkisi vermez.

**Canlı denetle** uzak GitHub manifestini okumak için Sahip veya Yönetici rolü ister ve on dakikada en fazla on istek kabul eder. Kontrol API ucu salt okunur lisansı ayrıca reddetmez. Yalnız durum başarıyla döndükten sonra `UPDATE_CHECK` denetim olayı yazılır; manifest indirme veya ayrıştırma hatası sonuç üretmez ve bu denetim olayını oluşturmaz. Normal özellik kapısını doğrudan istekle aşmaya çalışmayın.

Sunucu MSI kurulumunda sunucu tarafındaki kesin yetki **Sahip** rolüdür. Arayüzde bir düğme görünse bile Yönetici sunucu kurulumunu başlatmaya yetkili sayılmaz. Lisans salt okunursa Sahip için de kurulum başlangıcı reddedilir. Denetçi yalnız görüntüler; paket kontrolü veya kurulum başlatamaz.

## Burada Ne Yapılır

- Yerel sunucu sürümünü, hedef sürümü, kartın gösterdiği paket/URL adını, boyutu, SHA-256 özetini ve doğrulama adımlarını inceleyin.
- **Doğrulama adımları** ile paketin neden **Güncel**, **Hazır** veya **İşlem gerekli** olduğunu okuyun.
- **Canlı denetle** ile yapılandırılmış uzak güncelleme manifestini yeniden alın ve imza/paket kanıtını doğrulayın.
- Kanıt uygunsa Sahip rolüyle **Sunucu MSI kur** seçeneğini kullanın.
- Kurulum sırasında yüzde, son kayıttan bu yana geçen süre, hedef sürüm, adımlar ve **Gelişmiş teknik log** özetini izleyin.
- Kurulum tamamlanınca çalışan sürümün hedef sürümle eşleşmesini ve konsolun yeniden bağlanmasını doğrulayın.

Bu ekranda güncelleme işini iptal etme düğmesi veya genel **Yeniden dene** işlemi yoktur. Engellenmiş iş korunur. Kök nedeni düzeltip kanıtı yeniden doğruladıktan sonra kurulum düğmesini tekrar kullanmak, eski işi devam ettirmek yerine yeni bir iş başlatır.

## Bileşen ve Sürüm Yüzeyleri

Ekrandaki tek kurulum kartı **VaultPilot server** MSI hattıdır. Kart; **Artefakt**, **Güncel sürüm**, **Paket boyutu** ve varsa SHA-256 gösterir. **Artefakt** metni bilinen `fileName` alanından değil `packageUrl` adresinin son bölümünden türetilir; URL yoksa sunucu dosya adını biliyor olsa bile **Paket yolu bekleniyor** görünür. Normal sunucu durumunda ayrı bir manifest adresi satırı yoktur. Paket URL'si açılmışsa **MSI indir** bağlantısı görünür.

Tarayıcı eklentisi müşteri kurulum ve güncellemelerini Chrome Web Store üzerinden alır; bu ekran ayrı bir eklenti kurulum işi oluşturmaz. Offline Share Decrypter, DC Agent ve başka bileşenler gömülü **Sürüm notları** içinde anılabilir, ancak burada ayrı kurulum kartı veya iş hattı değildir.

**Sürüm notları** bu konsol paketine gömülü zaman çizelgesidir; sürüm, bileşen ve not sayılarını gösterir. Üst çubuktaki en son GitHub sürüm özeti ayrı, bilgilendirici bir sorgudur. GitHub yanıtı yokken üst çubuktaki sürüm akışı yerel uygulama sürümünü kullanıp **yayınlandı** diyebilir; bu yedek metin dış yayın kanıtı değildir. Gömülü not, üst çubuk akışı, en son sürüm özeti veya **Canlı denetle** sonucu tek başına bir yayının oluşturulduğunu, yayımlandığını ya da bütün dosyalarının hazır olduğunu kanıtlamaz.

## Yerel Durum ve Canlı Denetim

Ekran ilk olarak sunucudaki yerel durumu okur:

- Sürümlü, uygun bir MSI yoksa çalışan sürümü **Güncel** gösterir ve kurulum başlatmaz.
- Daha yeni, sürümü belirli yerel MSI bulunduğunda paket boyutu ve SHA-256 değeri hesaplanır; sürüm amacı uygunsa paket **Hazır** olabilir. Bu yalnız yerel ön denetimdir.
- Daha eski paket, sürümü belirlenemeyen paket veya aynı sürüm onarım paketi otomatik kurulum için **İşlem gerekli** durumuna alınır. Aynı sürüm onarımı manuel MSI Repair akışına aittir.

**Canlı denetle**, yapılandırılmış HTTPS GitHub manifestini sunucudan okur. Başarılı denetim, imzalı manifestin doğrulandığını ve sunucu MSI varlığının/uygunluğunun değerlendirildiğini gösterir. İmza anahtarı eksik veya doğrulama başarısızsa uzak paket adresleri açılmaz ve indirme adımı engellenir. Yerel paket bulunduğuna dair bilgi paneli görünebilir; ancak uzak durum `BLOCKED` iken ekran ayrı bir yerel paket kartı veya indirme bağlantısı oluşturmaz.

Uzak bağlantı veya en son sürüm sorgusu başarısız olduğunda ekran yayın oluşturmaz, manifesti değiştirmez ve yerel paketi otomatik olarak uzak paket saymaz. Yerel paket kendi sürüm/SHA ön denetimi ve kurulum işi içindeki Authenticode kontrolüyle ayrı değerlendirilir.

## Paket ve İmza Doğrulaması

Uzak otomatik kurulumda sıralı güvenlik sınırı şöyledir:

1. Manifest, yapılandırılmış veya paketle gelen yayın açık anahtarıyla Ed25519 imzası üzerinden doğrulanır.
2. Sunucu varlığı, manifestteki izinli HTTPS adresi, dosya adı, sürüm ve beklenen boyutla eşleştirilir.
3. İndirme sunucuda sınırlı boyutla yapılır ve hesaplanan SHA-256, manifestteki tam değerle karşılaştırılır.
4. MSI Authenticode bilgisi Windows üzerinde okunur. Manifest imzalayan sertifikanın SHA-1 parmak izini sabitlemişse MSI imzacısı bununla eşleşmelidir; sabitlenmemiş uzak pakette Windows imza durumu geçerli olmalıdır.
5. Bu denetimler geçmeden sessiz Windows Installer adımı başlatılmaz.

Yerel hazırlanmış MSI'ın kart durumu sürüm amacını, dosya varlığını/boyutunu ve hesaplanan SHA-256 değerini önceden denetler. Bu yerel `READY` değerlendirmesi manifest Ed25519 imzası doğrulamaz ve MSI Authenticode imzasını henüz kontrol etmez; Authenticode, kurulum işi başladıktan sonra doğrulanır. Üretim ortamında imzasız kurulum için belge veya ekran üzerinden bir atlama yolu yoktur. Yerel **Hazır**, yalnız bu ön koşulların geçtiğini gösterir; kurulum veya imza doğrulaması tamamlandı anlamına gelmez.

Kart SHA-256 değerinin yalnız başlangıç bölümünü görünür metinde gösterir; tam değer öğe ayrıntısında bulunabilir. Görünen kısaltmayı tam eşleşme kanıtı saymayın.

## Paket ve İş Durumları

### Paket durumu

| Durum | Anlamı |
| --- | --- |
| **Güncel** (`CURRENT`) | Çalışan sürüm için kurulabilir yeni yerel/uzak MSI yoktur. |
| **Hazır** (`READY`) | Uzak pakette imzalı manifest kanıtı, yerel pakette ise sürüm ve SHA-256 ön denetimi uygundur. Yerel Authenticode denetimi iş sırasında yapılır. |
| **İşlem gerekli** (`ACTION_REQUIRED`) | İmza anahtarı, manifest, varlık, sürüm amacı veya başka paket kanıtı eksik/uygunsuzdur. Engelli adımı okuyun. |

### Güncelleme işi durumu

| Durum | Anlamı |
| --- | --- |
| `QUEUED` | Şema ve eski/kayıtlı iş uyumluluğu için tanınır; güncel başlatma akışı bu durumu üretmez. Görülürse aktif kabul edilir. |
| `RUNNING` | İndirme, doğrulama, MSI veya yeniden başlatma aşaması ilerliyor. |
| `BLOCKED` | Bir güvenlik, paket, Windows Installer, UAC veya yeniden bağlanma adımı işi durdurdu. Bu akışta ayrı `FAILED` iş durumu yoktur. |
| `READY` | Şema uyumluluğu için tanınır; güncel başlatma akışı bu iş durumunu üretmez ve kurulum tamamlandı anlamına gelmez. |
| `COMPLETED` | Çalışan VaultPilot sürümü hedef sürümle eşleşecek şekilde iş tamamlandı. |

Güncel başlatma yolu yeni işi doğrudan `RUNNING`, `BLOCKED` veya `COMPLETED` olarak yazar. İş başlangıcı isteği kayıt oluşturulmadan hata verirse ekranda **Güncelleme işlemi başlatılamadı** görünür; bu, kalıcı bir `FAILED` iş satırı değildir. Sunucu en fazla 12 güncelleme işini listeler; aktif işler önce, ardından son güncellenen tamamlanmış veya engellenmiş işler gelir.

## Adımlar ve Teknik Log

Doğrulama ve iş adımları `DONE`, `RUNNING`, `PENDING` veya `BLOCKED` olabilir. Sunucu MSI akışında görülebilecek adımlar şunları kapsar:

- kurulu sürümü okuma ve hedef sürümü kabul etme,
- yerel paketi seçme veya doğrulanmış MSI'ı sunucuya indirme,
- indirilen SHA-256 değerini doğrulama,
- MSI Authenticode imzasını doğrulama ve durumunu kaydetme,
- sessiz Windows Installer çalıştırma,
- VaultPilotServer servisini yeniden başlatma ve hedef sürümü bekleme.

Karttaki **Doğrulama adımları** paket durumuna veya seçili işin adımlarına dayanır. Aktif iş varsa ayrıca **Gelişmiş teknik log** bütün iş adımlarını durum, etiket ve isteğe bağlı ayrıntıyla listeler. Bu bölüm ham PowerShell, MSI veya Windows Event Log değildir. Yerel yolların sunucu yanıtına sızmasını azaltmak için bazı yükleyici ayrıntıları redakte edilir; yine de her satırı paylaşmadan önce inceleyin.

## Kurulum, UAC ve Servis Yeniden Başlatma

Sunucu kurulumu sessiz `msiexec` akışını yeniden başlatma istemlerini bastırarak çalıştırır, ardından VaultPilotServer servisini ayrı bir yardımcıyla yeniden başlatır. Kurulum sırasında tarayıcı bağlantısı kesilebilir. Konsol, sağlık ve sürüm sinyali geri geldiğinde hedef sürümle otomatik yeniden yüklenmeye çalışır.

Yükleyici yardımcısı yönetici yetkisi gerektirirse sunucu Windows UAC yükseltmesi isteyebilir. Bu istem tarayıcıda değil Windows sunucu oturumunda görülür. Onay verilmezse veya yükseltilmiş yardımcı başlatılamazsa iş yaklaşık MSI aşamasında **BLOCKED** olur. Kurulumu yetkili bir Windows yönetici oturumu ve onaylı bakım penceresi olmadan başlatmayın.

Güncellemeler ekranı bakım penceresi planlamaz, yedek oluşturmaz ve kullanıcı oturumlarını koordine etmez. Başlatmadan önce onaylı yedeği, kısa servis kesintisini, kullanıcı iletişimini ve geri dönüş yolunu işletim prosedürünüzde hazırlayın.

## Engellenme ve Kurtarma

Kalıcı güncelleme işleri sayfa yenilendiğinde veya servis geri geldiğinde yeniden okunur. Sunucu çalışan `RUNNING` işi yükleyici yardımcısı günlüğü ve çalışan sürümle uzlaştırır:

- Hedef sürüm zaten çalışıyorsa iş `COMPLETED` yapılabilir.
- MSI tamamlanmış ancak servis hedef sürümle dönmemişse yeniden başlatma adımı bekler; zaman aşımında `BLOCKED` olur.
- Yükleyici yardımcısı başlangıç sinyali yazmazsa iş yaklaşık `%76` düzeyinde engellenebilir.
- Yardımcı başlamış ancak MSI tamamlanma/çıkış kodu gelmemişse iş yaklaşık `%82` düzeyinde engellenebilir.
- MSI tamamlandıktan sonra hedef sürüm zamanında doğrulanamazsa iş yaklaşık `%96` düzeyinde engellenebilir.

Yüzdenin birkaç dakika aynı kalması tek başına takılma kanıtı değildir. Son kayıttan bu yana geçen süre kısa ve yeni sinyal geliyorsa işi bekleyin. Sayfa yenilendikten sonra kurtarılan aktif iş kartta görünebilir, ancak oturum içi aktif iş sinyali yeniden kurulmadıysa otomatik sorgulama kendiliğinden devam etmeyebilir. Pencereye yeniden odaklanın veya tarayıcı sayfasını yenileyerek yeni iş anlık görüntüsünü alın; **Canlı denetle** paket kontrolüdür, iş yenileme düğmesi değildir. Yeni iş başlatmadan önce Güncellemeler ve İşlemler ekranlarında aktif kayıt bulunmadığını doğrulayın.

İptal denetimi yoktur. `BLOCKED` işi veritabanından düzenlemeyin, paketi doğrulamasız değiştirmeyin ve imza kontrolünü atlamayın. Kanıtı koruyun, kök nedeni düzeltin, **Canlı denetle** veya yerel kanıtla durumu yeniden doğrulayın ve yalnız sonra yeni bir kurulum işi başlatın.

## Önerilen İş Akışları

### Uzak imzalı MSI kurulumunu doğrulama

1. Bakım penceresi, yedek, geri dönüş ve sunucu yönetici erişimini hazırlayın.
2. **Canlı denetle** kullanın; manifest imzası ve paket adımlarının engellenmediğini doğrulayın.
3. Dosya adı, hedef sürüm, boyut, tam SHA-256 ve imzacı kanıtını bağımsız yayın kanıtıyla karşılaştırın.
4. Paket **Hazır** ise Sahip rolüyle **Sunucu MSI kur** seçeneğini kullanın.
5. İndirme, SHA-256, Authenticode, MSI ve yeniden başlatma adımlarını izleyin.
6. Konsol geri geldiğinde çalışan sürümü, servis sağlığını ve terminal iş durumunu doğrulayın.

### Engellenmiş işi inceleme

1. `BLOCKED` işte ilk engellenen adımı ve son kayıt zamanını belirleyin.
2. Manifest/imza/hash engeli ile Windows Installer/UAC/servis engelini birbirinden ayırın.
3. Paket veya güven ayarını değiştirmeden önce redakte kanıtı koruyun.
4. Gerekirse yüzde 76 bilgi bankasını ve Windows Installer/VaultPilot servis kanıtını kullanın.
5. Kök neden düzelmeden yeni iş başlatmayın; düzeltme sonrası durumu yeniden denetleyin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Yükleniyor | İki iskelet satırı görünür; geçici boşluğu kesin paket durumu saymayın. |
| Güncelleme durumu okunamadı | Kasa/oturum, rol, otomatik güncelleme lisansı ve sunucu bağlantısını doğrulayın. |
| Güncel | Yeni otomatik MSI işi yoktur; gömülü sürüm notunu yayın kanıtı saymayın. |
| Hazır | Sürüm, manifest, tam SHA-256, imzacı ve bakım penceresini doğruladıktan sonra Sahip başlatabilir. |
| İşlem gerekli | İlk `BLOCKED` doğrulama adımını giderin; indirme veya kurulumu zorlamayın. |
| Kontrol çalışıyor | İkinci canlı denetim başlatmayın; sonuç veya uyarıyı bekleyin. |
| Kurulum sürüyor | Yüzde ile birlikte son kayıttan bu yana geçen süreyi izleyin; servis bağlantı kesintisine hazır olun. |
| UAC bekleniyor | Windows sunucu oturumunda onayı değerlendirin; beklenmeyen istemi kabul etmeyin. |
| Yüzde 76/82 civarında sabit | Yeni kayıt geliyorsa bekleyin; zaman aşımı veya `BLOCKED` oluşursa ilgili yükleyici kanıtını inceleyin. |
| Yüzde 96 civarında sabit | MSI sonucu ile çalışan servis sürümünü karşılaştırın; hedef sürüm gelmeden tamamlandı saymayın. |
| Blocked | Engellenen adımı ve redakte ayrıntıyı koruyun; otomatik yeniden deneme beklemeyin. |
| Completed | Çalışan sürüm ve servis sağlığı hedefle eşleşiyorsa tamamlandı kabul edin. |
| Konsol bağlantısı kesildi | Beklenen bakım penceresinde sağlık sinyalini bekleyin; bağlantı gelince pencereye odaklanın veya sayfayı yenileyin, hemen ikinci kurulum başlatmayın. |

## İşlemden Önce

- Sahip rolünü, otomatik güncelleme lisans özelliğini ve lisansın yazılabilir olduğunu doğrulayın.
- Onaylı bakım penceresi, güncel yedek, geri dönüş yöntemi ve Windows yönetici erişimini hazırlayın.
- Yerel ve uzak kaynakları karıştırmayın; karttaki `LOCAL` veya `GITHUB_RELEASE` kaynağını ve hedef sürümü doğrulayın.
- Uzak pakette manifest imzasını, izinli paket adresini, dosya adını/boyutunu, tam SHA-256 değerini ve Authenticode imzacısını birlikte değerlendirin; yerel `READY` durumunda Authenticode'un iş sırasında doğrulanacağını unutmayın.
- Aktif `QUEUED` veya `RUNNING` iş olmadığını Güncellemeler ve İşlemler ekranlarında kontrol edin.
- Canlı denetim, sürüm notu veya en son sürüm özetinin yayın oluşturmadığını ve kurulum başarısını kanıtlamadığını unutmayın.

## Güvenli Kanıt

- Paylaşılabilir: genel kaynak türü, bileşen, sürüm/etiket, herkese açık paket adı ve boyutu, beklenen/gözlenen SHA-256 eşleşme durumu, Authenticode durumu veya imzacı özeti, adım durumu, geniş zaman aralığı ve redakte hata kategorisi.
- Gizli kalmalı: yerel indirme/hazırlama yolu, sunucu adı ve kullanıcı adı, iş kimliği, özel manifest veya destek bağlantısı, kopyalanmış MSI, ham PowerShell/MSI/Windows olay günlükleri, destek paketi, ortam değerleri, lisans verisi ve imzalama özel anahtarı/sertifika dosyası.
- Herkese açık bir yayın dosyasının tam SHA-256 değeri ve imzacı parmak izi paylaşılabilir kanıt olabilir; bunun gerçekten herkese açık varlığa ait olduğunu doğrulamadan dahili paket kanıtını yayımlamayın.
- Ekran görüntüsünde paket URL'sinden türetilen artefakt metnini, teknik adım ayrıntısını ve son kayıt zamanını ayrı ayrı inceleyip gerekli alanları maskeleyin; normal kartta manifest adresi bulunduğunu varsaymayın.

## Ne Zaman Durmalı ve Destek İstemelisiniz

Manifest imzası doğrulanmıyorsa, SHA-256 veya boyut uyuşmuyorsa, Authenticode imzacısı beklenen kanıtla eşleşmiyorsa, beklenmeyen UAC istemi çıkıyorsa, MSI geri alınıyorsa, servis hedef sürümle dönmüyorsa veya iş uzlaştırma sonrası `BLOCKED` kalıyorsa kurulumu durdurun. Paket değiştirmeden veya yeni iş başlatmadan; sürüm, kaynak sınıfı, adım adı, geniş zaman aralığı, genel hata kodu ve redakte imza/SHA-256 durumuyla özel destek kaydı açın.

## Operatör Notları

Güncellemeler ekranı tüketici taraftaki doğrulama ve kurulum yüzeyidir. GitHub sürümü, manifesti, MSI'ı veya başka bileşen varlığını oluşturmaz, imzalamaz, yüklemez, etiketlemez ya da yayımlamaz. Gömülü sürüm notları da dış yayın durumunun canlı kaynağı değildir.

## İlgili

- [Güncelleme Merkezi](update-center.md)
- [Yayın dosyası doğrulama](release-asset-verification.md)
- [İşlemler ekranı](screen-executions.md)
- [Sunucu ayarları ekranı](screen-server-settings.md)
- [Update yüzde 76 civarında takılıyor KB](../../kb/tr/update-stuck-76.md)
