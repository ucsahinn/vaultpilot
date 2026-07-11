# Sertifikalar Ekranı

Üst çubuktaki `?` simgesi Sertifikalar ekranına ait bu rehberi açar. Bu ekran, seçili kasada tutulan sertifika, sertifika paketi ve özel anahtar kayıtları içindir. VaultPilot sunucusunun HTTPS sertifikasını kurmaz veya değiştirmez; canlı yayın sertifikası **Sunucu ayarları** içindeki ayrı akıştan yönetilir.

Denetçi rolü gizli kayıtlara ve kasa anahtarına erişemez. Sahip, Yönetici ve Kullanıcı rolleri yalnız kendilerine açılmış kasaları kullanır. Seçili kasadaki **Görüntüleyici** kaydı okuyabilir, gizli materyali geçici gösterebilir, kopyalayabilir ve varsa özgün dosyayı indirebilir. **Düzenleyici** ile kasa **Yöneticisi**, lisans yazılabilir durumdayken kayıt oluşturabilir, çoğaltabilir, düzenleyebilir ve silebilir.

## Burada Ne Yapılır

- **Sertifikalarda ara** ile başlık, sahip/servis, uç nokta, kategori, etiket, imzalayan, Subject/CN ve seri numarası içinde arayın.
- **Yenileme**, **Süresi doldu**, **Tarih yok** ve **İptal / pasif** hızlı filtrelerini; geçerlilik aralığı, sertifika otoritesi ve organizasyon gibi akıllı filtrelerle birleştirin. Hızlı filtre düğmesi yalnız ilgili kayıt sayısı sıfırdan büyükse görünür.
- Kart veya tablo görünümünü seçin ve yenile düğmesiyle seçili kasayı yeniden sorgulayın.
- Yazma yetkiniz varsa **Yeni sertifika** ile editörü açın; editördeki **Sertifika dosyasını içe aktar** alanını kullanın veya sertifika/özel anahtar materyalini metin olarak yapıştırın.
- Satır eylemleriyle gizli materyali gösterin, özgün dosyayı indirin veya menüden ayrıntıları açın, gizli değeri kopyalayın, kayıt kopyası oluşturun, düzenleyin ya da silin.

## Ekranı Nasıl Okumalısınız

Liste satırı başlığı ve son güncelleme zamanını gösterir. İçe aktarılmış kayıtlarda dosya adı, biçim, boyut, kalan süre, Subject/CN, imzalayan ve SHA-256 özetinin kısa bölümü de görünebilir. Bunlar kasa açıldıktan sonra kaydı tanımlayan meta verilerdir; sertifika gövdesi, özel anahtar veya paket içeriği değildir.

**Sertifika ayrıntılarını aç** yan paneli kaynak, risk, kayıt durumu, hesap/servis, hedef, kategori, sahip, etiket ve son güncelleme gibi bağlamı gösterir. Gizli materyali veya özgün dosyayı açığa çıkarmaz ve tek başına `VIEW` denetim olayı yazmaz.

Göz düğmesi onaydan sonra materyali önce tarayıcı oturumunda görünür yapar, ardından `VIEW` olayını yazmayı dener. **Gizli değeri kopyala** önce tüm gizli alanı panoya alır, ardından `COPY` olayını yazmayı dener. **Sertifika dosyasını indir** yalnız indirilebilir özgün dosya bulunan kayıtlarda etkinleşir; dosyayı önce indirir, ardından `EXPORT` olayını yazmayı dener. Sunucunun denetim isteğini reddetmesi tamamlanmış yerel gösterme, kopyalama veya indirme işlemini geri almaz; arayüz hata gösterebilir ve operatör sonucu denetim kaydıyla uzlaştırmalıdır. Gizleme değeri yeniden maskeler.

### Meta veri ile gizli materyal sınırı

Başlık, sahip/servis, uç nokta, not, geçerlilik tarihi, Subject/CN ve sertifika otoritesi sınıflandırması kasa açıkken görünür kayıt bağlamıdır. Bunlar da şifreli kayıt yükünde saklanır, ancak görüntülenmeleri için ayrıca gizli değeri gösterme onayı gerekmez.

