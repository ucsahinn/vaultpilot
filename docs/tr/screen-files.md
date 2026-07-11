# Dosyalar Ekranı

Üst çubuktaki `?` bu rehberi **Dosyalar** ekranından açar. Bu ekran, etkin kasadaki `FILE` türü kayıtları yönetir; genel amaçlı bir belge arşivi, ağ paylaşımı veya bulut depolama istemcisi değildir.

## Erişim ve Lisans Sınırı

Dosyalar ekranı, Denetçi dışındaki sistem rollerine yalnızca kendilerine atanmış ve tarayıcı oturumunda kilidi açılmış kasalar için görünür. **Görüntüleyici**, **Düzenleyici** ve **Yönetici** kasa rolleri dosya kayıtlarını listeleyebilir ve indirebilir. Denetçi rolünün gizli kayıtlara veya kasa anahtarına erişimi yoktur.

Yeni dosya oluşturma, dosya değiştirme, kopya oluşturma, kayıt bilgilerini düzenleme ve silme için yazılabilir lisans ile etkin kasada **Düzenleyici** veya **Yönetici** rolü gerekir. Görüntüleyici rolü ve salt okunur lisans bu yazma işlemlerini kapatır; mevcut bir dosyayı indirme yolunu kapatmaz. Dosyalar ekranının ayrı bir lisans modülü yoktur. **Toplu paylaş** ile açılan paylaşım akışında ise lisansın **Paylaşım** yeteneği ve Paylaşım ekranının daha dar rol koşulları ayrıca uygulanır.

## Burada Ne Yapılır

- **Dosyalarda ara** ile etkin kasanın dosya kayıtlarında arayın.
- **Akıllı filtre ekle** ile içe aktarılan, uyarı taşıyan, kategori, etiket veya ürün bilgisi eşleşen kayıtları birlikte süzün.
- **Tümü** hızlı filtresine dönün; **Kart** veya **Tablo** görünümünü seçin ve **Yenile** ile kasa listesini yeniden alın.
- Yazma yetkiniz varsa **Yeni dosya** ile şifreli dosya kaydı oluşturun.
- Satırda dosya adı, boyut, parça sayısı, kısaltılmış SHA-256 özeti ve son güncelleme zamanını inceleyin.
- **Dosyayı indir** ile parçaları tarayıcıda çözüp dosyayı indirin.
- **VirusTotal SHA-256 araması** ile yalnız dosya özetini VirusTotal üzerinde arayın.
- **Diğer işlemler** içinden **Kopyasını oluştur**, **Kaydı düzenle** veya **Kaydı sil** işlemini başlatın.
- Satırları seçip **Toplu işlemler** menüsünden dosya kayıtlarına uygulanabilen işlemleri yürütün.

## Dosya Boyutu, Parçalar ve Şifreleme Sınırı

Seçilen tek dosya 1 GB'ı aşamaz. Sunucu ayrıca geçerli kullanıcının etkin kasaya yazdığı şifreli dosya parçalarının toplamını kullanıcı ve kasa başına 1 GB ile sınırlar; bu nedenle 1 GB'tan küçük bir dosya da kullanılabilir alan yetersizse reddedilebilir. Dosyalar ekranı tam olarak ne kadar alan kaldığını göstermez; sınır, parçalar yazılırken sunucu tarafından uygulanır.

VaultPilot dosyayı 2 MB'lık en fazla 512 parça halinde işler. Kaydetme sırasında SHA-256 özeti tarayıcıda hesaplanır; dosya her parça için etkin kasa anahtarıyla tarayıcıda şifrelenir. Sunucu şifreli parçaları, parça sırasını ve kota için gereken boyut bilgisini saklar. Dosya içeriğini ayrı bir bulut nesne deposuna yüklemez ve sunucu tarafında düz metin dosya olarak tutmaz.

