# Bildirimler Ekranı

Üst çubuktaki `?` simgesi Bildirimler ekranına ait bu rehberi açar. Bu ekran, hangi kalıcı denetim olaylarının SMTP e-postasına aday olacağını ve e-postaların hangi adreslere yönlendirileceğini yönetir. SMTP sunucu bağlantısı ayrı **Sunucu ayarları > SMTP** sekmesindedir; üst çubuktaki canlı uygulama bildirimleri ise farklı, oturuma bağlı bir yüzeydir.

## Erişim, Rol ve Lisans Sınırı

Sahip, Yönetici ve Denetçi sistem rolleri Bildirimler ekranını açabilir. Yalnız **Sahip** alıcıları ve olay seçimlerini değiştirebilir, ayarları kaydedebilir ve SMTP testi gönderebilir. Yönetici ile Denetçi aynı veriyi salt okunur görür. Kullanıcı rolü sistem ayarlarını görüntüleyemediği için bu ekrana erişemez.

Bildirimler ayrı bir lisans özelliğiyle kapatılmaz. Ekrandaki **Salt okunur** durumu lisans modunu değil, Sahip dışındaki sistem rolünü anlatır. Kasa yazmalarını kapatan salt okunur lisans da Sahip için bu sunucu düzeyi ayarları veya SMTP testini kendiliğinden devre dışı bırakmaz; işlem öncesinde kurum politikanızı ayrıca uygulayın.

## Burada Ne Yapılır

- SMTP'nin açık/kapalı durumunu, tanımlı alıcı sayısını ve seçili olay kuralı sayısını okuyun.
- **E-posta alıcıları** alanında adresleri ekleyin, tekilleştirin veya kaldırın.
- **Test alıcısı** ile geçerli SMTP form değerlerini kaydetmeden önce kontrollü olarak sınayın.
- **Tümü**, **Seçilenler**, **Info**, **Suspicious** ve **Critical** filtreleriyle olay kataloğunu daraltın.
- Tek bir olayın, bütün bir önem grubunun veya tüm kataloğun e-posta seçimini değiştirin.
- Her satırdaki **Anında**, sessizlik aralığı veya eşik politikasını okuyup gürültü ve görünürlük dengesini kurun.
- **Bildirimleri kaydet** ve **Sıfırla**, Bildirimler ile diğer Sunucu ayarları sekmelerinin paylaştığı formun tamamında çalışır. Başka bir sekmede kaydedilmemiş değişiklik varken bu düğmeleri kullanmayın.

## Ekranın Yapısı

Bildirimler ekranının kendi içinde sekme yoktur. Üst durum şeridi ve iki ana alan bulunur:

- SMTP durum düğmesi ve **SMTP ayarları**, **Sunucu ayarları > SMTP** sekmesini açar.
- **Teslimat** alanı alıcı listesini ve test gönderimini içerir.
- **Olay kuralları** alanı filtreleri, toplu seçimleri, önem gruplarını ve tek tek olay satırlarını içerir.

Durum şeridindeki **Gönderime hazır**, yalnız formda SMTP açık, host ve gönderen adresi dolu, en az bir alıcı ve en az bir olay seçili olduğu anlamına gelir. SMTP bağlantısının çalıştığını, uzak sunucunun iletiyi kabul ettiğini veya alıcının gelen kutusuna teslim edildiğini kanıtlamaz.

## Teslimat ve SMTP

### Alıcı listesi

Her satır, virgül veya noktalı virgül ayrı alıcı kabul edilir. Adresler kaydetme öncesinde küçük harfe çevrilir, boş girdiler kaldırılır ve aynı adres yalnız bir kez tutulur. SMTP açıkken host, gönderen e-posta ve en az bir alıcı zorunludur. Kimlik doğrulama açıksa kullanıcı adı ile yeni ya da önceden kaydedilmiş parola/erişim anahtarı gerekir.

Bildirimler ekranı SMTP hesabı, host, port, gönderen adresi, TLS/STARTTLS, kimlik doğrulama kullanıcı adı veya parolayı düzenlemez. Bunlar **SMTP ayarları** üzerinden ayrı sekmede yönetilir. SMTP kapatıldığında bağlantı ayrıntıları saklanır; denetim kayıtları ve oturum içi uygulama bildirimleri devam eder, e-posta gönderimi durur. Bu sırada oluşan olayların e-posta adayları işleme sırasında atlanır ve ilgili çıkış kuyruğu satırları silinir; SMTP yeniden açıldığında geriye dönük gönderilmez.