**Sertifika veya özel anahtar** alanı zorunlu gizli değerdir ve varsayılan olarak maskelenir. Dosya içe aktarıldığında özgün dosya baytları ile hazırlanan materyal şifreli kayıt yüküne alınır. PFX/P12 parolası için ayrı alan yoktur. Paket parolasını başlık, sahip/servis, uç nokta veya not alanına yazmayın; gerekiyorsa ayrı bir parola kaydında yönetin.

Sertifika otoritesi kartlarında sağlayıcı adı, sinyal açıklaması ve erişim biçimi etiketi gösterilir. Bir kart seçildiğinde önceki tanınan sertifika otoritesi etiketi değiştirilir, kategori `Certificate` yapılır, kaynak boşsa `manual` atanır ve `certificate` etiketiyle seçilen otorite etiketi eklenir. DigiCert, GoDaddy, GlobalSign, Let’s Encrypt, Microsoft CA veya Self-signed seçmek dış hizmete bağlanmaz; sertifika düzenleme, yenileme, yeniden anahtarlama veya iptal işlemi başlatmaz.

## Önerilen İş Akışları

### Dosyadan sertifika kaydı oluşturma

1. Yazma yetkili kasayı açıp **Yeni sertifika** seçeneğini kullanın.
2. Zorunlu başlığı girin; sahip/servis ile ilgili uç noktayı kayıt bağlamı olarak doldurun.
3. **Sertifika dosyasını içe aktar** alanından PEM, CRT, CER, DER, P7B/P7C, PFX/P12, PKCS12, P8/P8E/PK8 veya KEY dosyası seçin. Dosya sınırı 10 MB’tır.
4. Dosya adı, biçim, boyut, içe aktarım zamanı, SHA-256 ve bulunabildiyse geçerlilik/Subject bilgilerini kontrol edin.
5. Gerekiyorsa **Geçerlilik bitişi** ile **Subject / CN** alanlarını düzeltip sertifika otoritesi sınıflandırmasını seçin.
6. Gizli alanın doğru materyali içerdiğini doğrulayıp kaydı saklayın.

Metin dosyalarında Subject, imzalayan, seri numarası ve bitiş zamanı yalnız tanınan satırlardan çıkarılabilir. İkili paketlerde bu alanlar otomatik dolmayabilir. Boş meta veri tek başına geçersiz paket kanıtı değildir; kaynağı özel kanaldan doğrulayın.

### Materyali elle ekleme veya kaydı yenileme

Dosya seçmeden başlık girip PEM, sertifika gövdesi veya özel anahtar materyalini zorunlu gizli alana yapıştırabilirsiniz. Geçerlilik bitişi ile Subject/CN elle eklenebilir. Elle oluşturulan kayıtta indirilebilir özgün dosya bulunmaz; indirme gerekiyorsa kaydı **Düzenle** ile açıp yetkili kaynak dosyasını yeniden içe aktarın.

Yenileme incelemesinde önce **Yenileme**, **Süresi doldu** ve **Tarih yok** filtrelerini kontrol edin; gerekirse geçerlilik aralığı veya sertifika otoritesi filtresi ekleyin. Yenilemeyi ilgili sertifika otoritesi ya da kurum sürecinde tamamlayın. Yeni dosya hazır olduğunda mevcut kaydı **Düzenle** üzerinden güncelleyin; sınıflandırma kartının yenileme yapmadığını unutmayın.

### Materyali görüntüleme, kopyalama veya indirme

