# Güvenlik Ekranı

Üst çubuktaki `?` simgesi bu yardımı **Güvenlik** ekranı açıkken getirir. Bu ekran, VaultPilot'ın güvenlik sinyallerini tek bir puana indirgemek yerine hangi kaydın, davranışın veya erişim olayının inceleme istediğini gösterir. Bütün sistem rolleri ekranı açabilir; sorgu içeriği, ayrıntıya geçiş ve eylemler role göre daralır.

Dashboard kartları kasa, denetim, lisans, güncelleme, entegrasyon ve işlem sorgularından üretilir. Her görsel etkileşimli değildir: düğme biçimindeki satır ve metrikler hedef ekrana gider; grafik çubukları ve **Risk dağılımı** yalnız okunur. Ekranın tek **Dashboard araçları** menüsü dokümanı açar, veriyi yeniler ve düzenleme modunu yönetir. Widget başına menü yoktur; gizleme ve sıralama yalnız düzenleme modunda görünür.

## Bu Ekranı Nasıl Okumalısınız

- **Güvenlik kapsamı:** Komuta Merkezi skorunun on faktörünü gösterir: 2FA, lisans, eklenti, güncelleme, parola sızıntısı, AD riski, sertifika sona-erme tarihi meta verisinin eksiksizliği, işlem geçmişi, dizin sağlayıcı eşitleme hatası ve kasa içeriği. Sertifika satırı gerçek geçerlilik testi, dizin satırı genel bağlantı testi değildir. Her satır kazandığı/toplam ağırlığı gösterir ve kaynak ekranına gider.
- **Sızıntı kontrolü:** Parolaları bilinen sızıntıda görülen, temiz ve henüz kontrol edilmemiş olarak ayırır.
- **Risk dağılımı:** Üç farklı hesabı yan yana koyar: **Sağlıklı sinyal**, sağlıklı skor faktörlerini; **İzlenecek konu** ve **Kritik işlem** ise ton normalizasyonundan sonraki önerileri sayar. Bunlar tek bir olay/sinyal nüfusu değildir; segmentlere basılmaz.
- **Davranış analizi:** Çubuk grafik erişim, oturum ve yönetim olaylarını karşılaştırır. Yanındaki en fazla beş **Riskli erişimler** satırı tıklanarak ilgili Denetim Kaydı olayına gidilir.
- **Denetim özeti:** En son altı olayı aktör, hedef, risk ve zamanla gösterir. Yalnız **Olay** sütunundaki düğme ilgili denetim olayını açar.
- **Erişim trendi:** Son yedi gündeki kilit açma, görüntüleme, kopyalama, doldurma ve entegrasyon eşitleme olaylarını sayan salt okunur grafiktir; gün çubukları zaman filtresi açmaz.

## Yetki ve Veri Koşulları

Sahip, Yönetici, Denetçi ve Kullanıcı ekranı açabilir; ancak bazı sistem sorguları ve ayrıntı hedefleri yetkisiz rolde boş, kısıtlı veya pasif kalır. Denetçi kasa kayıtlarını açamaz. Gizli kaydı göstermek veya kopyalamak için Denetçi dışındaki uygun rol ve okunabilir kasa erişimi; kasa kaydı yazmak için ayrıca aktif kasada **Editor** ya da **Manager** üyeliği ve yazılabilir lisans gerekir. Sistem hedefleri kendi rol kapılarını uygular.

## Uygulanabilir İnceleme Akışları

### Sızıntıda görülen parolaları ele alma

1. **Sızıntı kontrolü** içindeki sızıntı sayısını, halka grafiğini veya ilgili durum satırını seçin.
2. Açılan Parolalar ekranında hazır sızıntı filtresini ve kayıt sahibini doğrulayın.
3. Parolayı önce ait olduğu sistemde değiştirin, ardından VaultPilot kaydını güncelleyin ve kontrolü yeniden çalıştırın.

Beklenen sonuç, eski değerin geçersiz kalması ve yeni kontrolün temiz sonuç vermesidir. Hedef sistemde değişiklik yapılamıyor veya kayıt sahibi belli değilse kasa değerini tek başına değiştirip işi kapatmayın.

### Beklenmeyen erişim artışını inceleme

