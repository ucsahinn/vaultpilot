# API Anahtarları Ekranı

Üst çubuktaki `?`, API Anahtarları çalışma alanı açıkken bu bağlama özel rehberi açar. Bu ekran; servis anahtarı, erişim belirteci ve benzeri makineden makineye gizli değerleri aktif kasada bulmak, incelemek ve yetkiniz varsa güncellemek içindir. VaultPilot’taki bir kaydı “iptal” durumuna almak, sağlayıcıdaki gerçek anahtarı iptal etmez.

## Erişim, Kasa Rolü ve Lisans

- Sahip, Yönetici ve Kullanıcı sistem rolleri, kendilerine okunabilir kasa erişimi verildiyse API anahtarı çalışma alanını kullanabilir. Denetçi gizli kayıt çalışma alanına giremez.
- Kayıtların çözülebilmesi için aktif kasanın kilidi açık ve kasa anahtarının tarayıcı oturumunda kullanılabilir olması gerekir.
- Listeleme, gösterme ve kopyalama okunabilir kasa erişimi ister. Oluşturma, kopya üretme, düzenleme, silme ve yazan toplu işlemler için aktif kasada **Editor** veya **Manager** rolü ve salt okunur olmayan lisans gerekir.
- Sistem rolü tek başına kasa yetkisi vermez. İşlemden önce doğru aktif kasayı ve bu kasadaki rolünüzü doğrulayın.

## Burada Ne Yapılır

- Başlık, istemci/sahip/servis hesabı, sağlayıcı konsol URL’si, API anahtarı veya token değeri ve kapsam/rotasyon notu içeren şifreli kayıt oluşturulur.
- Arama, hızlı filtreler ve akıllı filtrelerle görünür kayıt kümesi daraltılır.
- Gizli değer kopyalanır veya onaydan sonra ekranda gösterilir; geçerli HTTP/HTTPS adresi varsa sağlayıcı konsolu açılır.
- Kayıt kopyalanır, düzenlenir, silinir, paylaşım akışına hazırlanır ya da kontrollü toplu işleme alınır.

## Arama, Filtreler ve Görünüm

Metin araması; başlık, istemci/sahip alanı, URL, sunucu adı, etki alanı, kategori, kaynak, risk ve etiketlerde çalışır. Gizli anahtar değerinin içinde arama yapılmaz.

Hızlı filtreler veriye göre **Tümü**, **Kritik**, **Uyarı**, **İçe aktarıldı** ve en sık ürün, kategori veya etiket seçeneklerinden en fazla yedisini gösterir. **Akıllı filtre ekle** ile birden fazla koşul seçildiğinde kayıt bütün koşullarla eşleşmelidir. **Tümü** tür, risk ve akıllı filtreleri varsayılana döndürür; arama metnini ayrıca temizlemeniz gerekebilir.

**Kart** görünümü daha geniş kayıt kartları, **Tablo** görünümü sıkı kolon düzeni kullanır. **Yenile** kayıt sorgusunu tekrar çalıştırır. Kayıtlar son güncellenen önce gelecek şekilde alınır.

### Seçim kapsamı

- Bir filtre kaydı gizlese bile daha önce işaretlenen kayıt bellekte seçili kalabilir.
- **Tümünü seç**, o anda görünür kayıtları yeni seçim yapar. Görünürlerin tamamı seçiliyse **Seçimi temizle** bütün seçimi boşaltır.
- Üstteki sayı görünür seçimi sayarken bazı toplu işlemler bellekte kalan görünmez kimlikleri de kullanır. Filtre değiştirdikten sonra seçimi açıkça temizleyip yeniden kurun.

## Kayıt Satırı İşlemleri

Birincil işlemler **Gizli değeri kopyala** ve geçerli bir HTTP/HTTPS adresi varsa **Konsolu aç**tır. **Diğer işlemler** menüsünde şunlar bulunur:

- **Gizli değeri göster / gizle**
- **URL’yi kopyala**
- **Kopya oluştur**
- **Kaydı düzenle**
- **Kaydı sil**

**Konsolu aç** yalnız doğrulanabilen HTTP/HTTPS adresini yeni bağlamda açar ve `VIEW` olayı yazmayı dener. Sağlayıcıya giriş yapmaz, anahtarı doğrulamaz ve gerçek kapsamı sorgulamaz.

## Gösterme, Kopyalama ve Denetim

**Gizli değeri göster** önce hassas değer uyarısı ister. Değer kartta görünür ve ardından `VIEW` olayı yazılmaya çalışılır. Gösterim kısa bir sayaçla otomatik kapanmaz; siz gizleyene, başka kayıt gösterene, kasayı kilitleyene veya 15 dakikalık hareketsizlik kilidi çalışana kadar açık kalabilir.

