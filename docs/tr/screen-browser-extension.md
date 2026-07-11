# Taray?c? Eklentisi Ekran?

?st ?ubuktaki `?`, **Entegrasyonlar > Taray?c? eklentisi** sekmesi a??kken bu ba?lama ?zel rehberi a?ar. D?? API veya Active Directory sekmesinde ayn? d??me genel Entegrasyonlar rehberine gider. Bu ekran? Chrome Web Store kanal?n? incelemek, k?sa ?m?rl? e?le?tirme isteklerini onaylamak, kasa yetkisi say?lar?n? g?rmek ve onayl? taray?c? profillerinin eri?imini iptal etmek i?in kullan?n.

## Eri?im, Rol ve Lisans S?n?r?

**Entegrasyonlar** men? yolu yaln?z **Sahip** rol?ne a??kt?r ve lisans?n **Entegrasyon** yetene?ini ister. Eklentiye ?zel k?sayol farkl? ?al???r: Sahip rol?n? ve ayr? **Eklenti** yetene?ini kontrol eder, ancak Entegrasyon yetene?ini yeniden denetlemez. Entegrasyonlar ekran? zaten a??ld?ktan sonra sayfa i?indeki **Taray?c? eklentisi** sekmesine ge?i? de Eklenti yetene?ini yeniden kontrol etmez. Bu nedenle sekmenin g?r?nmesi iki yetene?in de lisansl? oldu?unu kan?tlamaz. Y?netici, Denet?i ve Kullan?c? rolleri mevcut men?den bu y?netim paneline ula?amaz.

Eklenti kayna??ndan ?a?r?lan e?le?tirme ba?lang?? ucu konsol oturumuyla ?al??maz; etkin bir Sahip, Y?netici veya Kullan?c? ad?n? hedefleyebilir. Kimlik do?rulamas? isteyen listeleme, onaylama ve iptal u?lar? Sahip, Y?netici ve Kullan?c? rollerini kabul eder, Denet?i'yi reddeder ve yaln?z oturum kullan?c?s?na ait cihaz kay?tlar?n? i?ler. Desteklenen aray?z ak??? olarak bu panelde Sahip i?lemini esas al?n; ba?ka bir yerde kullan?c? ad? g?rmek o ki?inin e?le?tirme iste?ini y?netme yetkisi vermez.

E?le?tirmeyi ba?latmak veya onaylamak i?in lisans yaz?labilir olmal?d?r. Salt okunur modda cihaz listesi incelenebilir ve g?venlik amac?yla mevcut onayl? cihaz?n eri?imi iptal edilebilir; bekleyen istek onaylanamaz. Onaydan ?nce etkin profilde en az bir kasan?n kilidi a??k olmal?d?r.

## Burada Ne Yap?l?r

- Desteklenen VaultPilot Browser Vault Extension ma?aza kayd?n? Chrome Web Store'da a??n.
- Son eklenti e?itlemesini ve onayl?/bekleyen cihaz ?zetlerini yenileyin.
- Bekleyen cihaz ad? ve kodun son d?rt karakterini, ayr? kanaldan do?rulanm?? kullan?c? iste?iyle e?le?tirin.
- Eklenti a??l?r penceresindeki tam kodu girip bu profilde o anda a??k olan kasalara eri?im verin.
- Etkin cihazlarla iptal edilmi? veya s?resi dolmu? ar?iv kay?tlar?n? ayr? inceleyin.
- Kaybolan, kullan?lmayan, beklenmeyen veya art?k g?venilmeyen onayl? taray?c? profilinin eri?imini iptal edin.

Bu panel eklentiyi uzaktan kurmaz veya kald?rmaz; taray?c? politikas?n? da??tmaz, Web Store g?ncellemesini zorlamaz, ba?ka bir taray?c?y? y?netmez ve bir sayfada otomatik doldurman?n ?al??t???n? kan?tlamaz. Yaln?z sunucu taraf?ndaki e?le?tirme ve kasa yetkilerini y?netir. Otomatik doldurma; kullan?c? i?lemi, etkin site, eklenti oturumu, taray?c? politikas? ve e?le?me kurallar?na ba?l? ayr? bir eklenti davran???d?r.

## Chrome Web Store ve Merkezi Kurulum

