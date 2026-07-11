# Discovery Ekranı

Üst çubuktaki `?`, **Operasyon > Discovery** ekranından bu rehberi açar. Discovery; onaylı özel ağ, TLS ve dosya maruziyeti kontrolleri için denetimli bir inceleme alanıdır. Operatörün değerlendireceği sinyaller ve maskelenmiş kanıt üretir; zafiyet tarayıcısı, kimlik bilgisi deneme aracı, varlık envanteri veya otomatik temizlik servisi değildir.

## Erişim, Rol ve Lisans Sınırı

Lisans **Discovery** yeteneğini içeriyorsa Sahip, Yönetici ve Denetçi ekranı açabilir. Yönetici ve Denetçi; tarama kurallarını, çalışmaları, bulguları, bastırmaları ve içe aktarım durumunu salt okunur görür. Kullanıcı rolü bu ekrana ulaşamaz.

Her değişiklik Sahip rolü, Discovery yeteneği ve yazılabilir lisans ister. Tarama kaydetme, Önizleme veya Tarama çalıştırma, işi durdurma/yeniden başlatma/logunu silme, bulgu inceleme veya bastırma, içe aktarım materyali hazırlama ve içe aktarımı tamamlama bu sınıra dahildir. İçe aktarım için ayrıca Sahip'in Düzenleyici veya Yönetici olduğu etkin ve kilidi açık bir kasa gerekir.

Çalışma alanı açıkken yaklaşık on saniyede bir yenilenir. Yükleme sırasında üç satırlı iskelet, sorgu başarısızlığında ayrı hata paneli görünür.

## Üç Adımlı İş Akışı

1. **Çalıştır** — onaylı kapsamı oluşturup kaydedin, kontrolleri seçin, Önizleme kaydı alın veya gerçek tarama çalıştırın.
2. **Bulgular** — maskelenmiş sinyalleri filtreleyin, kanıtı inceleyin ve karar verin.
3. **İçe aktar** — uygun ve incelenmiş sınırlı sayıdaki dosya bulgusunu isteğe bağlı olarak etkin kasaya alın.

İçe aktarım zorunlu değildir. Ağ yüzeyi, sertifika sorunu veya zayıf dosya sinyali kasa kaydına dönüşmeden operatör bulgusu olarak kalabilir.

## Çalıştır: Onaylı Tarama Hazırlama

### Kontrolleri seçme

Yalnız seçilen ve kapsamı bulunan kontroller çalışır:

| Kontrol | Gerçek davranış | Gerekli kayıtlı kapsam |
| --- | --- | --- |
| Giriş yüzeyleri | Seçili portlara bağlanır; bilinen ve aynı kaynaktan bulunan giriş yollarına sınırlı HTTP/HTTPS `GET` istekleri gönderir. Form veya kimlik bilgisi göndermez. | En az bir kabul edilmiş özel IPv4 hedefi. |
| SSL/TLS sertifikaları | TLS bağlantısı açıp geçerlilik, ana makine/parmak izi, kendinden imzalı/iç CA, tekrarlı parmak izi ve AD CS web kanıtını okur. | En az bir kabul edilmiş özel IPv4 hedefi. |
| Dosyalarda açık gizli değerler | Onaylı dosyaları geçici olarak okur; desteklenen gizli değer, kimlik bilgisi, sertifika ve anahtar sinyalleri için yalnız metadata ve maskelenmiş bulgu oluşturur. | En az bir çözümlenmiş hazır klasör veya onaylı yol. |

Hızlı seçimler uygun tüm kontrolleri, yalnız dosyaları veya Ağ + SSL/TLS'yi seçer. Ağ ve dosya kontrolleri birlikte seçilebilir. İki kol eşzamanlı çalışır; herhangi birindeki hata bütün çalışmayı başarısız yapar.

### Özel ağ kapsamı

Ağ kapsamı tek RFC1918 IPv4 adresi, CIDR veya açık IPv4 aralığı kabul eder. Genel IP, ana makine adı, IPv6, loopback ve link-local hedef kabul edilmez. Birleşik sınır 512 hedeftir; açık aralık tek `/24` içinde kalmalıdır. Dolu bir kapsamda tek bir reddedilen giriş bulunması bile kaydı engeller.

Hedef önizlemesi kabul edilen adresleri genişletir, reddedilen girişleri gösterir ve kalanları özetlemeden önce en fazla 64 eşleşen hedefi listeler. Bu yerel bir kapsam önizlemesidir; erişilebilirlik testi değildir.

