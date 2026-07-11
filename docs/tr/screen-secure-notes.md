# Güvenli Notlar Ekranı

Üst çubuktaki `?` düğmesi bu sayfayı **Güvenli Notlar** ekranından açar. Bu ekran; kurtarma adımları, bakım sırasında izlenecek özel yönergeler veya yalnız yetkili kişilerin görmesi gereken operasyon notları gibi yapılandırılmış bir kayıt türüne sığmayan hassas metinler içindir. Parola, API anahtarı, sertifika veya dosya kendi kayıt türünde tutulmalıdır.

Kayıtları okuyabilmek için açık bir kasaya erişiminiz olmalıdır. Yeni not oluşturma, mevcut notu değiştirme, kopyalama veya silme işlemleri için kasada yazma yetkisi ve yazılabilir lisans gerekir.

## Ekranı Tanıyın

- **Seçili ekranda ara** alanı not gövdesini veya isteğe bağlı gizli alanı taramaz. Arama; başlık, sahip/ekip, sistem veya referans, URL, sunucu ve etki alanı bilgileri ile kategori, etiket, kaynak ve risk gibi görünür meta verilerde çalışır.
- **Akıllı filtre ekle** ile kategori, etiket, risk ve kaynak gibi birden fazla ölçütü birlikte kullanabilirsiniz. Etkin filtreler ayrı rozetler halinde görünür; **Temizle** tümünü kaldırır.
- Tür filtreleri ve sayaçlar görünür kayıt kümesini daraltır. **Kart** ve **Tablo** düğmeleri yalnız görünümü değiştirir; kaydı değiştirmez.
- Her satırda gizli içeriği gösterme, panoya kopyalama ve işlem menüsü bulunur. Menüden **Kopyasını oluştur**, **Kaydı düzenle** veya **Kaydı sil** seçeneklerine ulaşılır.
- **Toplu işlemler** menüsündeki **Excel şablonu indir** yazma yetkisi istemez. **Excel’den içeri aktar** ise yazılabilir kasa gerektirir ve kayıt eklemeden önce çakışma seçenekleriyle bir önizleme gösterir.
- Kayıt seçildiğinde **Seçilenleri dışa aktar**, **Güvenlik kontrolü başlat** ve **Denetim raporuna ekle** salt okunur kullanımda da açık kalabilir. **Kategori ata**, **Etiket ata**, **Arşivle**, **Pasifleştir / iptal et**, **Toplu not ekle**, **Seçiliyi düzenle** ve **Onayla ve kaldır** kasada yazma yetkisi ister. **Toplu paylaş** seçimle açılır; paketi gerçekten oluşturabilmek için Paylaşım ekranındaki kasa ve rol koşulları ayrıca uygulanır.

## Temel İş Akışları

### Yeni bir güvenli not oluşturma

1. Güvenli Notlar ekranındaki **Yeni güvenli not** düğmesini seçin. Bu düğme tür seçimi istemeden doğrudan güvenli not formunu açar.
2. Başlığa gizli bilgi yazmadan notun amacını anlatan kısa bir ad verin. İçeriği, yalnız doğru kasaya ve doğru kişilere açık olacak şekilde hazırlayın.
3. Sonraki incelemede işe yarayacak kategori ve etiketleri ekleyin; genel prosedür metnini gereksiz yere kasaya kopyalamayın.
4. Kaydetmeden önce hedef kasayı doğrulayın. Kayıt satırındaki işlem menüsü daha sonra **Kopyasını oluştur**, **Kaydı düzenle** ve **Kaydı sil** seçeneklerini sunar.

Beklenen sonuç: Not listede görünür ve içeriği yalnız kasa açıldıktan sonra görüntülenebilir. Kayıt engellenirse formdaki gizli metni destek mesajına kopyalamayın; yetki, lisans ve kasa durumunu ayrı ayrı kontrol edin.

### Bir notu bulma ve güvenle okuma