**Chrome Web Store'da a?**, `hjkbedlaieikhkoplgpiohlaakgebobi` kimlikli desteklenen ma?aza kayd?n? a?ar. Normal m??teri kurulumu ve g?ncellemeleri bu ma?aza kanal?ndan yap?l?r. Ma?aza kurulumunda ZIP indirme, Geli?tirici Modu veya **Paketlenmemi? ??e y?kle** gerekmez.

Merkezi y?netilen Chrome veya Edge cihazlar?nda ayn? Web Store eklenti kimli?ini kurumun taray?c? politikas?yla da??t?n. Bu i?lem VaultPilot ekran?nda de?il, taray?c? y?netim platformunda yap?l?r. Chrome otomatik g?ncelleme kontrollerini kendi y?r?t?r; eklentinin Hakk?nda g?r?n?m? Web Store kontrol? isteyebilir, ancak Chromium iste?i s?n?rlayabilir ve g?ncellemeyi yaln?z taray?c? haz?r olarak bildirdi?inde uygular.

Yay?n ZIP'i ar?iv, yerel geli?tirme, laboratuvar do?rulamas? veya acil geri d?n?? i?indir; ola?an merkezi kurulum yolu de?ildir. Paketlenmemi? veya geri d?n?? ama?l? bir derleme i?in ayr?ca izin verilen eklenti kayna?? gerekebilir. Ma?aza kimli?ini veya ?retim izin listesini geli?ig?zel de?i?tirmeyin.

## E?le?tirme Ya?am D?ng?s?

### 1. Eklenti a??l?r penceresinden ba?latma

A??l?r pencerede VaultPilot sunucu adresini, VaultPilot kullan?c? ad?n?, ay?rt edilebilir bir cihaz ad?n? ve eklenti PIN'ini girip **E?le?tirmeyi ba?lat** se?ene?ini kullan?n. PIN, eklenti ?zel anahtar?yla e?le?tirme belirtecini bu taray?c? profilinde korur; VaultPilot ana parolas? de?ildir.

Eklenti; cihaz ad?n?, iste?e ba?l? kullan?c? ad?n? ve a??k anahtar?n? e?le?tirme ba?lang?? ucuna g?nderir. Sunucu etkin ve Denet?i olmayan profili se?er; e?le?tirme kimli?i ve belirteci ?retir, on dakika sonra s?resi dolan `XXXX-XXXX` kodunu d?nd?r?r. ?stek ayr?ca kabul edilen eklenti kayna??na ba?lan?r. Tam kod yaln?z eklenti a??l?r penceresinde g?sterilir; sunucudaki cihaz sat?r?ndan geri okunmaz.

### 2. Bekleyen durumu inceleme ve onay? kontrol etme

Eklenti e?le?tirme kimli?ini, belirtecini ve kodu yerel olarak tutar; **Onay? kontrol et** i?lemini sunar. Durum sorgusu e?le?tirme kimli?i ve belirteciyle do?rulan?r, kabul edilen eklenti kayna??ndan gelmelidir. Bekleyen istek onaylanmadan kullan?lamaz. On dakikal?k s?re biterse sorgu s?re dolumu hatas? verir ve sunucu listesi kayd? Ar?iv alt?nda s?n?fland?r?r.

Bu ekrandaki **Aktif cihazlar**, getirilen kay?t aral???ndaki bekleyen ve onayl? sat?rlar? i?erir. Bekleyen sat?rda kullan?c?n?n girdi?i cihaz ad?, e?le?tirme kodunun yaln?z son d?rt karakteri ve mevcut kasa yetkisi say?s? g?r?n?r. Tam kod, kullan?c? ad?, taray?c? profili, istek kayna??, eklenti kimli?i, a??k anahtar, e?le?tirme belirteci veya cihaz kimli?i g?sterilmez. Cihaz ad? kullan?c? taraf?ndan yaz?lan bir etikettir; do?rulanm?? cihaz kimli?i de?ildir.

### 3. Onaylama ve kasa yetkisi verme

Onaydan ?nce iste?in sahibini ve taray?c? profilini kurum i?i kanaldan do?rulay?n. A??l?r penceredeki tam kodu beklenen istekle ve sat?rdaki son d?rt karakter ipucuyla kar??la?t?r?n; ard?ndan kodun tamam?n? `XXXX-XXXX` bi?iminde girin.