Dosya satırındaki parça sayısı ve boyut, kayıt meta verisidir. Kısaltılmış SHA-256 değeri dosyanın kimliğini doğrulamaya yardımcı olur; gizli dosya içeriğinin güvenli biçimde paylaşılabileceği anlamına gelmez.

## Yeni Dosya Oluşturma

1. Yazılabilir ve doğru kasanın etkin olduğunu doğrulayın.
2. **Yeni dosya** düğmesini seçin.
3. Zorunlu **Başlık** alanını doldurun.
4. İsteğe bağlı olarak **Sahip veya teslim alan**, **İlgili sistem veya talep kaydı** ve **Dosya notu** alanlarını doldurun.
5. **Dosya seç** ile tek dosyayı seçin. Ekran dosya adını, boyutu ve hesaplanacak parça sayısını gösterir; başlık boşsa dosya adını başlık olarak kullanır.
6. **Şifreli kaydı kaydet** ile işlemi başlatın. İlerleme alanı önce şifreli kayıt verisinin kaydını, ardından dosya parçalarının şifrelenip yüklendiğini gösterir.
7. İşlem tamamlanınca Dosyalar listesinde dosya adını, boyutu, parça sayısını ve SHA-256 özetini doğrulayın.

Dosya seçimi zorunludur. 1 GB sınırı aşılırsa seçim temizlenir. Kasa kilitli, rol yetersiz, lisans salt okunur veya kullanıcı/kasa kotası doluysa kayıt tamamlanmaz.

## Düzenleme, Değiştirme, Kopyalama ve Silme

**Kaydı düzenle**, mevcut başlık, sahip, ilgili sistem ve not bilgilerini açar. Dosyayı değiştirmek zorunlu değildir. **Dosyayı değiştir** ile yeni bir dosya seçerseniz kayıt meta verisi yeniden şifrelenir, eski parçalar temizlenir ve yeni dosya 2 MB'lık parçalar halinde yüklenir. Kaydetme sırasında sayfadan ayrılmayın.

**Kopyasını oluştur** bir pano işlemi değildir. VaultPilot kaynak parçaları etkin kasa anahtarıyla tarayıcıda çözer, yeni kayıt için yeniden şifreler ve aynı kasada ayrı bir dosya kaydı oluşturur. Kaynak parçalar eksikse kopya oluşturulmaz; eksik hazırlanmış yeni kopya kaydı temizlenmeye çalışılır.

**Kaydı sil**, onaydan sonra dosya kaydını ve ona bağlı şifreli parçaları sunucu kasasından kalıcı olarak kaldırır. İşlem geri alınamaz. Toplu silme de ayrı onay ister; işlem kısmen başarısız olursa listedeki kalan kayıtları yenileyip yeniden değerlendirin.

## İndirme, Gösterme, Kopyalama ve Denetim Davranışı

Dosya satırında **Gizli değeri göster** veya **Gizli değeri kopyala** işlemi yoktur. Dosya içeriği satırda ya da panoda açılmaz. **Dosyayı indir**, sunucudan şifreli parçaları sırasıyla alır, beklenen parça sayısını doğrular, parçaları etkin kasa anahtarıyla tarayıcıda çözer ve tarayıcının indirme akışına verir. İndirme için kasanın kilidi açık olmalıdır.

Sunucu, dosya parça listesini başarıyla döndürdüğünde; arayüz beklenen parça sayısını doğrulamadan, parçaları çözmeden veya tarayıcı indirmesini başlatmadan önce `EXPORT` denetim olayını yazar. Bu nedenle parçalar eksik olduğunda, tarayıcıda çözme veya indirme başarısız olduğunda ya da **Kopyasını oluştur** ön kontrolü kaynak parçaları listeledikten sonra durduğunda da `EXPORT` görülebilir. Paylaşım hazırlığı da kaynak parça listesini aldığı için paket daha sonra başarısız olsa bile aynı olay oluşabilir.