Erişim trendindeki yükselişin hangi güne denk geldiğini ve toplamı belirleyin. Grafik olay türünü ayırmaz ve çubuklar tıklanmaz. **Denetim özeti** yalnız son altı olayı gösterdiğinden ayrıntılı zaman ve eylem filtresi için sol gezintiyle Denetim Kaydı’na gidin; belirli bir olay için **Riskli erişimler** satırını veya **Olay** düğmesini kullanın. Beklenen sonuç artışın onaylı çalışmayla eşleşmesidir; eşleşmiyorsa oturum ve hesap güvenliğini özel olay sürecinde inceleyin.

### Kritik risk ile denetim olayını eşleştirme

**Risk dağılımı** yalnız özet olduğu için kritik segmentten ayrıntı açılmaz. Kritik sayıyı not edin; **Davranış analizi > Riskli erişimler** satırlarından veya **Denetim özeti** olay düğmesinden kaynağa gidin. Kartların aynı olayı anlattığını varsaymayın; redakte zaman, işlem türü ve hedef sınıfını karşılaştırın. Çelişki varsa yeni değişiklik yapmadan veriyi bir kez yenileyin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Yükleniyor | Widget'lar tamamlanana kadar puan, oran veya trend yorumlamayın. |
| Sağlıklı | Kapsam oranını ve kontrol bekleyen kayıtları doğrulayıp rutin incelemeyi kaydedin; ekranda tek bir küresel “son yenileme” zamanı yoktur. |
| İzlenecek | Kartı açın, hedef kaydı veya olayı doğrulayın ve sorumlu takip işini belirleyin. |
| Kritik | Önce etkilenebilecek erişimi sınırlandırın; ardından kayıt ve denetim ayrıntısını private süreçte inceleyin. |
| Boş | Gerçekten olay olmadığını söylemeden önce kasa, tarih aralığı ve widget görünürlüğünü kontrol edin. |
| Yenileme sonrası değişmiyor | Küresel zaman damgası aramayın; kaynak widget’ın sorgusunu ve hedef ekran verisini kontrol edin. |
| Yetki kısıtlı | Drill-down açılamıyorsa rolü ve kasa üyeliğini doğrulayın; daha geniş yetkiyi doğrudan kullanıcıya vermeyin. |
| Hata | Hata metnini ve zamanı koruyun; kısmi widget verisini tam tablo gibi raporlamayın. |

## İşlemden Önce

- Widget'ın hangi zaman aralığını ve veri kaynağını özetlediğini kontrol edin.
- Sızıntı sonucu ile risk etiketini, erişim trendi ile denetim olayını birbirinin yerine kullanmayın.
- Dashboard'dan açılan filtreyi temizlemeden önce hangi sinyalin sizi oraya getirdiğini not edin.
- Kayıt değişikliği için aktif kasa rolünü ve lisansın yazılabilir olduğunu doğrulayın.
- Düzenleme modunda widget gizlemenin veriyi veya riski silmediğini unutmayın; gizli bileşeni yine bu modda geri yükleyin.

## Güvenli Kanıt

- **Paylaşılabilir:** genel risk seviyesi, sinyal kategorisi, redakte olay türü, zaman aralığı, kontrolün son çalışma zamanı ve izlenen çözüm adımları.
- **Gizli kalmalı:** kullanıcı ve kasa adları, gerçek kayıt başlıkları, URL'ler, dahili host/etki alanı bilgileri, tam erişim zaman çizelgesi ve gizli değer görünen her ekran görüntüsü.
- Sızıntı kontrolünde bulunan değer, parola örneği olarak bile paylaşılmaz. Public alana düşen gerçek bir parola önce ait olduğu sistemde değiştirilmelidir.

## Ne Zaman Durmalı veya Yükseltmeli

Kritik sinyal yenilemeden sonra kaybolmuyorsa, erişim trendi ile denetim kayıtları uyuşmuyorsa, birçok kullanıcı veya kasa etkileniyorsa ya da dashboard verisi sürekli bayat kalıyorsa güvenlik sorumlusuna ve gerekirse private support'a yükseltin. Sürüm, saat dilimiyle zaman, kart adı, redakte hata ve denediğiniz adımlar yeterlidir.

## Operatör Notları

Bu dashboard bir inceleme yüzeyidir; olayın kaynağı ilgili kayıt veya Denetim Kaydı'ndadır. Sağlıklı renk tek başına tüm parolaların kontrol edildiğini göstermez. Özellikle “kontrol edilmemiş” kayıt sayısını sıfır görmeden sızıntı kapsamını tamamlanmış saymayın.

## İlgili

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Güvenlik Komuta Merkezi ekranı](screen-security-command-center.md)
- [Giriş güvenliği ekranı](screen-sign-in-security.md)
