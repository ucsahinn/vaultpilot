# Etki Alanı

Üst çubuktaki `?` simgesi bu yardımı Etki Alanı açıkken getirir. Bu ekran farklı kaynaklardan gelen dört özeti bir araya getirir: DC Agent'ın eşitleme anlık görüntüsü ve seçilmiş dizin kapsamı, kasadaki RDP/SSH kimlik bilgileri, erişim denetim kayıtları, dizin iş kuyruğu ve daha önce yüklenmiş olabilecek tarayıcı oturumları. Bu veriler aynı kapsama veya aynı yenilenme zamanına sahip değildir; ekrandaki toplamları Active Directory'nin eksiksiz envanteri olarak yorumlamayın.

Etki Alanı ekranı çoğunlukla bir inceleme yüzeyidir. Bazı kartlar filtreli ayrıntı ekranı açar, bazı metrikler ise yalnız bilgi verir. Dolu bir bileşende genel bir **İlgili ekrana git** menüsü bulunmaz; bu çağrı yalnız bileşenin küçük boş durumunda görünebilir. Dolu görünümde yalnız düğme olarak sunulan karta basın veya sol gezinmeden ilgili çalışma alanına geçin.

## Ekrandaki Dört Bileşen

### Etki alanı envanteri

Canlı ajan oranı, kullanıcı, grup/OU ve risk sinyali metriklerini; sağlayıcı adı, son görülme/eşitleme zamanı ve seçilmiş oturum açma/kimlik bilgisi sayılarını gösterir. Kaynağı, yalnız Sahip rolünde çalışan dizin sağlayıcısı sorgusudur. Bu bileşenin içindeki topoloji, metrikler ve sağlayıcı satırları salt okunurdur; ayrıntı için sol gezinmeden Entegrasyonlar > Active Directory ekranına geçin.

### Etki alanı eşitleme sağlığı

Nesne dağılımındaki tıklanabilir **Kullanıcı**, **Grup** ve **OU** satırları Entegrasyonlar'da karşılık gelen ağaç filtresini açar; sayı sıfırsa veya Sahip yetkisi yoksa pasiftir. **Cihaz**, **Ayrıcalıklı** ve **Eski nesne** satırları salt okunurdur. **Ajan kuyruğu** kartı, bekleyen/kiralanmış dizin işi sayısını kullanır ve değer sıfırdan büyükken sistem görünürlüğü olan rolleri İşlemler ekranına götürür. Diğer kapsam kartları ile ajan sağlık satırları bilgi amaçlıdır.

### Uzak oturumlar

Tıklanabilir RDP ve SSH kartları, kasadaki kimlik bilgisi kayıtlarının sayısını ve bu kayıtlara ait denetim erişimlerini birleştirir; Active Directory Kayıtları ekranını ilgili protokole göre filtreler. **AD oturum açma** kartı sağlayıcıdaki seçilmiş oturum açma kapsamını gösterir ve salt okunurdur. **Ajan kuyruğu** kartı dizin işlerinden gelir ve İşlemler ekranına gidebilir. Erişim grafiği denetim kayıtlarından, tarayıcı oturumu satırları ise oturum sorgusundan beslenir. Etki Alanı bu oturum sorgusunu ayrıca çalıştırmadığı için yalnız daha önce yetkili bir güvenlik ekranında yüklenmiş önbellek görünebilir; güncel inceleme için Giriş Güvenliği ekranını kullanın.

### Kimlik bilgisi yaşam döngüsü

Bu bileşen kasadaki Active Directory kimlik bilgileri ile bunlara ait denetim erişimlerinden üretilir; dizin seçimi toplamlarını kullanmaz. **Kimlik bilgileri**, **Yönetilen**, **Süresi dolan** ve **Bilgi eksik** kartları tıklanabilir ve Active Directory Kayıtları ekranını ilgili durum filtresiyle açar. **Kullanımda** ve **Güncellenen** kartları salt okunurdur. “Yönetilmeyen” adlı bir yaşam döngüsü kartı yoktur. Erişim grafikleri ile cihaz, kimlik bilgisi, son erişim ve toplam sütunlarını gösteren tablo da salt okunurdur.

## Yetki, Veri ve Ajan Yetenekleri