**VirusTotal SHA-256 araması** dosyayı yüklemez; `https://www.virustotal.com/gui/file/{sha256}` adresini yeni sekmede açar ve `VIEW` denetim olayı yazmayı dener. Bu işlem SHA-256 özetini üçüncü taraf bir hizmete taşır; kurum politikası izin vermiyorsa kullanmayın.

Yeni dosya kaydı normalde iki denetim kanıtı üretir: kayıt oluşturma `IMPORT`, parça yüklemeden önce mevcut parça kümesini temizleme `EDIT`. Dosya değiştirme, kayıt güncellemesi için bir `EDIT` ve eski parçaları temizleme için ikinci bir `EDIT` üretebilir. Silme `DELETE` olarak kaydedilir. Kopya ön kontrolünde kaynak parçaların listelenmesi `EXPORT`; yeni kopya kaydının ve parçalarının yazılması ise `IMPORT` ile `EDIT` üretir. Dosya adını veya ekrandaki meta veriyi işletim sistemi yoluyla kopyalamak için ayrı bir VaultPilot denetim olayı yoktur.

## Paylaşım ve Toplu İşlemler

Yazılabilir kasada **Tümünü seç**, yalnız geçerli arama ve filtrede görünen dosya kayıtlarını seçer. Görünür kayıtların tümü seçildiğinde düğme **Seçimi temizle** olur ve seçimi kaldırır. Görüntüleyici veya salt okunur modda dosya kayıtları toplu görünür seçim kümesinden çıkarıldığı için bu düğme devre dışıdır; satır onay kutuları yine görünür ve dosyalar tek tek seçilebilir. Bu modda seçimi kaldırmak için satır kutularını tek tek temizleyin.

Dosya ekranında kullanılabilen toplu menü şunları içerebilir:

- **Seçilenleri dışa aktar** hassas onaydan sonra kayıt verilerini JSON dosyasına yazar ve her kayıt için `EXPORT` olayı oluşturur. Dosya kaydı için bu çıktı başlık, not ve dosya meta verisini taşır; şifreli dosya parçalarının veya indirilebilir dosya içeriğinin yerine geçmez.
- **Kategori ata**, **Etiket ata**, **Arşivle**, **Pasifleştir / iptal et**, **Toplu not ekle**, **Seçiliyi düzenle** ve **Onayla ve kaldır** yazılabilir kasa ister.
- **Denetim raporuna ekle** CSV'ye yalnız genel kayıt alanlarını yazar: başlık, tür, kaynak, durum, risk, sahip, kategori, etiketler, güncelleme zamanı ve dosya kayıtlarında boş kalan dizin alanları. Dosya adı, boyut, parça sayısı, SHA-256 özeti ve dosya içeriği rapora eklenmez.
- **Güvenlik kontrolü başlat** dosya için antivirüs veya zararlı yazılım taraması değildir; dosya kaydında kopyalanabilir gizli değer bulunmadığı için ikili dosya içeriğini taramaz.
- **Excel'den içeri aktar** genel kayıt şablonu akışıdır; birden çok ikili dosyayı yükleyen dosya aktarım aracı değildir. Şifreli ek oluşturmak için **Yeni dosya** akışını kullanın.
- **Toplu paylaş**, seçili kayıtları **Paylaşım** ekranına taşır. Burada alıcı, süre ve kullanım sınırı ayrıca doğrulanmadan paket gönderilmez.

Dahili paylaşım için etkin kasada **Yönetici** rolü, kullanıcı yönetimi yetkisi ve yazılabilir lisans gerekir. Dahili pakette seçili dosyaların toplamı 1 GB'ı ve toplam parça sayısı 512'yi aşamaz. Dış paylaşım paketi için etkin kasada **Yönetici** rolü ve yazılabilir lisans gerekir; dış pakette ayrıca toplam parça tavanı yoktur, ancak paket toplamı 1 GB ve her kaynak dosya en fazla 1 GB/512 parça sınırında kalır. Her iki yöntemde de dosya parçaları tarayıcıda açılır ve paylaşım anahtarıyla yeniden şifrelenir; bu işlem orijinal kasa kaydını herkese açık yapmaz.