Onay i?in yaz?labilir lisans ve en az bir a??k kasa gerekir. VaultPilot, **onaylayan profilde o anda a??k olan b?t?n kasalar?n** anahtarlar?n? bekleyen cihaz?n a??k anahtar? i?in sarar; bu ekranda kasa ba??na yetki se?ici yoktur. Sat?rdaki kasa yetkisi say?s? ka? sar?lm?? kasa anahtar? verildi?ini g?sterir. Onay `EXTENSION_PAIR` olay? yazar, cihaz listesini ve Denetim Ge?mi?ini yeniler, yaz?lan kod alan?n? temizler.

Onaydan sonra eklenti a??l?r penceresinde **Onay? kontrol et** se?ene?ini kullan?n. Eklenti yaln?z onayl? yetkileri i?in ?ifreli kasa snapshot'? isteyebilir ve bunu korunan ?al??ma alan?nda ??zebilir. E?le?tirme, ana parolay? veya d?z metin kasa kay?tlar?n? cihaz listesinde g?stermez.

## Cihaz Listesi, E?itleme ve ?ptal

Cihaz sorgusu oturum kullan?c?s?na ait yaln?z olu?turulma zaman?na g?re en yeni 50 kayd? getirir. ?zetteki e?itleme zaman? ve onayl?/bekleyen say?lar? ile **Aktif cihazlar**/**Ar?iv** ayr?m? yaln?z bu kay?t aral???ndan hesaplan?r; tam cihaz ge?mi?i de?ildir. Daha eski e?le?tirme, iptal ve e?itleme hareketlerini Denetim Ge?mi?inde ara?t?r?n. **Yenile** ve ?zet kontrolleri listeyi tekrar sorgular; ekran a??kken liste yakla??k be? saniyede bir de yenilenir.

Konsol **?ptal et** d??mesini yaln?z `APPROVED` durumundaki sat?rda g?sterir. D??me ikinci bir onay penceresi g?stermeden hemen ?al???r; cihaz? iptal durumuna ge?irir, saklanan sar?lm?? kasa yetkilerini kald?r?r, `EXTENSION_REVOKE` olay? yazar ve kayd? Ar?ive ta??r. Yaln?z onayl? sat?rda g?r?nme kural? konsol d??mesine aittir. Alttaki iptal ucunda yaz?labilir lisans veya cihaz durumu kontrol? yoktur; kimli?i do?rulanm?? Sahip, Y?netici veya Kullan?c? kendi kayd?yla e?le?en sat?r? mevcut durumundan ba??ms?z olarak iptal edebilir. Desteklenen operat?r ak???nda ekrandaki i?lemi kullan?n. ?ptalden sonra eklenti art?k onayl? ?ifreli kasa snapshot'? alamaz. Sunucu eri?imini iptal etmek eklentiyi kald?rmaz veya taray?c? profilini silmez; gerekirse yerel e?le?tirmeyi veya eklentiyi o taray?c?da ayr?ca kald?r?n.

Her ba?ar?l? ?ifreli kasa snapshot'? al?m? son g?r?lme zaman?n? g?nceller ve `EXTENSION_SYNC` olay? yazar. G?rme, kopyalama ve doldurma i?lemlerinin ayr? eklenti denetim yolu vard?r; ancak bu y?netim ekran? sayfa d?zeyinde otomatik doldurma kan?t? g?stermez. Olaylar? Denetim Ge?mi?inde inceleyin ve cihaz ili?kisini gizli tutun.

## Ar?iv, S?re Dolumu ve Hatalar

**Ar?iv**, en yeni 50 cihazl?k kay?t aral???ndaki iptal edilmi? ve s?resi dolmu? sat?rlar? i?erir. Tam ge?mi? de?ildir; daha eski olaylar i?in Denetim Ge?mi?ini kullan?n. S?resi dolan istek onaylanamaz; eklenti a??l?r penceresinden yeni istek ba?lat?n. Ar?iv sat?rlar?nda konsol onaylama veya iptal i?lemi yoktur. Bu kay?tlar ?zel incelemede i?e yarar, ancak eklentinin taray?c?dan yerel olarak kald?r?ld???n? kan?tlamaz.

Onay hatas? kodun ve s?renin kontrol edilmesini isteyen genel bir mesaj g?sterir. Ayr?ca lisans?n yaz?labilirli?ini, etkin profili, en az bir a??k kasay?, istek sahipli?ini ve sat?r?n h?l? bekliyor olmas?n? denetleyin. ?ptal hatas? da genel bir eri?im iptali mesaj?d?r; eski durumla i?lem yapmamak i?in yeniden denemeden ?nce listeyi yenileyin.

Cihaz listesi y?klenirken iki iskelet sat?r? g?r?n?r. Liste sorgusu i?in ayr? bir hata kart? yoktur. Saklanm?? veri bulunmad???nda ba?ar?s?z sorgu ilgili bo? durum gibi g?r?nebilir. Oturumu, sunucu ba?lant?s?n? ve **Yenile** sonucunu kontrol etmeden **Hen?z e?le?tirme iste?i yok** mesaj?n? veya bo? Ar?ivi kesin kan?t saymay?n.

## ?nerilen ?? Ak??lar?

### Yeni merkezi y?netilen taray?c? profilini onaylama

1. Taray?c?n?n desteklenen Web Store eklenti kimli?ini onayl? kullan?c? veya politika kanal?ndan ald???n? do?rulay?n.
2. A??l?r pencerede do?ru HTTPS sunucu adresini, kullan?c? ad?n?, cihaz ad?n? ve yeni eklenti PIN'ini girip e?le?tirmeyi ba?lat?n.
3. Kodu okumadan veya girmeden ?nce iste?i yapan ki?iyi ve taray?c? profilini kurum i?i kanaldan do?rulay?n.
4. Bu ekranda cihaz ad?n? ve son d?rt karakter ipucunu e?le?tirin; iste?in h?l? bekledi?ini kontrol edin.
5. Yaln?z yetki verilecek kasalar? a??k b?rak?n; a??k olan her kasan?n kapsama girece?ini unutmay?n.
6. Tam `XXXX-XXXX` kodunu girip **Onayla** se?ene?ini bir kez kullan?n.
7. A??l?r pencerede onay? kontrol edip e?itleyin; `EXTENSION_PAIR` ve beklenen ilk `EXTENSION_SYNC` olay?n? ?zel kan?tta do?rulay?n.

### Kaybolan veya g?venilmeyen taray?c? profilini iptal etme

1. Aktif cihazlar? yenileyin; onayl? sat?r? yaln?z cihaz ad?na g?re de?il, ?zel envanter kan?t?yla belirleyin.
2. Kod, kimlik veya kasa ayr?nt?s? kopyalamadan genel iptal nedenini ve beklenen etkiyi kaydedin.
3. ?kinci onay olmad???n? bilerek **?ptal et** se?ene?ini bir kez kullan?n.
4. Sat?r?n Ar?ive ta??nd???n?, kasa yetkisi say?s?n?n temizlendi?ini ve `EXTENSION_REVOKE` olay?n? do?rulay?n.
5. Taray?c?ya eri?ilebiliyorsa yerel e?le?tirmeyi kald?rma veya eklentiyi kald?rma i?lemini taray?c? y?netim kanal?nda ayr?ca y?r?t?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Cihazlar y?kleniyor | ?ki iskelet sat?r?n? bekleyin; gerekirse sunucu oturumunu kontrol edip Yenile kullan?n. |
| Hen?z e?le?tirme iste?i yok | Desteklenen eklenti a??l?r penceresinden ba?lay?n; konsolda yapay istek olu?turmay?n. |
| Onay bekliyor | Onaydan ?nce iste?i yapan ki?iyi, taray?c? profilini, cihaz ad?n? ve kodu ayr? kanallardan do?rulay?n. |
| E?le?tirme kodu ge?ersiz | A??l?r penceredeki tam `XXXX-XXXX` kodunu yeniden girin; son d?rt karakterden kod tahmin etmeyin. |
| E?le?tirme s?resi doldu | Kayd? Ar?ivde bulun ve a??l?r pencereden yeni on dakikal?k istek ba?lat?n. |
| A??k kasa yok | Onaydan ?nce ama?lanan kasalar? a??n; b?t?n a??k kasalara yetki verilece?ini unutmay?n. |
| Salt okunur lisans | E?le?tirme ba?latmay?n veya onaylamay?n; mevcut onayl? cihaz g?venlik amac?yla iptal edilebilir. |
| E?le?ti | Kasa yetkisi say?s?n?, beklenen e?itlemeyi ve ?zel denetim kan?t?n? kontrol edin. |
| ?ptal edildi | Sunucu yetkilerini kald?r?lm?? say?n; yerel eklenti temizli?ini ayr?ca y?r?t?n. |
| Ar?iv bo? | Ba?lant?y? do?rulay?p yenileyin; eski iptal veya s?re dolumu ge?mi?i olmad??? sonucuna varmadan ?nce en yeni 50 kay?t s?n?r?n? ve Denetim Ge?mi?ini kontrol edin. |
| Onay ba?ar?s?z | Sahiplik, bekleyen durum, tam kod, s?re, yaz?labilir lisans ve a??k kasalar? kontrol edin. |
| ?ptal ba?ar?s?z | Listeyi yenileyin, ge?erli onayl? sat?r? ve sunucu oturumunu do?rulay?p bir kez daha deneyin. |

## ??lemden ?nce

- Konsol oturumunun Sahip rol?nde oldu?unu, Entegrasyon ve Eklenti yeteneklerinin ama?lanan yolu kapsad???n? do?rulay?n.
- ??lemin Web Store da??t?m?, e?le?tirme onay?, e?itleme incelemesi veya iptal oldu?unu ay?r?n; bu ekran d?rd?n? de uzaktan yapmaz.
- Kullan?c?y? ve taray?c? profilini kurum i?i istek kanal?ndan do?rulay?n; cihaz sat?r? bunlar? kan?tlamaz.
- Onaydan ?nce yetki kapsam?na girmemesi gereken kasalar? kilitleyin.
- Tam kodu, son d?rt karakter ipucunu, cihaz ad?n? ve zaman? birlikte hassas ili?kilendirme verisi say?n.
- **?ptal et** i?leminin ikinci onay? olmad???n?, eklentiyi kald?rmad???n? ve taray?c? profilini temizlemedi?ini unutmay?n.

## G?venli Kan?t

- Payla??labilir: sekme ad?, Chrome Web Store kanal?, bekliyor/e?le?ti/iptal/s?resi doldu gibi genel durum, en yeni 50 kay?t aral???na ait oldu?u a??k?a belirtilmi? toplu onayl? ve bekleyen say?lar?, geni? zaman aral??? ve genel hata s?n?f?.
- Gizli kalmal?: tam veya k?smi e?le?tirme kodu, cihaz ad?, cihaz/e?le?tirme kimli?i ve belirteci, a??k ya da ?zel anahtar materyali, eklenti kayna??, kullan?c?/hesap, tam zaman damgas?, kasa ad?, kasa yetkisi say?s?, ?ifreli kasa snapshot'? ve herhangi bir gizli de?er veya otomatik doldurmada g?r?nen veri.
- E?le?tirme kodu veya belirteci a???a ??kt?ysa genel payla??m? durdurun. ?ste?in s?resinin dolmas?n? bekleyin ya da onayl? cihaz? iptal edin; sonra ?zel kanaldan yeni e?le?tirme ba?lat?n.
- Cihaz ad?, kod ipucu, yetki say?s? ve zaman?n ili?kilendirilebildi?i ekran g?r?nt?s?nde sat?r?n tamam?n? maskeleyin. Tek alan? k?rpmak yeterli de?ildir.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

?ste?in sahibi do?rulanam?yorsa, cihaz ad? veya son d?rt karakter uyu?muyorsa, beklenmeyen say?da kasaya yetki verilecekse, istek s?rekli zaman a??m?na u?ruyorsa, iptal edilen cihaz h?l? ?ifreli kasa snapshot'? alabiliyorsa, bilinen cihazlara ra?men liste bo? g?r?n?yorsa ya da denetim olaylar? i?lemle e?le?miyorsa durun. E?le?tirme materyali veya kasa verisi eklemeden genel durum, geni? zaman aral???, gizli de?erleri ??kar?lm?? hata metni ve son g?venli ad?mla ?zel destek kayd? a??n.

## Operat?r Notlar?

E?le?tirme, onayl? cihaz ve sar?lm?? anahtar g?ven karar?d?r; uzaktan taray?c? y?netimi de?ildir. Chrome Web Store da??t?m?, kurum politikas?, sunucu yetkileri, yerel eklenti durumu ve sayfa d?zeyindeki otomatik doldurma ayr? s?n?rlard?r. Yaln?z onay verildi diye eklentinin kuruldu?unu, g?ncellemenin uyguland???n?, yerel verinin silindi?ini veya otomatik doldurman?n garanti edildi?ini s?ylemeyin.

## ?lgili

- [Taray?c? eklentisi](browser-extension.md)
- [Entegrasyonlar ekran?](screen-integrations.md)
- [Chrome Web Store ma?aza kayd? ve gizlilik](chrome-web-store-listing.md)
- [Eklenti e?le?tirme KB](../../kb/tr/extension-pairing.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
