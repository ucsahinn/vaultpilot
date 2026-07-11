# Denetim Kaydı Ekranı

Üst çubuktaki `?` simgesi Denetim Kaydı ekranına ait bu rehberi açar. Bu ekran yalnız kronolojik bir liste değildir; işlemi yapan kişi, etkilenen hedef, rol, zaman, işlem ayrıntıları ve bütünlük özetlerini aynı bağlamda incelemenizi sağlar.

Arayüzdeki **Operasyon > Denetim kaydı** bağlantısı yalnız Sahip, Yönetici ve Denetçi rollerine gösterilir. Buna karşılık denetim listesini döndüren GET API'si, normal Kullanıcı rolü dahil tüm doğrulanmış oturumları kabul eder. Menü görünürlüğü ile API yetkisini aynı şey saymayın; her istek için sunucunun uyguladığı rol denetimi belirleyicidir. Ekran mevcut olayları değiştirmez. CSV ve Excel dışa aktarımları yalnız o anda filtrelenmiş ham olayları kapsar.

## Burada Ne Yapılır

- Üstteki kategori düğmeleri, **İşlem türü** seçimi ve **Denetimde ara** alanıyla gürültüyü azaltın.
- Sonuç özetindeki ham olay sayısını, seçili kategoriyi ve işlem türünü dışa aktarmadan önce kontrol edin. Arama metni bu özette gösterilmez.
- Bir satırı açarak aktör, hedef, rol, zaman, işlem ayrıntıları, bu olayın özeti ve önceki olayın özetini birlikte okuyun.
- **Filtreleri temizle** ile başlangıç görünümüne dönebilir; CSV veya Excel ile yalnız görünen sonuçları dışa aktarabilirsiniz.
- Bir satırdaki `Nx` işareti, aynı dakika içinde aynı işlem–aktör–hedef birleşimindeki olayların arayüzde gruplanmış olduğunu gösterir.

## Ekranı Nasıl Okumalısınız

Kategori düğmeleri olayları anlamlı gruplara ayırır ve her düğmedeki sayı o gruptaki ham olay miktarını gösterir. **İşlem türü** belirli bir eylemi, arama alanı ise işlem adı, aktör, hedef, anlatım, ayrıntı metni, zaman, olay özeti ve hedef kimliği içinde eşleşme bulmaya yardım eder. Ayrı aktör, hedef, risk veya zaman filtresi yoktur.

Sonuç özeti ham olay sayısını, seçili kategoriyi ve işlem türünü gösterir; arama metnini göstermez. Aynı işlem, aktör ve hedef için aynı dakika içinde oluşan olaylar ekranda tek temsilci satır altında `Nx` biçiminde gruplanır. Bu satıra tıklamak grubun tüm üyelerini değil, temsilci olayı ayrıntı panelinde açar. Kategori sayaçları, sonuç özeti ve dışa aktarımlar ise gruplanmamış ham olayları sayar.

Ayrıntı panelinde aktör, hedef, rol, zaman, işlem ayrıntıları, bu olayın özeti ve önceki olayın özeti görünür. Bunlar operatörün elle karşılaştıracağı kanıt alanlarıdır; ekran “tam”, “kısmi” veya “geçersiz zincir” sonucu hesaplamaz. Özellikle kritik değişikliklerde komşu olayları ayrı ayrı açarak sırayı ve özet bağlantısını doğrulayın.

## İnceleme İş Akışları

### Belirli bir değişikliği bulma

1. Olayın yaklaşık zamanını ve olası aktör ya da hedefi belirleyin.
2. Önce kategori, sonra **İşlem türü** seçin.
3. **Denetimde ara** alanını son daraltma adımı olarak kullanın.
4. Satırı açıp aktör, hedef, rol ve zamanın beklenen işlemle örtüştüğünü doğrulayın.

Beklenen sonuç, tek bir olayı yakınındaki olaylardan koparmadan tanımlamaktır. Sonuç yoksa hemen “kayıt tutulmamış” sonucuna varmayın; **Filtreleri temizle** kullanın, saat dilimini ve arama yazımını kontrol edip yeniden deneyin.

### Olay özetlerini elle karşılaştırma

1. İlgili olayın ayrıntısını açın.
2. Bu olayın özeti ile önceki olayın özetini kaydedin.
3. Satır `Nx` ile gruplanmışsa ayrıntı panelinin yalnız temsilci olayı gösterdiğini not edin.
4. Aynı zaman aralığındaki önceki ve sonraki ham olayları arama ve dışa aktarma yardımıyla karşılaştırın.

Özetlerin bulunması, zincirin uygulama tarafından doğrulandığı anlamına gelmez. Önceki özetin boş, beklenmedik veya komşu olayla uyuşmaz görünmesi halinde ham kayıtları değiştirmeyin; dar zaman aralığı ve redakte edilmiş bağlamla özel destek akışına geçin.

### Dar kapsamlı kanıt dışa aktarma

1. Kategori, işlem türü ve arama metnini olaya ilişkin en küçük kapsama getirin.
2. Ham olay sayısını, kategori ve işlem türünü not edin; arama metnini ayrıca kaydedin.
3. Hangi alanlara ihtiyacınız olduğuna göre CSV veya Excel uyumlu tabloyu seçin.
4. İndirilen dosyanın yanında filtreleri ayrı bir inceleme notunda saklayın; dosya kendi filtre kapsamını içermez.
5. Orijinali özel ve değişmez tutun; paylaşılacak kopyada kullanıcı, nesne, IP ve müşteri bağlamını redakte edin.