Port planları düşük gürültülü yaygın kümeler sunar: Premium varsayılan, Web login, Windows kimlik ve Dar TLS. Tarama kuralı en fazla 32 benzersiz port kabul eder. Varsayılan küme `443, 8443, 9443, 636, 3269, 5986, 80, 8080` değerleridir.

Ağ kontrolleri gerçek trafik üretir: TCP bağlantısı, TLS el sıkışması ve sınırlı HTTP/HTTPS GET istekleri. Giriş veya AD CS kanıtını sınıflandırmak için HTTP yanıt gövdesinin en fazla 64 KiB bölümü okunabilir; aynı kaynaktaki sınırlı sayıdaki giriş bağlantısı takip edilebilir. Kullanıcı adı, parola, kimlik doğrulama formu, exploit, kaba kuvvet veya parola püskürtme gönderilmez.

TLS kontrolü, geçersiz veya güvenilmeyen sertifikanın metadata bilgisini okuyabilmek için güven zinciri reddine takılmaz. IP adresi biçimindeki hedeflerde SNI gönderilmez. Sertifika bulgusu risk kanıtıdır; güvenilir TLS bağlantısının başarıyla kurulduğunu kanıtlamaz.

### Dosya kapsamı ve hazır klasörler

Hazır kaynak grupları VaultPilot sunucusunda çözümlenir:

- Windows klasörleri: Masaüstü, Belgeler, İndirilenler, OneDrive, Ortak Masaüstü ve Ortak Belgeler.
- Sunucu uygulamaları: IIS yapılandırma/site/log konumları ile Nginx veya Apache yapılandırma yolları.
- DevOps ve yönetim: uygun `.ssh`, `.kube`, `.docker`, `.aws`, Azure ve gcloud profil klasörleri.

Hazır seçimler uygun yerel Windows profillerine genişleyebilir. Gerçekte hangi yolların okunabildiğini VaultPilot sunucu servis hesabının dosya sistemi izinleri belirler. Eksik veya erişilemeyen hazır yol, açık hata vermeden hiç dosya üretmeyebilir.

Ek kapsam; onaylı mutlak sürücü yolu veya normal UNC yolu kabul eder. Kayıtlı tarama en fazla 32 çözülmüş yol tutar. Sürücü kökü, üst dizine çıkma içeren yol, cihaz yolu, çoğu Windows sistem yolu, VaultPilot/eski PassMan veri yolu, sembolik bağlantı, oluşturulmuş dizin/dosya, desteklenmeyen uzantı, erişilemeyen kayıt ve boyut sınırını aşan dosya atlanır veya reddedilir.

Kural en fazla 80 izinli uzantı kabul eder. Varsayılan azami dosya boyutu 5 MB, kesin üst sınır 25 MB'dir. Zaman aşımı 250–15.000 ms, eşzamanlılık 1–16 aralığındadır.

Dosya incelemesi; desteklenen metin, yapılandırma, betik, VPN/RDP, kayıt defteri, Terraform, paket yöneticisi kimlik bilgisi, sertifika/anahtar ve desteklenen Office/Excel OOXML içeriğini sunucu işlemi belleğine geçici olarak okuyabilir. Kalıcı Discovery verisi kaynak gizli değeri değil; dedektör metadatası, maskeli yol, karmalar, gerekçe kodları ve maskelenmiş önizleme içerir. Kaynak dosya değiştirilmez, taşınmaz, karantinaya alınmaz, temizlenmez veya silinmez.

### Açık onay ve tarama kuralı davranışı

Ağ kapsamı **Bu özel hedefleri tarama yetkim var**, dosya kapsamı **Bu dosya yolları salt okunur tarama için onaylı** seçimini ister. Kapsam değiştirildiğinde ilgili onay sıfırlanır. Geçerli özel ağ kapsamı, onaylı dosya kapsamı veya ikisinden biri olmadan tarama kaydedilemez.

**Taramayı kaydet** her seferinde yeni tarama kuralı oluşturur; mevcut ekranda kayıtlı kuralı düzenleme veya silme işlemi yoktur. **Bu tarama aktif** kapalı kaydedilirse kural Devre dışı olur. Tarama düğmesi kapanır; mevcut arayüzde Önizleme etkin görünebilse de sunucu Devre dışı kural için hem Önizleme hem Taramayı reddeder.

## Önizleme, Tarama ve İş Kontrolleri

Önizleme ile Tarama aynı değildir:

