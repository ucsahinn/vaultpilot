# Parolalar Ekranı

Üst çubuktaki `?`, Parolalar ekranı açıkken bu bağlama özel rehberi açar. Bu ekran, aktif kasadaki parola kayıtlarını bulmak, incelemek ve yetkiniz varsa düzenlemek içindir. Buradaki üretme, kopyalama ve “otomatik doldurma paketi” işlemleri hedef sistem hesabını kendiliğinden değiştirmez.

## Erişim, Kasa Rolü ve Lisans

- Sahip, Yönetici ve Kullanıcı sistem rolleri, kendilerine okunabilir kasa erişimi verildiyse parola çalışma alanını kullanabilir. Denetçi gizli kayıt çalışma alanına giremez.
- Kayıtların çözülebilmesi için aktif kasanın kilidi açık ve kasa anahtarının tarayıcı oturumunda kullanılabilir olması gerekir.
- Görüntüleme okunabilir kasa erişimi ister. Oluşturma, kopya üretme, düzenleme, silme ve yazan toplu işlemler için aktif kasada **Editor** veya **Manager** rolü ve salt okunur olmayan lisans gerekir.
- Salt okunur lisans listeleme, gösterme, kopyalama ve yerel sızıntı kontrolüne engel değildir; kasa verisini değiştiren işlemler kapalıdır.
- Sistem rolü tek başına kasa yetkisi vermez. Her işlemden önce doğru aktif kasayı ve o kasadaki rolünüzü doğrulayın.

## Burada Ne Yapılır

- Başlık, kullanıcı adı/e-posta, giriş URL'si, parola ve not içeren kayıtlar oluşturulur veya yeniden şifrelenerek güncellenir.
- Arama, hızlı filtreler ve birleştirilebilir akıllı filtrelerle görünür kayıt kümesi daraltılır.
- Kart veya tablo görünümünde parola, kullanıcı adı ve URL ayrı işlemlerle kopyalanır.
- HIBP Pwned Passwords üzerinden isteğe bağlı sızıntı kontrolü çalıştırılır.
- Seçili kayıtlar paylaşım ekranına veya toplu düzenleme, rapor, dışa aktarma ve silme işlemlerine hazırlanır.

## Arama, Filtreler ve Görünüm

Metin araması; başlık, kullanıcı adı, URL, sunucu adı, etki alanı, sahip, kategori, kaynak, risk ve etiket alanlarında çalışır. Parola değerinin içinde arama yapılmaz.

Hızlı filtre bandı veriye göre **Tümü**, **Sızıntı görüldü**, **Kontrol bekliyor**, **Uyarı** ve en sık ürün/servis ya da kategori seçeneklerinden en fazla yedisini gösterir. **Akıllı filtre ekle** menüsünde kullanıcı adı veya sahip, ürün/servis, kategori, etiket ve sızıntı durumu seçenekleri bulunabilir. Birden fazla akıllı filtre birlikte seçildiğinde kayıt bütün koşullarla eşleşmelidir.

Bir filtre çipine basmak yalnız o filtreyi, **Temizle** bütün akıllı filtreleri kaldırır. **Tümü** hızlı filtresi tür, risk ve akıllı filtre durumunu varsayılana döndürür; arama metnini ayrıca temizlemeniz gerekebilir.

**Kart** daha geniş kayıt kartları, **Tablo** kolon başlıklı sıkı yerleşim kullanır. **Yenile** kayıt sorgusunu tekrar çalıştırır. Kayıtlar son güncellenen önce gelecek şekilde alınır.

### Seçim kapsamı

- Tek tek işaretlenen kayıtlar filtre değiştiğinde görünüm dışında kalabilir ama seçili kalabilir.
- **Tümünü seç**, o anda görünür kayıtları seçim olarak yazar; önceki gizli seçimi korumaz. Görünürlerin tümü seçiliyse **Seçimi temizle** bütün seçimi boşaltır.
- Üstteki seçili sayısı yalnız görünür seçimi sayar; bazı toplu işlemler bellekte seçili kalan görünmez kayıtları da kullanır. Filtre değiştirdikten sonra seçimi açıkça temizleyip yeniden kurun.

## Kayıt Satırı İşlemleri