CSV; `created_at`, `action`, `actor`, `target`, `summary`, `details`, `target_id`, `integrity_hash` ve `previous_hash` alanlarını içerir. **Excel** düğmesi gerçek `.xlsx` değil, Excel uyumlu HTML tablo taşıyan `.xls` dosyası üretir; Created, Action, Actor, Target, Summary, Details ve Integrity hash sütunlarını içerir, ancak `target_id` ile `previous_hash` alanlarını içermez.

Görünen ham olay sayısı sıfırsa iki dışa aktarma düğmesi de pasiftir; boş dosya üretilmez. Her dışa aktarma, dosyayı indirdikten sonra sunucuya bir `EXPORT` denetim olayı yazma isteği gönderir ve listeyi yeniler. Bu olay yalnız sunucu yazma isteğini kabul ederse kaydedilir. Örneğin Denetçi dosyayı indirebilir, ancak Denetçi rolü denetim olayı oluşturamadığı için `EXPORT` olayı listeye eklenmeyebilir. Yeni olay kaydedilse bile kendisinden önce hazırlanmış dosyanın içinde yer almaz.

### Aktif olay sırasında güvenli duruş

Yetkisiz erişim şüphesi, açıklanamayan rol değişikliği veya olay özetlerinde beklenmeyen bağlantı varsa kritik olmayan yönetim işlemlerini durdurun. İlgili zaman aralığını, gerçek filtre kapsamını ve olay özetlerini koruyup olay müdahale sorumlusuna aktarın. İnceleme sürerken kayıt temizliği veya saklama süresi değişikliği yapmayın.

## Ekran Durumları ve Operasyonel Koşullar

| Durum | Operatör cevabı |
| --- | --- |
| Yükleniyor | Filtreleri değiştirmeden iskelet satırların tamamlanmasını bekleyin. |
| Filtre sonucu boş | Filtreleri temizleyin; zaman ve arama ifadesini yeniden doğrulayın. |
| Gruplanmış `Nx` satırı | Satırın temsilci olayı açtığını; sayaç ve dışa aktarımın ham olayları kullandığını unutmayın. |
| Dışa aktarma kapalı | Filtrelenmiş ham olay sayısı sıfırdır; filtreleri gözden geçirin. |
| Dışa aktarma tamamlandı | Dosyanın kapsam notunu saklayın; `EXPORT` olayı yalnız sunucu yazma isteğini kabul ederse görünür. |

## İşlemden Önce

- Dışa aktarma öncesi kategori, işlem türü ve arama metnini ayarlayın; ayrı aktör, hedef veya zaman filtresi olmadığını unutmayın.
- Olay özetlerini karşılaştırırken yakın zamanlı ham olayları ve `Nx` gruplanmasını hesaba katın.
- Özet bağlantısı belirsizse ve aktif bir olay incelemesi sürüyorsa kritik olmayan değişiklikleri durdurun.
- Dışa aktarma dosyasının güvenli saklama konumunu ve kimlerle paylaşılacağını önceden belirleyin.
- Ham olay listesini etkileyebilecek temizlik veya saklama işlemlerini kanıt sorumlusuyla uzlaştırın.
- Arama metnini, saat dilimi varsayımını, kategori ve işlem türünü dosyadan ayrı kapsam notuna yazın.

## Güvenli Kanıt

- Paylaşılabilir: olay kategorisi, dar zaman aralığı, aktör rolünün maskelenmiş biçimi, olay özetinin kısa bölümü ve gerçek filtre kapsamı.
- Gizli kalmalı: kullanıcı adı, nesne kimliği, ham denetim dışa aktarımı, dahili IP ve müşteri bağlamı içeren olay materyali.
- Önceki olay özeti eksik veya beklenmedikse kanıtı koruyun; uygulamanın görünür bir zincir sağlık sonucu üretmediğini açıkça belirtin.
- Paylaşılabilir kopyada kategori, işlem türü, arama metni ve ham olay sayısı kalsın; dosyanın kendi başına bu kapsamı anlatmadığını unutmayın.
- Ham CSV/Excel dosyasını, ayrıntı panelindeki işlem ayrıntılarını veya müşteri bağlamını herkese açık bir kanala yüklemeyin.

## Ne Zaman Durmalı ve Destek İstemelisiniz

Olay özetleri komşu ham olaylarla uzlaştırılamıyorsa, ayrıntı aktör veya hedefle eşleşmiyorsa, dışa aktarma beklenen olayları vermiyorsa ya da aktif bir güvenlik olayı sürüyorsa yeni yönetim değişiklikleri yapmayın. Kategori, işlem türü, arama metni, dar zaman aralığı, aktör rolünün maskelenmiş biçimi ve olay özetleriyle özel destek kaydı açın; ham müşteri verisini paylaşmayın.

## Operatör Notları

Denetim kanıtı kullanıcı adı, dahili nesne kimliği ve işlem zamanını gösterebilir. Herkese açık kayıtlarda bunları redakte edin; gerçek olay materyali için özel destek kullanın.

## İlgili

- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Denetim zinciri inceleme KB](../../kb/tr/audit-chain-partial.md)
- [Destek kanıt paketi](support-evidence-pack.md)