## Önerilen İş Akışları

### Yeni şifreli dosya ekleme

1. Doğru kasayı ve Düzenleyici/Yönetici rolünü doğrulayın.
2. Dosyanın boyutunu, sahibini ve saklama gerekçesini kontrol edin. Ekran tam kalan alanı göstermediği için 1 GB kullanıcı/kasa sınırında pay bırakın.
3. **Yeni dosya** ile kaydı hazırlayın ve kaydetme ilerlemesi bitene kadar bekleyin.
4. Listede ad, boyut, parça sayısı ve SHA-256 değerini doğrulayın.
5. Denetim Kaydı'nda normal dosya oluşturma akışının `IMPORT` ve parça temizleme `EDIT` olaylarını kontrol edin.

### Dosyayı güvenli indirme

1. Dosya adını, boyutunu ve kısaltılmış SHA-256 değerini beklenen kayıtla eşleştirin.
2. **Dosyayı indir** seçeneğini kullanın.
3. Parça eksikliği uyarısı yoksa indirilen dosyayı kurumun onaylı konumuna taşıyın.
4. Gerekirse yerel SHA-256 değerini kayıtla karşılaştırın ve `EXPORT` denetim olayını doğrulayın. Bu olay parçaların listelendiğini kanıtlar; tarayıcı indirmesinin tamamlandığını tek başına kanıtlamaz.

### Dosyayı değiştirme

1. **Kaydı düzenle** ile doğru kaydı açın.
2. **Dosyayı değiştir** ile yeni dosyayı seçip boyut, parça sayısı ve adı kontrol edin.
3. Şifreli güncellemeyi kaydedin; işlem bitmeden sekmeyi kapatmayın.
4. İndirme testi ve Denetim Kaydı'ndaki iki olası `EDIT` olayıyla yeni parçaları doğrulayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Dosyalar yükleniyor | İskelet satırlar bitene kadar oluşturma, toplu işlem veya indirme başlatmayın. |
| Bu kasada kayıt yok | Yazma yetkiniz varsa **Yeni dosya** kullanın; dosyanın bu kasaya ait olduğundan emin olun. |
| Arama veya filtre sonucu yok | Arama ifadesini değiştirin, etkin akıllı filtreleri temizleyin veya **Tümü** seçeneğine dönün. |
| Görüntüleyici / salt okunur | İndirme kullanılabilir; oluşturma, değiştirme, kopya, düzenleme, silme ve paylaşım oluşturma kapalıdır. **Tümünü seç** devre dışıdır; satır kutuları tek tek kullanılabilir. |
| Dosya seçilmedi | Yeni kayıtta **Dosya seç** ile tek dosya seçmeden kaydetmeyin. |
| 1 GB sınırı veya kota aşıldı | Dosya boyutunu veya kullanıcı/kasa kullanımını azaltın. Ekran tam kalan alanı göstermez; sınırı sunucu uygular. |
| Dosya şifrelenip yükleniyor | İlerleme tamamlanana kadar sayfayı yenilemeyin veya sekmeyi kapatmayın. |
| Dosya parçaları eksik | Kasayı yenileyin; sorun sürerse kaydı düzenleyip dosyayı yeniden ekleyin. Eksik kaydı paylaşmayın veya kopyalamayın. |
| Dosya indirilemedi | Kasanın açık olduğunu, erişim rolünü ve parça bütünlüğünü kontrol edip bir kez yenileyin. |
| Toplu işlemde kayıt seçilmedi | Önce görünür dosya kayıtlarından en az birini seçin. |
| Paylaşım dosya eklerini hazırlıyor | Parçalar tamamlanmadan paketi indirmeyin, kopyalamayın veya alıcıya göndermeyin. |