Parola satırının birincil işlemleri **Gizli değeri kopyala** ve geçerli HTTP/HTTPS adresi varsa **Siteyi aç**tır. Diğer işlemler menüsünde şunlar bulunur:

- **Otomatik doldurma paketi hazırla**
- **Sızıntı kontrolü**
- **Kullanıcı adını kopyala**
- **Gizli değeri göster / gizle**
- **URL'yi kopyala**
- **Kopya oluştur**, **Kaydı düzenle** ve **Kaydı sil**

**Siteyi aç** yalnız doğrulanabilen HTTP/HTTPS adresini açar ve `VIEW` olayı yazmayı dener. Giriş yapmaz ve sayfadaki alanları doldurmaz.

## Gösterme, Kopyalama ve Denetim

**Gizli değeri göster** önce uyarı onayı ister. Değer ardından tarayıcıdaki kartta görünür ve `VIEW` olayı yazılır. Gösterim sabit kısa bir sayaçla kapanmaz; düğmeyle gizleyene, başka bir kaydı gösterene, kasayı kilitleyene veya 15 dakikalık hareketsizlik kilidi devreye girene kadar açık kalabilir.

Parola, kullanıcı adı, URL ve doldurma paketi işletim sistemi panosuna yazılır; ardından `COPY` olayı oluşturulur. Pano temizleme zamanlayıcısı 30 saniyedir ve yalnız pano hâlâ aynı değeri içeriyorsa boş yazmayı dener. Tarayıcının kapanması, pano izni, işletim sistemi veya pano yöneticisi bu temizliği engelleyebilir; zamanlayıcı erişimin geri alındığına dair garanti değildir.

Pano yazımı ve görünür kılma, denetim isteğinden önce gerçekleşir. Denetim yazımı sonradan başarısız olsa bile değer ekranda veya panoda bulunabilir. Denetim olayının olmaması hassas değerin hiç açılmadığını kanıtlamaz.

### “Otomatik doldurma paketi” sınırı

Bu ekrandaki **Otomatik doldurma paketi hazırla**, kullanıcı adı ile parolayı sekmeyle ayrılmış tek metin olarak panoya kopyalar ve `COPY` olayı yazar. Kullanıcı bu metni hedef sayfanın kullanıcı adı alanına yapıştırır. Bu işlem tarayıcı eklentisini uzaktan çalıştırmaz; alanları bulduğunu, doldurduğunu veya girişin başarılı olduğunu garanti etmez. VaultPilot Browser Vault Extension'ın sayfa içi doldurma akışı ayrı bir güven sınırıdır.

## HIBP Sızıntı Kontrolü

Tek kayıt veya düzenleyicideki **Sızıntı kontrolü**, parolanın SHA-1 özetini tarayıcıda hesaplar. Yalnız özetin ilk beş karakteri `api.pwnedpasswords.com/range` adresine gönderilir; tam parola ve tam özet gönderilmez. Dönen son ekler tarayıcıda karşılaştırılır ve istek dolgu başlığı kullanır.

Sonuç **Sızıntı görüldü** veya **Bulunmadı** olarak, görülme sayısı ve kontrol zamanı ile gösterilir. **Bulunmadı**, parolanın güçlü, benzersiz veya güvenli olduğunu kanıtlamaz. **Sızıntı görüldü** sonucunda önce gerçek sistemde parolayı değiştirin, sonra kasa kaydını güncelleyin.

Tek kayıt kontrolü özel bir sunucu denetim olayı yazmaz. Toplu **Güvenlik kontrolü başlat**, başarıyla kontrol ettiği her kayıt için `VIEW` olayı yazmayı dener.

Sonuçlar parola olmadan; kayıt kimliği, durum, görülme sayısı ve zaman bilgisiyle bu tarayıcı profilinin `localStorage` alanında tutulur. Başka tarayıcı veya temizlenmiş depolama farklı sonuç kümesi gösterir. Kayıt parolası değiştiyse eski sonuç güncel değeri temsil etmeyebilir; karar vermeden önce yeniden kontrol edin.

## Yeni Kayıt ve Düzenleyici