### Test gönderimi

**Test gönder** yalnız Sahip rolünde, SMTP açıkken ve başka test sürerken değilken kullanılabilir. Test için şu değerler gerekir:

- Geçerli `1-65535` portu,
- SMTP hostu ve gönderen e-posta,
- ayrı **Test alıcısı**,
- kimlik doğrulama açıksa kullanıcı adı ile formdaki veya önceden kaydedilmiş parola/erişim anahtarı.

Test, henüz kaydedilmemiş geçerli SMTP form değerlerini kullanabilir. SMTP açıkken sunucu test isteğinde de en az bir bildirim olayı seçimi ister; seçim sıfırsa düğme kullanılabilir görünse bile test doğrulamada reddedilir. Sunucu on dakikada en fazla beş test isteği kabul eder. Başarı mesajındaki adres, SMTP sunucusunun alıcıyı kabul ettiğini gösterir; gelen kutusuna, karantinaya veya son kullanıcıya kesin teslim kanıtı değildir. Başarılı test `SERVER_MAINTENANCE` denetim olayı yazar. Başarısız test ekranda hata ve canlı uygulama bildirimi üretir, ancak otomatik olarak başarılı teslimat kanıtı oluşturmaz. Mevcut test e-postası şablonu Türkçe hazırlanır; arayüz dilini değiştirmek test iletisinin dilini değiştirmez.

## Olay Kuralları ve Önem Grupları

Filtreler yalnız görünür satırları değiştirir; kayıtlı seçimi değiştirmez:

| Filtre | Gösterdiği |
| --- | --- |
| Tümü | SMTP için tanımlı bütün denetim olayları. |
| Seçilenler | Şu anda e-posta adayı olarak işaretlenmiş olaylar. |
| Info | Bakım ve bilgilendirme olayları. |
| Suspicious | Şüpheli erişim ve inceleme isteyen sinyaller. |
| Critical | Kritik güvenlik ve işlem gerektiren olaylar. |

**Tümünü seç** bütün olayları işaretler. **Temizle** bütün işaretleri kaldırır. SMTP açıkken seçim sıfırsa **Bildirimleri kaydet** kapalı kalır ve SMTP testi de sunucu doğrulamasında reddedilir; kaydetmeden veya test etmeden önce en az bir olay seçin. SMTP kapalıyken olay seçimi olmadan ayar kaydedilebilir.

Grup başlığındaki onay kutusu o önem düzeyindeki bütün olayları açar veya kapatır; kısmi seçim kutuda karma durum olarak görünür. Tek satır kutusu yalnız o olayı değiştirir. Seçilmemiş olaylar silinmez ve Denetim Geçmişinde kalır; yalnız SMTP e-postasına aday olmaz.

### İletim politikası

Seçilmiş olmak her olayda hemen bir e-posta gönderileceği anlamına gelmez. Her satır kendi politikasını gösterir:

- **Anında:** olay oluştuğunda SMTP kuyruğuna aday olur.
- **İlk olay, sonra N dk sessizlik:** ilk olay aday olur; aynı grup sessizlik süresince bastırılır.
- **N olay / M dk:** yalnız belirtilen zaman aralığında eşik oluştuğunda aday olur.

Gruplama olaya göre aktör veya aktör-hedef temelinde yapılabilir. Sunucu aday e-postaları kalıcı çıkış kuyruğunda işler ve geçici hataları sınırlı sayıda yeniden dener; kalıcı ret veya deneme sınırı son teslimi engelleyebilir. Bildirimler ekranında alıcı bazlı teslim makbuzu, okunma bilgisi veya çıkış kuyruğu geçmişi yoktur. Bu nedenle kural seçimi ya da **Kurallar hazır** durumu teslimat garantisi değildir.

## Canlı Bildirimler ile Kalıcı Olayların Farkı

Üst çubuktaki zil ve yaklaşık 5,2 saniye görünen anlık bildirimler, bu tarayıcı oturumundaki işlem başarıları, hataları ve sistem iletileridir. En fazla üç anlık bildirim aynı anda gösterilir. Zil merkezi oturum belleğinde en fazla 30 bildirimi tutar ve son sekizini listeler; aynı tür ve metindeki tekrarlar tek kayda indirgenir.