- **Önizleme**, hemen tamamlanmış bir `PREVIEW` işi ve denetim olayı kaydeder. TCP, TLS, HTTP veya dosya kontrolü yapmaz ve bulgu oluşturmaz.
- **Tarama**, seçilen kontrolleri gerçekten yürütür. Birkaç dakika sürebilir; istek iş son duruma ulaşınca tamamlanır, bu sırada periyodik sorgular kaydedilmiş ilerlemeyi gösterebilir.

Bir tarama kuralı için aynı anda yalnız bir iş etkin olabilir. İş durumları Sırada, Çalışıyor, İptal bekleniyor, Tamamlandı, İptal edildi ve Başarısız değerleridir. İlerleme; taranan hedef, taranan dosya, işlenen bulgu ve son güncelleme bilgisini gösterir.

**Durdur** iptal isteğini kaydeder. İptal anlık değildir; çalıştırıcı onaylayana kadar kural etkin kalır ve yeni iş başlatılamaz. **Sil**, yalnız son duruma ulaşmış işte onaydan sonra kullanılabilir; çalışma logunu siler, ilgili bulguları korur. **Tekrar**, kayıtlı kuralı ve o anda seçili kontrolleri kullanır; eski işin kontrol seçiminin değişmez kopyasını yeniden oynatmaz.

İşlem logu en yeni altı işi gösterir. Genişletilmiş tarama geçmişi dönen bütün işleri listeler. Sunucu yeniden başlarsa yarım kalan etkin iş daha sonra kesintiye uğramış veya iptal edilmiş olarak kurtarılabilir.

Ekrandaki bulgu sayısı o çalışmada işlenen veya güncellenen sinyalleri gösterir; yalnız yepyeni benzersiz bulgu satırı sayısı olduğu garanti edilmez.

## Bulgular: Maskelenmiş Sinyalleri İnceleme

İlk Bulgular görünümü bilerek **Güçlü sinyal + Açık** filtreleriyle başlar. Varsayılan görünümü geri yüklemek bütün bulguları değil bu filtreleri getirir. Arama ve gelişmiş filtreler; güven, durum, önem, kaynak türü, aday tipi, varlık kimliği, gerekçe kodu, maskeli yol ve karmaları kapsar.

İlk sayfa 200 bulgu yükler. **Daha fazla bulgu yükle** eski sayfaları getirir; API sayfa başına en fazla 500 kayıt kabul eder. Filtreler, toplu seçim, inceleme sayıları ve İçe aktar yalnız tarayıcıya yüklenmiş bulgular üzerinde çalışır. Filtre dışında kalan seçimler temizlenene kadar seçili kalabilir.

Tablo ve detay paneli; önem, güven, aday tipi, varlık kimliği, maskelenmiş önizleme, dedektör, gerekçe kodları, durum, kısaltılmış kanıt karması, isteğe bağlı maskeli yol/yol karması ve güncelleme zamanı gösterir. Maskelenmiş kanıt bile iç sistemi tanımlayabilir; bilinçli biçimde güvenli hale getirilmeden özel kanalda tutun.

### Bulgu yaşam döngüsü

| Geçerli durum | Kullanılabilir kararlar |
| --- | --- |
| Açık | İncelemeye al, Yok say, Bastır |
| İncelemede | Uygun dosya materyalini Kasaya alınabilir yap, Yok say, Bastır, Açığa döndür |
| Kasaya alınabilir | Uygun materyal için İçe aktar ekranını aç veya Açığa döndür |
| Kasaya aktarıldı | Temizliği işaretle |
| Temizliği doğrulandı | Açığa döndür |
| Yok sayıldı | Açığa döndür veya Bastır |
| Bastırıldı | Açığa döndür |

Yok say yalnız o bulguyu kapatır. Bastır; dedektör ve bastırma anahtarı için kalıcı kural oluşturur, gelecekteki benzer sinyaller Bastırıldı durumunda saklanır. Geçerli arayüz bastırma nedeni istemez veya göndermez; kural normalde **Not yok** gösterir. Bastırılmış bulguyu Açığa döndürmek kalıcı bastırma kuralını silmez; bu ekranda bastırma kuralı silme kontrolü yoktur.

Bulgu işlemleri onay penceresi göstermez. Toplu **İncelemeye al**, yalnız görünür ve seçili Açık bulguları etkiler. Geçerli arayüz bulguyu mevcut kasa kaydına bağlamaz.