Gizli değeri yalnız ihtiyaç anında ve ekran paylaşımı kapalıyken gösterin. Kopyalama sonrası 30 saniyelik pano temizliği en iyi çaba yaklaşımıyla çalışır: VaultPilot yalnız izinler elverirse panoyu okuyabilir ve değer hâlâ aynıysa temizleyebilir. İzin hatası veya arada panoya yazılan farklı bir değer temizliği engeller; önceki kopyalama geri alınmış olmaz. İndirme düğmesi kapalıysa kayıt elle girilmiş materyal veya indirilebilir özgün dosyası olmayan eski bir paket içeriyor olabilir. Dosyayı yetkili kaynaktan yeniden içe aktarın; ekranda olmayan bir dönüştürme ya da paket parolası çözme işlemi varsaymayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Yükleniyor | İskelet satırlar tamamlanmadan sonuç çıkarmayın. |
| Kayıt yok | Yazma yetkiniz varsa ilk kaydı oluşturun; yoksa doğru kasa ve rolü doğrulayın. |
| Eşleşme yok | Aramayı ve aktif akıllı filtreleri temizleyin. |
| Geçerli | Kalan süreyi, kullanılan uç noktayı ve yenileme sorumlusunu yine de doğrulayın. |
| Yenileme aralığında | 30 gün veya daha az kalan kaydı kurumun yenileme sürecine alın. |
| Süresi doldu | Materyali kullanıma vermeyin; kaynak durumunu ve yerine geçen sertifikayı doğrulayın. |
| Tarih yok | Bitiş tarihini yetkili kaynaktan tamamlayın; boş değeri sınırsız geçerlilik saymayın. |
| İptal / pasif | Kaydı etkin sertifika gibi kullanmayın; kaynak sistemle uzlaştırın. |
| Sertifika okunuyor | İçe aktarım bitmeden kaydetmeyin veya ikinci dosya seçmeyin. |
| Dosya çok büyük / okunamadı | 10 MB sınırını ve desteklenen biçimi doğrulayın; dosyayı açık kanala yüklemeyin. |
| İndirme kapalı | İndirilebilir özgün dosya yoktur; gerekiyorsa yetkili kaynaktan yeniden içe aktarın. |
| Yazma kapalı | Kasa rolünü ve lisansın salt okunur durumunu kontrol edin. |

## İşlemden Önce

- Seçili kasayı ve kasa rolünüzün yapmak istediğiniz işleme izin verdiğini doğrulayın.
- Kayıt yazmadan önce lisansın salt okunur olmadığını kontrol edin.
- İşlemin kasa kaydını mı yoksa sunucunun canlı HTTPS sertifikasını mı hedeflediğini kesinleştirin.
- Dosya kaynağını, beklenen SHA-256 özetini, Subject/CN bilgisini, imzalayanı ve bitiş tarihini güvenilir kanaldan doğrulayın.
- Gösterme, kopyalama ve indirme işlemlerinin sırasıyla `VIEW`, `COPY` ve `EXPORT` denetim olayları istediğini hesaba katın.
- Toplu kategori, etiket, arşivleme, pasifleştirme, not, düzenleme ve silme eylemlerinin Düzenleyici/Yönetici kasa rolü istediğini doğrulayın.

## Güvenli Kanıt

- **Paylaşılabilir:** sertifika durum sınıfı, genel geçerlilik aralığı, dosya biçimi ve boyutu, sertifika otoritesi sınıfı ve SHA-256 özetinin kısa bölümü.
- **Gizli kalmalı:** sertifika veya özel anahtar materyali, özgün PEM/KEY/PFX/P12 paketi, paket parolası, tam seri numarası ve parmak izi, iç sistem adı, tam Subject/issuer bilgisi, müşteri uç noktası ve açık kayıt ekran görüntüsü.
- Desteğe gönderilen görüntüde başlık, sahip/servis, URL, Subject/CN, imzalayan ve tam SHA-256 değerini maskeleyin.
- Özel anahtar veya paket parolası açığa çıktıysa kopyalama ve yeniden paketlemeyi bırakıp kurumun olay müdahale ve sertifika otoritesi sürecini özel kanaldan başlatın.

## Ne Zaman Durmalı ve Destek İstemelisiniz

Dosyanın SHA-256 özeti beklenen değerle uyuşmuyorsa, Subject/issuer veya bitiş tarihi kaynak kayıttan farklıysa, özgün dosyanın kaynağı doğrulanamıyorsa, gizli materyal yanlış kişiye gösterildiyse ya da kasa kaydı canlı sunucu sertifikası sanılıyorsa durun. Gizli materyali göndermeden; kayıt kimliği, genel biçim ve boyut, kısa SHA-256 bölümü, hassas ayrıntıları çıkarılmış hata ve denenen adımlarla özel destek kaydı açın.

## Operatör Notları

Kasa sertifika kaydı bir dağıtım aracı veya sertifika otoritesi istemcisi değildir. Dosya içe aktarmak VaultPilot sunucusunun HTTPS bağını değiştirmez; canlı yayın sertifikası yalnız **Sunucu ayarları** akışında yönetilir. Yenileme, sertifika otoritesi ve dağıtım notları operasyon bağlamıdır, otomatik işlem değildir.

## İlgili

- [Sertifika Paneli ekranı](screen-certificate-dashboard.md)
- [Sunucu ayarları ekranı](screen-server-settings.md)
- [Genel erişim adresi ve HTTPS](public-host-https-certificate.md)