**Yeni parola** düzenleyicisi zorunlu başlık ve parola; isteğe bağlı kullanıcı adı/e-posta, giriş URL'si ve not alanları sunar. Parola taslağı düzenleyicide düz metin görünen bir metin alanındadır; ekran paylaşımı ve omuz üzerinden görüntüleme riskini yönetin.

Kaydetme sırasında kayıt aktif kasa anahtarıyla tarayıcıda şifrelenir. Yeni kayıt `CREATE`, güncelleme `EDIT` olayı üretir. **Düzenle** mevcut kaydı Yeni kayıt ekranına taşır; **Kaydet** hedef sistem hesabını değil yalnız şifreli kasa kaydını günceller.

### Parola üretici

Üretici varsayılan olarak 24 karakter kullanır. Arayüz 12-64 karakter aralığı ile büyük harf, rakam ve sembol seçenekleri sunar; küçük harf kümesi her zaman etkindir. Üretim tarayıcıda `crypto.getRandomValues` ile yapılır. Etkin sınıflar olası karakter havuzuna eklenir; her etkin sınıftan mutlaka bir karakter gelmesi garanti edilmez.

**Kısa**, **Hazır** ve **Güçlü** göstergeleri yalnız uzunluğa bakar: 16 karakterden kısa, 16-23 ve en az 24. Bunlar hedef sistem politikasını, benzersizliği veya sızıntı durumunu doğrulamaz.

Sızıntılı karttaki **Yeni parola üret**, geçerli ayarlarla yeni değer oluşturup düzenleyiciyi açar. Siz **Kaydet** demeden kasa kaydına yazılmaz; hedef sistem parolasını hiçbir zaman otomatik değiştirmez.

## Kopya, Silme, Toplu İşlem ve Paylaşım

**Kopya oluştur**, aynı kasada yeni kayıt üretir ve başlığa “kopyası” ekler. Dış sistemde ikinci hesap oluşturmaz. Yazma yetkisi gerekir ve yeni kayıt `CREATE` olayı bırakır.

**Kaydı sil**, geri alınamaz işlem için ikinci onay ister ve başarılı olduğunda `DELETE` olayı üretir. Yalnız kasa kaydını kaldırır; hedef sistem hesabını kapatmaz veya parolasını değiştirmez.

Toplu işlemler menüsünde Excel şablonu indirme/içe aktarma, dışa aktarma, kategori veya etiket atama, arşivleme, pasifleştirme, güvenlik kontrolü, denetim raporu, paylaşım, not ekleme, ilk seçiliyi düzenleme ve onaylı silme bulunur.

- Kategori, etiket, arşiv, pasifleştirme, not, düzenleme, içe aktarma ve silme yazma yetkisi ister.
- **Pasifleştir / iptal et**, parola kaydının şifreli meta verisini `DISABLED` yapar; hedef hesabı devre dışı bırakmaz.
- **Seçilenleri dışa aktar**, çözülen tam kayıtları ve parolaları düz metin JSON dosyasına yazar; tehlikeli işlem onayı ister. Denetim olayları sonradan en iyi çabayla yazılır.
- **Denetim raporuna ekle**, parola değerini değil kayıt meta verilerini CSV dosyasına yazar.
- Toplu düzenleme ve silme kayıtları sırayla işler; ortadaki hata önceki başarılı değişiklikleri geri almaz. Kasayı yenileyip kayıtları ve denetim izini uzlaştırın.
- **Toplu paylaş**, seçili kimlikleri Paylaşım ekranının yöntem adımına taşır; henüz paket göndermez. Gerçek gönderim Paylaşım özelliği, Manager rolü, yazılabilir lisans ve seçilen yöntemin ayrı kurallarına tabidir.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Kayıtlar yükleniyor | Dört iskelet satırı kaybolana kadar bekleyin; gerekirse oturumu doğrulayıp **Yenile** kullanın. |
| Kasada kayıt yok | Aktif kasayı ve kilit durumunu doğrulayın; yazma yetkiniz varsa **Yeni parola** ile başlayın. |
| Eşleşen kayıt yok | Arama metnini, hızlı filtreyi ve akıllı filtre çiplerini ayrı ayrı temizleyin. |
| Liste boş ama kayıt bekleniyor | Ayrı sorgu hata kartı yoktur. Oturumu, sunucu bağlantısını, aktif kasayı ve ağ isteğini kontrol edin. |
| Salt okunur | Gösterme ve kopyalama mümkün olabilir; oluşturma, kopya, düzenleme, silme ve yazan toplu işlemler kapalıdır. |
| Pano hatası | Değer panoya yazılmış olabilir. Panoyu elle temizleyip `COPY` denetim izini kontrol edin. |
| Gösterim denetimi yazılamadı | Değer görünür kalabilir. Hemen gizleyin veya kasayı kilitleyin; denetimi ayrıca uzlaştırın. |
| Sızıntı kontrolü kullanılamıyor | Ağ, tarayıcı politikası veya HIBP erişimini kontrol edin; sonucu “temiz” saymayın. |
| Sızıntı görüldü | Hedef sistemde gerçek parolayı değiştirin, sonra kasa kaydını güncelleyip yeniden kontrol edin. |
| Toplu işlem yarım kaldı | Körlemesine tekrarlamayın; görünür/gizli seçimi, kasa durumunu ve denetim olaylarını karşılaştırın. |