**Okundu işaretle** zaman damgasını koruyarak mevcut kayıtları okundu yapar. Okunmuş kayıt varsa **Okunanları temizle** yalnız onları kaldırır; hiç okunmuş kayıt yoksa **Tümünü temizle** geçerli oturum listesini boşaltır. Tek satırdaki kapatma düğmesi o bildirimi ve varsa açık anlık bildirimi kaldırır.

Bu canlı liste sunucu veritabanına kalıcı yazılmaz ve sayfa/oturum yenilenince geri gelmesi beklenmez. Zil merkezini temizlemek Denetim Geçmişini, SMTP çıkış kuyruğunu, kayıtlı olay kurallarını veya gönderilmiş e-postayı silmez. Tersine, bir denetim olayının kalıcı olması onun mutlaka canlı bildirim ya da e-posta üreteceği anlamına gelmez.

## Önerilen İş Akışları

### İlk SMTP bildirim kurulumunu doğrulama

1. **SMTP ayarları** üzerinden SMTP'yi açın; host, port, gönderen, TLS ve gerekiyorsa kimlik doğrulamayı doldurun.
2. Bildirimler ekranına dönüp en az bir gerçek alıcı girin.
3. Önce dar bir olay kümesi seçin; her satırın eşik veya sessizlik politikasını okuyun.
4. Ayrı test alıcısına **Test gönder** kullanın ve SMTP kabul sonucunu doğrulayın.
5. Gelen kutusu, istenmeyen posta/karantina ve kurum ağ geçidi kayıtlarını ayrıca kontrol edin.
6. Diğer Sunucu ayarları sekmelerinde kaydedilmemiş değişiklik olmadığını doğrulayın; ardından **Bildirimleri kaydet** seçeneğini kullanıp sayfayı yeniden açarak alıcı ve olay sayılarının korunduğunu doğrulayın.

### Gürültüyü azaltma

1. **Seçilenler** filtresiyle yalnız e-posta adayı olayları gösterin.
2. Önce yüksek hacimli satırların eşik ve sessizlik politikasını okuyun.
3. İnsan müdahalesi gerektirmeyen satırları tek tek kapatın; bütün önem grubunu yalnız açık bir kurum kararıyla kapatın.
4. Ayarı kaydedin ve değişmeyen olayların Denetim Geçmişinde kalmaya devam ettiğini doğrulayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Sunucu ayarları yükleniyor | Panelde ayrı iskelet yoktur; değerler yüklenene kadar varsayılan SMTP kapalı görünümünü kesin durum saymayın ve kaydetmeyin. |
| Sunucu ayarları alınamadı | Panel ayrı hata kartı göstermeyebilir. Beklenen alıcı veya kurallar yoksa Sunucu ayarlarını ve bağlantıyı doğrulayıp sayfayı yenileyin; boş formu mevcut ayarların üstüne yazmayın. |
| SMTP kapalı | E-posta gönderimi yoktur; denetim ve oturum içi bildirimler devam eder. Bu sırada atlanan e-posta adayları kuyruktan silinir ve SMTP yeniden açıldığında geriye dönük gönderilmez. |
| Eksik ayar var | SMTP açık olsa da host, gönderen, alıcı veya olay seçimi eksiktir; hazır kabul etmeyin. |
| Gönderime hazır / Kurallar hazır | Yalnız form bütünlüğü sağlanmıştır; test ve alıcı tarafı doğrulaması hâlâ gerekir. |
| Alıcı yok | SMTP açıkken en az bir geçerli adres ekleyin. |
| Olay seçili değil | SMTP açıksa en az bir olay seçmeden kaydedemezsiniz; test düğmesi kullanılabilir görünse bile sunucu test isteğini doğrulamada reddeder. |
| Filtrede olay yok | **Tümü** veya başka önem filtresine geçin; kayıtlı seçim kendiliğinden değişmez. |
| Test gönderiliyor | İkinci test başlatmayın; sonuç veya hata bildirimini bekleyin. |
| Test kabul edildi | SMTP sunucusu adresi kabul etmiştir; gelen kutusu teslimini ayrı doğrulayın. |
| Test gönderilemedi | Host, port, TLS, kimlik doğrulama, gönderen, alıcı ve ağ erişimini gizli değer göstermeden kontrol edin. |
| Rol nedeniyle salt okunur | Yönetici ve Denetçi kuralları görebilir fakat değiştiremez, kaydedemez veya test gönderemez. |
| Kaydedilmemiş değişiklik | Paylaşılan form başka Sunucu ayarları sekmelerindeki değişiklikleri de içerir. **Bildirimleri kaydet** bunları birlikte yazabilir; **Sıfırla** bunları da son yüklenen değerlere döndürebilir. |
| Canlı bildirim yok | Bu yalnız geçerli tarayıcı oturumunda yeni işlem sonucu olmadığını gösterir; denetim geçmişinin boş olduğunu göstermez. |