Etki alanı sağlayıcı sorgusu yalnız **Sahip** rolünde etkinleşir. **Yönetici**, **Denetçi** veya **Kullanıcı** ekran kabuğuna ulaşsa bile boş ya da sıfır değerler “ajan yok” anlamına gelmez; bu durum **yetki nedeniyle veri yüklenmedi** olarak değerlendirilmelidir. Sahip oturumunda da önce sorgunun tamamlandığını doğrulayın.

Ajanın ilan ettiği yetenekler gösterilebilecek veri ve yapılabilecek işlemleri sınırlar. Envanter için `READ_INVENTORY`, parola durumu için `READ_PASSWORD_STATE`; hesap açma, sonraki girişte parola değişikliği isteme ve geçici parola atama için ilgili `UNLOCK_ACCOUNT`, `REQUIRE_PASSWORD_CHANGE` ve `RESET_TEMP_PASSWORD` yetenekleri gerekir. Bir yetenek yoksa sıfır veya eksik metrik “risk yok” demek değildir; veri toplanmamış olabilir. Hassas dizin eylemleri ayrıca ajanın `CONNECTED` olmasını, lisansın yazılabilir kalmasını, Sahip rolünü ve hedef hesabın ayrıcalıklı olmamasını gerektirir.

## Önerilen İnceleme Akışları

### Ajan sağlığını doğrulama

1. Etki alanı envanterindeki canlı ajan oranını, sağlayıcı durumunu ve son görülme/eşitleme zamanını okuyun.
2. Durum etiketinin önceliğini doğru okuyun: ajan sağlığı `CONNECTED` değilse önce `STALE`, `OFFLINE`, `AWAITING` veya `REVOKED` görünür. Ajan bağlıyken hata varsa **HATA**, ardından etkin eşitleme varsa **EŞİTLENİYOR**, yalnız bunlar yokken bekleyen komut varsa **EŞİTLEME KUYRUKTA** gösterilir.
3. Bağlı olmayan veya hata gösteren sağlayıcı için sol gezinmeden Entegrasyonlar > Active Directory ekranını açın ve sağlayıcı kartını inceleyin.

Beklenen sonuç `CONNECTED` durumu ile ilerleyen son görülme ve eşitleme zamanıdır. Zaman ilerlemiyorsa yeni kimlik bilgisi aktarımı veya kapsam değişikliği başlatmayın.

### Seçim kapsamını sayılarla karşılaştırma

Etki alanı eşitleme sağlığındaki tıklanabilir **Kullanıcı**, **Grup** veya **OU** satırını açın ve Entegrasyonlar'daki hazırlanmış filtreyi kontrol edin. Bilgisayar sayısı salt okunurdur; bilgisayar kapsamı için Entegrasyonlar'a sol gezinmeden geçin. Beklenmeyen artış veya düşüşte son başarılı eşitlemeyi ve ajan yeteneklerini karşılaştırın. Tamamlanma ölçütü, değişimin onaylı kapsam güncellemesiyle veya kaynak sistemde doğrulanmış bir sorunla açıklanmasıdır.

### RDP/SSH sinyalini inceleme

Değeri olan RDP ya da SSH kartını seçin; açılan Active Directory Kayıtları ekranında protokol filtresinin uygulandığını doğrulayın. Kayıt kaynağını, risk etiketini ve son eşitleme zamanını inceleyin. Tarayıcı oturumu satırını veya erişim grafiğini tıklayarak ayrıntı beklemeyin; bu bölümler yalnız özet sunar.

### Yaşam döngüsü durumunu inceleme