## İşlemden Önce

- Doğru aktif kasa, kayıt başlığı, kullanıcı adı ve URL'nin aynı hesaba ait olduğunu doğrulayın.
- Gösterme, kopyalama veya dışa aktarma öncesinde ekran paylaşımını ve pano yöneticilerini kapatın.
- Filtre değiştirdiyseniz gizli kalmış toplu seçimi temizleyip kapsamı yeniden kurun.
- Yeni parolayı önce hedef sistemde uygulama, ardından kasa kaydını güncelleme sırasını planlayın.
- Paylaşımda alıcıyı, süreyi, kullanım hakkını ve teslim sınırını Paylaşım ekranında yeniden doğrulayın.

## Güvenli Kanıt

- Paylaşılabilir: ekran adı, genel kart/tablo görünümü, geniş zaman aralığı, kayıt sayısı, genel filtre türü, hesapla ilişkilendirilemeyen sızıntı durumu, genel hata sınıfı ve rol/lisansın yazılabilir olup olmadığı.
- Gizli kalmalı: parola, kullanıcı adı ile URL eşleşmesi, kayıt başlığı, not, kasa adı/kimliği, tam zaman damgası, belirli hesapla ilişkili HIBP sayısı, seçili kayıt kümesi, pano içeriği, düz metin JSON dışa aktarımı ve değer gösteren ekran görüntüsü.
- Parola veya doldurma paketi genel kanala girdiyse panonun temizlenmesini beklemekle yetinmeyin; hedef sistemde parolayı değiştirin ve kasa kaydını ardından güncelleyin.

## Ne Zaman Durmalı

Aktif kasa belirsizse, kayıt ile hedef URL eşleşmiyorsa, gizli toplu seçimden şüpheleniyorsanız, pano veya ekran kaydı kontrolünüz dışında ise, denetim olayı işlemle çelişiyorsa, sızıntı sonucu eski olabilecekse, toplu işlem yarım kaldıysa ya da yeni parola hedef sistemde uygulanmadan yalnız kasa kaydı değiştirilecekse durun. Kapsamı ve son güvenli adımı özel kanalda uzlaştırmadan işlemi tekrarlamayın.

## Operatör Notları

VaultPilot parola kaydını şifreli saklar; ancak kilidi açık tarayıcı oturumu gösterme, düzenleme, HIBP kontrolü, dışa aktarma ve pano işlemleri için değeri geçici olarak düz metne çevirir. Ekran, pano ve indirilen düz metin dosya bu anda ayrı güven sınırlarıdır. VaultPilot'taki “pasif”, “yeni parola” veya “otomatik doldurma paketi” işlemlerini hedef sistemde tamamlanmış hesap değişikliği olarak raporlamayın.

## İlgili

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Paylaşım ekranı](screen-sharing.md)
- [Tarayıcı eklentisi ekranı](screen-browser-extension.md)
- [Denetim Geçmişi ekranı](screen-audit-log.md)
- [Güvenli destek kanıtı](support-evidence-pack.md)
- [Operatör çalışma kılavuzu](operator-runbook.md)