## İşlemden Önce

- Oturum rolünü kontrol edin; alıcı, kural, SMTP testi ve kaydetme işlemleri için Sahip gerekir.
- **Bildirimleri kaydet** veya **Sıfırla** kullanmadan önce diğer Sunucu ayarları sekmelerinde kaydedilmemiş değer olmadığını doğrulayın; bu işlemler paylaşılan formun tamamını etkiler.
- SMTP kanalının açık olduğunu ve **Gönderime hazır** ifadesinin yalnız form yeterliliği olduğunu unutmayın.
- Alıcı adresinin kurum içi onayını, veri sınıflandırmasını ve nöbet sorumluluğunu doğrulayın.
- Olay satırının önem grubunu ve gerçek iletim politikasını okuyun; seçili olayı otomatik olarak anında e-posta sanmayın.
- Değişiklik öncesi mevcut alıcı sayısını ve seçili olay sayısını kaydedin; gizli adresleri açık kanıta koymayın.
- Testte kaydedilmemiş SMTP değerlerinin kullanılabileceğini ve hız sınırı olduğunu hesaba katın.
- Canlı zil bildirimleri ile kalıcı Denetim Geçmişini birbirinin yerine kullanmayın.

## Güvenli Kanıt

- Paylaşılabilir: SMTP açık/kapalı sınıfı, redakte host sınıfı, port ve TLS modu, alıcı sayısı, olay adı/önem grubu, iletim politikası, genel hata kodu ve geniş zaman aralığı.
- Gizli kalmalı: SMTP kullanıcı adı ve parola/erişim anahtarı, gerçek alıcı ve gönderen adresleri, tam host adı, ileti kimliği, konu/gövde, denetim hedefi, kullanıcı/kasa adı, olay zamanı ve kurum içi yönlendirme bilgisi.
- Test sonucu paylaşırken kabul edilen gerçek adresi, SMTP hostunu ve ileti kimliğini maskeleyin; **kabul edildi** ifadesini son teslim kanıtı olarak sunmayın.
- Ekran görüntüsünde yalnız kırpma yapmayın; adres, host, olay hedefi, kullanıcı, zaman ve müşteri bağlamını tamamen maskeleyin.

## Ne Zaman Durmalı ve Destek İstemelisiniz

Yüklenen değerlerin güncel olduğundan emin değilseniz, beklenen alıcılar kaybolduysa, SMTP testi yanlış adrese gittiyse, kimlik bilgisi açık kanala düştüyse, kritik olaylar denetimde bulunduğu hâlde kuyruk/posta kanıtı oluşmuyorsa veya aynı kural beklenmedik ölçüde fazla ileti üretiyorsa değişiklik yapmayı bırakın. Gizli değer eklemeden; genel SMTP durumu, redakte olay adı, iletim politikası, geniş zaman aralığı, hata kodu ve son güvenli adımla özel destek kaydı açın.

## Operatör Notları

Bildirimler ekranı bir posta kutusu veya teslimat izleme konsolu değildir. Alıcı ve olay kurallarını kaydeder; gerçek SMTP bağlantı ayrıntıları Sunucu ayarlarındadır. Denetim kaydı, SMTP kuyruğu/e-postası ve tarayıcı oturumundaki canlı bildirim üç ayrı yaşam döngüsüne sahiptir.

SMTP parolası/erişim anahtarı, gerçek e-posta adresi, müşteri hostu, ileti kimliği, tam hata yanıtı veya olaya özel gizli değer içeren bildirim örneğini yayımlamayın.

## İlgili

- [Sunucu ayarları ekranı](screen-server-settings.md)
- [Denetim Geçmişi ekranı](screen-audit-log.md)
- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Sunucu ayarları yeniden başlatma ve bakım bilgi bankası](../../kb/tr/server-settings-restart-maintenance.md)