Tamamlanan dosya taraması, daha önce görülen kanıt başarıyla taranmış yollardan kaybolursa Açık, İncelemede veya Kasaya alınabilir durumundaki eski dosya bulgusunu otomatik olarak Temizliği doğrulandı durumuna alabilir. Yok sayıldı, Bastırıldı ve Kasaya aktarıldı durumları bu geçişle otomatik temizlenmez.

## İçe Aktar: Kısa Ömürlü Materyal Aktarımı

Yalnız dar kapsamlı dosya bulgusu içe aktarılabilir. Bulgu Kasaya alınabilir ve `FILE_EXPOSURE` türünde olmalı; yol karması ve materyal konumu bulunmalı; Parola, API anahtarı, Sertifika veya Kimlik bilgisi adayı olarak sınıflandırılmalıdır. Ağ yüzeyi, TLS bulgusu, not ve genel dosya kanıtı yalnız sinyaldir.

İçe aktarım adayları yüklenmiş bulgulardan oluşur. Beklenen eski aday görünmüyorsa önce Bulgular ekranında daha eski sayfaları yükleyin.

Her içe aktarımda:

1. VaultPilot onaylı kaynağı yeniden okur; yol karması, dedektör, aday tipi, kanıt karması ve materyal parmak izini doğrular.
2. Düz metin değer yalnız kullanıcıya bağlı, beş dakikalık kısa aktarım için döner.
3. Tarayıcı kaydı oluşturup etkin kasa anahtarıyla şifreler.
4. Sunucu belirteci, kanıtı, kasa yazma yetkisini ve aday tipini doğrular; şifreli kaydı saklayıp bulguyu Kasaya aktarıldı durumuna geçirir.

Kaynak materyal değiştiyse, taşındıysa, kaybolduysa veya kanıtla artık eşleşmiyorsa içe aktarım durur ve bulgu yeniden incelenmelidir. Sunucu düz metin kaynak değeri kalıcı olarak saklamaz.

Seçili içe aktarımlar sırayla çalışır; tek atomik işlem değildir. Sonraki kayıt başarısız olursa daha önce başarıyla aktarılanlar kasada kalır. İçe aktarım kaynağı temizlemez; **Temizliği işaretle** yalnız bulgu iş akışı durumunu değiştirir.

## Denetim İzi

Discovery; tarama kuralı kaydı, Önizleme/Tarama başlangıcı, çalışma iptali ve log silme, bulgu inceleme/Yok say/Bastır, içe aktarım hazırlama ve materyal okuma, genel kasa `IMPORT`, içe aktarım tamamlama ve elle temizlik işaretleme olaylarını denetime yazar. İş logunu silmek bulguları silmez. Eski dosya bulgularının otomatik temizliği tamamlanan dosya taramasının parçasıdır; her satır için ayrı elle temizlik denetim olayı olarak anlatılmamalıdır.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Discovery yükleniyor | İskelet tamamlanana kadar bekleyin; durum bilinmeden ikinci tarama kuralı oluşturmayın. |
| Discovery verisi alınamadı | Oturumu, Discovery yeteneğini ve sunucu bağlantısını kontrol edin; güvenli hale getirilmiş hatayı koruyun. |
| Salt okunur rol veya lisans | Yalnız inceleyin. Bütün işlemler Sahip ve yazılabilir Discovery lisansı ister. |
| Kapsam reddedildi | Kapsamı genişletmeyin veya denetimi aşmayın; özel IPv4 kapsamını düzeltin ya da yalnız dosya taraması için ağ alanını boşaltın. |
| Kural Devre dışı | Önizleme düğmesinin görünümüne güvenmeyin; çalışma gerekiyorsa etkin yeni kural oluşturun. |
| Tarama çalışıyor | Kaydedilmiş ilerlemeyi izleyin; aynı kural ikinci işi başlatamaz. |
| İptal bekleniyor | Çalıştırıcı onayını bekleyin; taramanın hemen durduğunu varsaymayın. |
| Tarama başarısız | İş detayını açın, gizli değerleri çıkarılmış hata kanıtını koruyun, onaylı kuralı düzeltip bilinçli yeniden başlatın. |
| Bulgu yok | Önizleme değil gerçek Tarama tamamlandı mı ve seçilen kontrollerin geçerli kapsamı var mı kontrol edin. |
| Filtreye uyan bulgu yok | Filtreleri sıfırlayın; varsayılan görünüm bile Açık olmayan ve Güçlü olmayan bulguları gizler. |
| İçe aktarım kuyruğu boş | Uygun dosya bulgularını inceleyin, gerekiyorsa eski sayfaları yükleyin ve doğrulanan materyali Kasaya alınabilir yapın. |
| İçe aktarım kilitli | Sahip'in Düzenleyici veya Yönetici olduğu yazılabilir etkin kasayı açın. |
| İçe aktarım kanıtı değişti | Durup kaynağı yeniden inceleyin; karma veya parmak izi doğrulamasını atlamayın. |