Yalnız **Kimlik bilgileri**, **Yönetilen**, **Süresi dolan** veya **Bilgi eksik** düğmelerinden birini açın. **Kullanımda**, **Güncellenen** ve erişim tablosu yalnız özet sunar. Kaynağı `ad_sync` olan bir kaydı elle yeniden oluşturmayın. Kayıt ile dizin nesnesi uyuşmuyorsa eşitleme tamamlanana kadar toplu işlem başlatmayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Yükleniyor | Sahip rolüne ait sağlayıcı sorgusu tamamlanmadan toplamları ve boş durumları yorumlamayın. |
| Bağlı (`CONNECTED`) | Hata, etkin eşitleme veya bekleyen komut yoksa son görülme/eşitleme zamanlarını ve gerekli yetenekleri doğrulayın. |
| HATA | Bağlı ajan üzerindeki hata, eşitleme ve kuyruk etiketlerinden önce gösterilir; sağlayıcı kartındaki son hatayı inceleyin. |
| EŞİTLENİYOR (`SYNCING`) | Yalnız bağlı ve hatasız ajanda görünür; işlemin tamamlanmasını bekleyin. |
| EŞİTLEME KUYRUKTA | Yalnız bağlı, hatasız ve eşitleme çalışmayan ajanda görünür; bekleyen işi İşlemler ekranında izleyin. |
| Bekliyor (`AWAITING`) | İlk ajan yoklaması tamamlanana kadar aktarım ve hassas işlem başlatmayın. |
| Bayat (`STALE`) | Ajan servisini, sunucu erişimini ve sağlayıcı kartındaki son hatayı kontrol edin. |
| Çevrimdışı (`OFFLINE`) | Yeni dizin işlemlerini durdurun; servis ve bağlantı kanıtını özel olarak toplayın. |
| İptal edilmiş (`REVOKED`) | Eski ajan anahtarını kullanmayın; Sahip onaylı yeniden kayıt veya onarım akışını izleyin. |
| Yetki nedeniyle boş | Sahip olmayan rolde sıfır değeri “ajan yok” diye raporlamayın; incelemeyi Sahip kullanıcıya aktarın. |
| Yetenek eksik | İlgili veri veya eylemi desteklenmiyor kabul edin; eksik metriği sağlıklı sonuç olarak yorumlamayın. |
| Hata | Son başarılı eşitleme zamanını koruyun; art arda kapsam değiştirerek ilk hatayı gölgelemeyin. |

## İşlemden Önce

- Rolün Sahip olduğunu, sağlayıcı sorgusunun tamamlandığını ve gösterilen tarih-saat bilgilerinin güncel olduğunu doğrulayın.
- Ajan sağlık durumu ile son başarılı eşitleme zamanını birlikte değerlendirin.
- İhtiyaç duyulan veri veya eylem için gerekli ajan yeteneğinin ilan edildiğini kontrol edin.
- Ekrandaki salt-okunur metrik ile tıklanabilir filtre kartını birbirinden ayırın.
- Kimlik bilgisi aktarımı için aktif kasanın açık, yazılabilir ve kasa anahtarının erişilebilir olduğunu doğrulayın.
- Ayrıcalıklı hesaplarda hassas eylemleri zorlamayın; kurumun onaylı Active Directory yönetim yolunu kullanın.

## Güvenli Kanıt

- **Paylaşılabilir:** ajan sağlık kategorisi, son görülme/eşitleme yaşı, nesne türüne göre kimliksizleştirilmiş toplam, kuyruk durumu, ilan edilen yetenek adı ve kişisel veri içermeyen hata kodu.
- **Gizli kalmalı:** etki alanı ve etki alanı denetleyicisi adları, distinguished name, OU/grup yolu, bind kullanıcısı, ajan anahtarı, gerçek kullanıcı listesi, RDP/SSH hedefi ve dizin ağacı ekran görüntüsü.
- Günlük gerekiyorsa kullanıcı, etki alanı, IP, anahtar ve LDAP ayrıntılarını çıkarın. Tam maskeleme mümkün değilse yalnız özel destek kullanın.

## Ne Zaman Yükseltmelisiniz

Ajan `CONNECTED` durumuna dönemiyorsa, eşitleme veya kuyruk ilerlemiyorsa, seçilmiş kapsam beklenmedik biçimde değişiyorsa, gerekli yetenek kaybolmuşsa ya da bu ekran Active Directory Kayıtları ile çelişiyorsa konuyu dizin yönetimi ekibine aktarın. Ajan sürümünü, genel sağlık durumunu, saat dilimi belirtilmiş tarih ve saati, hassas ayrıntıları çıkarılmış hatayı ve denenen ön kontrol adımlarını ekleyin.

## Operatör Notları

Nesne sayıları kapasite ve sağlık sinyalidir; herkese açık kimlik envanteri değildir. Active Directory ve ajan, dizin kaynaklı kimlik bilgisi kayıtlarının asıl kaynağıdır. Aynı kaydı elle oluşturmak kopya ve yanlış rotasyon riski doğurur.

## İlgili

- [Active Directory ajanı](active-directory-agent.md)
- [Active Directory kayıtları ekranı](screen-active-directory-records.md)
- [Giriş güvenliği ekranı](screen-sign-in-security.md)
- [DC Agent sorun giderme](../../kb/tr/dc-agent-service.md)