Anahtar veya URL panoya yazıldıktan sonra `COPY` olayı oluşturulmaya çalışılır. Pano temizleme zamanlayıcısı 30 saniye sonra, pano hâlâ aynı değeri içeriyorsa boş değer yazmayı dener. Tarayıcı kapanması, pano izni, işletim sistemi veya pano yöneticisi temizliği engelleyebilir. Zamanlayıcıyı erişimin geri alındığı garantisi saymayın.

Pano yazımı ve ekranda gösterme, denetim isteğinden önce gerçekleşir. Denetim yazılamasa bile değer ekranda veya panoda bulunabilir; eksik olay, değerin açılmadığını kanıtlamaz.

## Yeni Kayıt ve Düzenleme

**Yeni API anahtarı** düzenleyicisi zorunlu başlık ile gizli değer; isteğe bağlı istemci/sahip/servis hesabı, konsol URL’si ve kapsam/rotasyon notu sunar. Taslak değer düzenleme sırasında tarayıcıda düz metin olarak bulunur. Ekran paylaşımını ve omuz üzerinden görüntülemeyi yönetin.

Kaydetme sırasında veri aktif kasa anahtarıyla tarayıcıda şifrelenir. Yeni kayıt `CREATE`, güncelleme `EDIT` olayı üretir. **Düzenle** yalnız VaultPilot kaydını değiştirir; sağlayıcıdaki token değeri, kapsamı, süresi veya istemci ayarları değişmez.

### Değer üretici ve sona erme meta verisi

Düzenleyicideki üretici tarayıcıda çalışır; varsayılan uzunluk 24, aralık 12–64 karakterdir. Küçük harfler her zaman havuzdadır; büyük harf, rakam ve sembol seçenekleri havuzu genişletir. Üretilen değer yalnız form alanını doldurur. Sağlayıcıda anahtar üretmez, doğrulamaz, döndürmez veya iptal etmez; gerçek anahtarı önce sağlayıcının onaylı akışında oluşturun.

Manuel düzenleyicide ayrı bir sona erme tarihi alanı yoktur. `API Keys` Excel sayfasıyla içe aktarılan `expiresAt`, şifreli kayıt meta verisi olur; otomatik rotasyon/iptal planlamaz ve sağlayıcıdaki gerçek sona erme durumunu kanıtlamaz. İçe aktarma kaynağı `imported`, durumu `ACTIVE` yapar; risk yalnız içe aktarma anında tarih geçmişse `expired`, aksi halde `unknown` olarak atanır. Bu sınıflandırmayı kendiliğinden ilerleyen canlı süre takibi saymayın.

Bir anahtar rotasyonunda güvenli sıra şudur:

1. Sağlayıcıda yeni anahtarı en az gerekli kapsamla üretin.
2. Tüketen sistemi kontrollü bakım penceresinde yeni değere geçirin ve işlevi doğrulayın.
3. Eski anahtarı sağlayıcıda iptal edin.
4. VaultPilot kaydını ve operasyon notunu güncelleyin; denetim izini uzlaştırın.

VaultPilot sağlayıcıya bağlanıp bu adımları otomatik uygulamaz.

## Kopya, Silme ve Toplu İşlemler

**Kopya oluştur** aynı kasada yeni bir şifreli kayıt üretir; sağlayıcıda yeni anahtar oluşturmaz. **Kaydı sil** ikinci onaydan sonra VaultPilot kaydını geri alınamaz biçimde kaldırır; sağlayıcıdaki anahtar çalışmaya devam edebilir.

Toplu menü; Excel şablonu/içe aktarma, düz metin dışa aktarma, kategori ve etiket atama, arşivleme, pasifleştirme/iptal, güvenlik kontrolü, denetim raporu, paylaşım, not ekleme, ilk seçiliyi düzenleme ve onaylı silme işlemlerini içerir.