## İşlemden Önce

- Her özel hedef, UNC paylaşımı, sürücü yolu ve hazır seçimle genişleyen profil alanı için açık yetki alın.
- VaultPilot sunucu hesabının yalnız amaçlanan okuma yetkisine sahip olduğunu doğrulayın; hazır seçimler dosya sistemi yetkisi vermez.
- Soruyu yanıtlayan en küçük hedef, port, yol, uzantı, boyut, zaman aşımı ve eşzamanlılık kapsamını seçin.
- Önizlemeyi yalnız kayıtlı plan sayın; gerçek kanıt gerektiğinde Tarama kullanın.
- HTTP kontrollerinin GET trafiği ürettiğini, dosya kontrollerinin kaynak içeriği geçici olarak okuduğunu unutmayın.
- Yok say, Bastır veya İçe aktar kararından önce durum, güven, dedektör, maskeli yol, gerekçe kodları ve sahipliği inceleyin.
- İçe aktarmadan önce etkin kasa, yazma rolü, kayıt sahibi, hedef kategori ve kaynak düzeltme planını doğrulayın.

## Güvenli Kanıt

- Paylaşılabilir: genel kontrol türü, tarama kuralı/iş durumu, yaklaşık hedef/dosya/bulgu sayıları, önem, güven, aday tipi, dedektör kimliği, geniş zaman aralığı, güvenli hale getirilmiş hata sınıfı ve bilinçli maskelenmiş yol veya ana makine biçimi.
- Gizli kalmalı: gerçek IP/CIDR/port envanteri, ana makine adı, UNC veya yerel yol, kullanıcı adı, tam varlık kimliği, bastırma anahtarı, kesin zaman damgası, ham veya ilişkilendirilebilir önizleme, kaynak dosya, kaynak değer, özel anahtar/sertifika materyali, içe aktarım belirteci, kasa adı, veritabanı/yedek/dışa aktarım ve içe aktarılan kayıt içeriği.
- Kanıt ve yol karmaları raporlar arasında sistemleri ilişkilendirebilir. Özel destekte tam karşılaştırma gerekmiyorsa kısaltılmış veya tamamen maskelenmiş değer paylaşın.
- Kaynak dosyayı eklemeyin ve keşfedilen düz metni destek kaydında yeniden yazmayın. Maskelenmiş bulgu metadatası ve özel destek kanalı kullanın.

## Ne Zaman Durmalı ve Destek İstemelisiniz

Kapsam sahipliği belirsizse, genel veya beklenmeyen hedef görünüyorsa, hazır seçim onay dışı alana çözülüyorsa, dosya erişimi amaçlanandan genişse, çalışma ilerlemeden etkin kalıyorsa, iptal onaylanmıyorsa, bulgular beklenenden fazla bağlam açığa çıkarıyorsa, bastırma açıklanmamış sinyal sınıfını gizliyorsa, materyal içe aktarım sırasında değişiyorsa, sıralı içe aktarım kısmen başarılı oluyorsa veya temizlik/iptal kararı denetim kanıtıyla çelişiyorsa durun. Gerçek kapsam veya gizli materyal eklemeden rol, genel durum, kontrol türü, geniş zaman aralığı, kısaltılmış karmalar, güvenli hata metni ve son güvenli adımla özel destek kaydı açın.

## Operatör Notları

Discovery kanıt toplama ve inceleme aracıdır; ihlal kanıtı veya hiçbir sorun bulunmadığının garantisi değildir. Temiz sonuç yalnız seçilen kontrolleri, kabul edilen kapsamı, okunabilen dosyaları, desteklenen biçimleri, limitleri ve o Taramanın zamanını kapsar. Bulguyu Temizliği doğrulandı durumuna almak kaynağı değiştirmez. Bastırma kalıcıdır; yalnız gelecekteki benzer sinyaller bilinçli olarak gizlenecekse kullanılmalıdır.

## İlgili

- [Discovery rehberi](discovery.md)
- [Discovery bulgu inceleme KB](../../kb/tr/discovery-finding-review.md)
- [Public issue redaction KB](../../kb/tr/public-issue-redaction.md)
- [Denetim Geçmişi ekranı](screen-audit-log.md)