## İşlemden Önce

- Doğru sunucu profili, kasa ve dosya kaydında olduğunuzu doğrulayın.
- Oluşturma/değiştirme için etkin kasa rolünün Düzenleyici veya Yönetici ve lisansın yazılabilir olduğunu kontrol edin.
- Dosya sahibini, saklama ve imha beklentisini, ilgili talep kaydını ve dosya adını doğrulayın.
- Boyutun 1 GB'ı aşmadığını kontrol edin. Tam kalan alan ekranda gösterilmediğinden kullanıcı/kasa sınırında güvenli pay bırakın; son kararı sunucu verir.
- Log, veritabanı dökümü, özel anahtar, sertifika paketi veya ekran görüntüsünü dosya kasasına koymadan önce veri sınıflandırma ve saklama politikasını uygulayın.
- İndirme hedefinin, paylaşım alıcısının ve VirusTotal gibi üçüncü taraf özet aramasının kurum politikasına uygun olduğunu doğrulayın.
- Değiştirme veya silme öncesi geri dönüş için gerekli onaylı yedeğin bulunduğunu doğrulayın.

## Güvenli Kanıt

- Paylaşılabilir: ekran durumu, genel hata sınıfı, yuvarlanmış boyut aralığı, parça sayısı, rol/lisans modu ve gizli bilgi içermeyen işlem zamanı.
- Gizli kalmalı: dosya içeriği, tam dosya adı, tam SHA-256 özeti, kayıt kimliği, sahip/alıcı, iç sistem veya talep kaydı adresi, kasa adı, not, müşteri bağlamı ve indirilen yerel yol.
- `IMPORT`, `EDIT`, `EXPORT`, `VIEW` veya `DELETE` olayını kanıt olarak gönderirken kullanıcıyı, hedef kimliğini, zaman ilişkisini ve bütünlük özetini uygun şekilde maskeleyin.
- Ham günlük kayıtlarını, veritabanı dökümlerini, özel anahtarları, imzalama materyalini, kurulum paketlerini, yayın arşivlerini veya redakte edilmemiş ekran görüntülerini herkese açık destek kanalına yüklemeyin.
- Dosya özeti üçüncü taraf aramasına gönderildiyse bunu kanıt paketinde belirtin; dosyanın kendisinin gönderildiğini varsaymayın.

## Ne Zaman Durmalı ve Destek İstemelisiniz

Beklenen dosya adı, boyutu veya SHA-256 özeti değiştiyse; parça sayısı eksik kalıyorsa; şifreleme/yükleme ilerlemesi tamamlanmıyorsa; silinen kayıt geri görünüyorsa; kullanıcı/kasa sınırı beklenmedik biçimde doluysa; denetim olayı oluşmuyorsa; yanlış dosya indirildi, kopyalandı veya paylaşıma eklendiyse işlemi durdurun. Dosya içeriğini eklemeden; ekran durumu, redakte kayıt kimliği, genel boyut, parça sayısı, son güvenli adım, zaman ve hata metniyle özel destek kaydı açın.

## Operatör Notları

Dosyalar ekranı dosya içeriğini otomatik olarak sınıflandırmaz, zararlı yazılım taraması yapmaz veya saklama süresi dolunca kendiliğinden silmez. **VirusTotal SHA-256 araması** yalnız harici bir özet sorgusudur. Veri sahibi, saklama politikası, güvenli indirme hedefi ve gerektiğinde kalıcı silme operatör sorumluluğundadır.

## İlgili

- [Yeni kayıt ekranı](screen-new-item.md)
- [Paylaşım ekranı](screen-sharing.md)
- [Denetim Kaydı ekranı](screen-audit-log.md)
- [Yedekleme ve geri yükleme](backups-and-restore.md)
- [Herkese açık depo sınırı](public-repository-boundary.md)
- [Destek kanıt paketi](support-evidence-pack.md)