- **Pasifleştir / iptal et**, seçili API anahtarlarının şifreli meta verisini `REVOKED`, kaynak alanını `revoked` ve riski `warning` yapar. Sağlayıcıya iptal isteği göndermez.
- **Seçilenleri dışa aktar**, çözülmüş tam kayıtları ve anahtar değerlerini düz metin JSON dosyasına yazar. Dosya ayrı bir hassas veri kopyasıdır; indirme sonrası otomatik silinmez.
- **Denetim raporuna ekle**, gizli değer yerine kayıt meta verisini CSV’ye yazar.
- Toplu güncelleme ve silme kayıtları sırayla işler. Ortadaki hata önceki başarıları geri almaz; yenileyip gerçek kapsamı ve denetim olaylarını uzlaştırmadan tekrar çalıştırmayın.
- **Toplu paylaş**, seçimi Paylaşım ekranının yöntem adımına taşır; paket henüz gönderilmez ve seçim yetki kazandırmaz. Dahili alıcı paketi için Sahip/Yönetici sistem rolü, aktif kasada **Manager** ve yazılabilir lisans; harici paket için aktif kasada **Manager** ve yazılabilir lisans gerekir.
- “Güvenlik kontrolü” HIBP parola denetim mekanizmasını gizli değere uygulayabilir; bir API anahtarının sağlayıcıda geçerli, doğru kapsamlı veya sızmamış olduğunu kanıtlamaz.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Kayıtlar yükleniyor | İskelet satırları kaybolana kadar bekleyin; gerekirse oturumu ve aktif kasayı doğrulayıp **Yenile** kullanın. |
| Kayıt yok | Doğru kasa ve kilit durumunu doğrulayın; yazma yetkiniz varsa **Yeni API anahtarı** ile başlayın. |
| Eşleşen kayıt yok | Aramayı, hızlı filtreyi ve akıllı filtre çiplerini ayrı ayrı temizleyin. |
| Salt okunur | Gösterme ve kopyalama mümkün olabilir; kayıt değiştiren işlemler kapalıdır. |
| `REVOKED` | Yalnız VaultPilot meta verisidir. Sağlayıcı konsolunda gerçek iptal durumunu ayrıca doğrulayın. |
| Pano veya denetim hatası | Değer zaten açılmış olabilir. Panoyu elle temizleyin, gösterimi kapatın ve olayı ayrı kanaldan uzlaştırın. |
| Toplu işlem yarım kaldı | Körlemesine tekrar etmeyin; gizli seçimi, değişen kayıtları ve sağlayıcıdaki gerçek durumu karşılaştırın. |

## İşlemden Önce

- Anahtarın sahibini, tüketen uygulamaları, ortamını, kapsamını ve bakım penceresini belirleyin.
- Aktif kasayı ve seçili kayıtları doğrulayın; filtre değiştiyse seçimi temizleyip yeniden kurun.
- Gösterme, kopyalama veya dışa aktarma öncesinde ekran paylaşımını ve pano yöneticilerini kapatın.
- Sağlayıcıda iptal/rotasyon yetkiniz ve geri dönüş planınız olmadan VaultPilot meta verisini “iptal edildi” diye değiştirmeyin.
- Paylaşımda alıcıyı, süreyi, kullanım sınırını ve teslim kanalını Paylaşım ekranında yeniden kontrol edin.

## Güvenli Kanıt

- Paylaşılabilir: ekran adı, geniş zaman aralığı, genel sağlayıcı türü, kayıt sayısı, redakte edilmiş hata sınıfı, genel rotasyon durumu ve yazma yetkisinin bulunup bulunmadığı.
- Gizli kalmalı: API anahtarı/token değeri, tam istemci kimliği, başlık ile URL eşleşmesi, kapsam ayrıntısı, kasa adı/kimliği, tam zaman damgası, seçili kayıtlar, pano içeriği, düz metin dışa aktarım ve değer gösteren ekran görüntüsü.
- Bir değer genel kanala girdiyse panoyu temizlemek yeterli değildir. Sağlayıcıda anahtarı iptal edin, yeni anahtar üretin, tüketicileri güncelleyin ve ancak sonra kasa kaydını uzlaştırın.

## Ne Zaman Durmalı

Aktif kasa, anahtar sahibi veya tüketen sistem belirsizse; sağlayıcıda gerçek rotasyon/iptal yetkisi yoksa; gizli toplu seçimden şüpheleniyorsanız; pano ya da ekran kaydı kontrolünüz dışında ise; denetim izi işlemle çelişiyorsa; toplu işlem yarım kaldıysa veya yalnız VaultPilot kaydını değiştirerek dış sistemde rotasyon tamamlandı sanılacaksa durun. Son güvenli adımı özel kanalda uzlaştırmadan işlemi tekrarlamayın.

## Operatör Notları

VaultPilot API anahtarı kaydını diskte şifreli saklar; kilidi açık tarayıcı gösterme, düzenleme, kopyalama ve dışa aktarma için değeri geçici olarak düz metne çevirir. Ekran, pano ve indirilen JSON ayrı güven sınırlarıdır. `REVOKED`, `ARCHIVED` veya silinmiş bir VaultPilot kaydını sağlayıcıdaki anahtarın durumuna ilişkin kanıt olarak raporlamayın.

## İlgili

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Paylaşım ekranı](screen-sharing.md)
- [Denetim Geçmişi ekranı](screen-audit-log.md)
- [Public API referansı](public-api-reference.md)
- [Entegrasyon API client'ları](api-clients.md)
- [API client erişimi KB](../../kb/tr/api-client-401.md)
- [Güvenli destek kanıtı](support-evidence-pack.md)