1. Arama ve filtrelerle görünür kayıtları daraltın; not gövdesinin arama dizinine alınmadığını unutmayın.
2. Doğru başlığı ve son güncelleme zamanını doğrulayın.
3. **Gizli değeri göster** seçildiğinde VaultPilot önce **Gizli değer gösterilsin mi?** onayını açar. **Geçici göster** onayından sonra değer görünür olur ve kayıt için bir `VIEW` denetim olayı yazılır. İşiniz bitince **Gizli değeri gizle** seçeneğini kullanın.
4. **Gizli değeri kopyala** not gövdesini, gövde yoksa isteğe bağlı gizli alanı panoya alır ve başarılı akışta bir `COPY` denetim olayı yazar.

VaultPilot panodaki değeri 30 saniye sonra temizlemeyi dener; bunu yalnız pano hâlâ aynı değeri içeriyorsa ve tarayıcı pano okuma/yazma izni veriyorsa yapabilir. Bu en iyi çaba korumasıdır: işletim sistemi pano geçmişini, bulut eşitlemesini veya değerin yapıştırıldığı başka bir uygulamayı temizleyemez. Hassas bir notu kopyaladıktan sonra işi geciktirmeyin ve panonun temizlendiğini varsaymayın.

### Notu güncelleme veya kaldırma

**Kaydı düzenle** ile içeriği ve sınıflandırmayı güncelleyin. Bir not artık gerekli değilse silmeden önce başka bir ekip tarafından kullanılmadığını doğrulayın. Silme onayı görünene kadar işlem uygulanmaz; onaydan önce vazgeçmek güvenli durma noktasıdır.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Kayıt yok | Filtre uygulanmadığından emin olun. Gerçekten boşsa **Yeni kayıt** ile ilk notu oluşturun. |
| Eşleşme yok | Etkin akıllı filtreleri ve arama metnini temizleyin; bu durum kayıtların silindiği anlamına gelmez. |
| Salt okunur | Notları okuyabilirsiniz ancak oluşturma, düzenleme ve silme kapalıdır. Lisans ve kasa rolünü kontrol edin. |
| Yetki yetersiz | Notun bulunduğu kasaya erişim isteyin; başka bir kasada kopya oluşturarak sahiplik sınırını aşmayın. |
| Kaydetme hatası | Formu kapatmadan önce başlık, içerik ve zorunlu alanları kontrol edin. Gizli metni hata kaydına eklemeyin. |
| Yükleniyor | Liste tamamlanana kadar toplu işlem başlatmayın; yenileme sonrasında seçiminizi yeniden doğrulayın. |

## İşlemden Önce

- Metnin parola, API anahtarı, sertifika veya dosya olarak ayrı bir kayıt türünde tutulması gerekip gerekmediğine karar verin.
- Doğru kasayı, kayıt sahibini ve saklama amacını doğrulayın.
- Başlık, kategori ve etiketlerin içeriği açmadan kaydı tanımlayabildiğinden; fakat müşteri veya sistem sırrı açıklamadığından emin olun.
- Toplu işlemde görünür kayıt sayısı ile seçili kayıt sayısını karşılaştırın.

## Güvenli Kanıt

- **Paylaşılabilir:** ekranın adı, yaklaşık olay zamanı, kayıt türü, maskelenmiş kategori veya etiket yapısı ve görünen hata kodu.
- **Gizli kalmalı:** not başlığı, not içeriği, gizli alan, iç sistem adı, kurtarma ayrıntıları, kullanıcı veya müşteri bilgisi ve panoya kopyalanan metin.

Bir sorunu anlatmak için gerçek not içeriği gerekmez. Hata yalnız belirli içerikle oluşuyorsa sentetik bir notla yeniden üretin. Gerçek içeriğin incelenmesi zorunluysa herkese açık bir issue yerine özel destek kanalını kullanın.

## İlgili

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Destek kanıt paketi](support-evidence-pack.md)
- [Herkese açık issue'larda maskeleme](../../kb/tr/public-issue-redaction.md)
