# G?ncellemeler Ekran?

?st ?ubuktaki `?`, G?ncellemeler ekran?na ait bu rehberi a?ar. Bu ekran VaultPilot sunucu MSI paketinin yerel veya imzal? uzak kan?t?n? denetler, uygun pakette kurulum i?i ba?lat?r ve Windows Installer ile servis yeniden ba?latma ilerlemesini izler. Bir yay?n olu?turma, etiketleme, dosya y?kleme veya yay?mlama arac? de?ildir.

## Eri?im, Rol ve Lisans S?n?r?

**Otomatik g?ncelleme** ?zelli?i, G?ncellemeler g?r?n?m? i?in istemci aray?z?ndeki gezinme kap?s?d?r. ?zellik a??ksa Sahip, Y?netici ve Denet?i ekran? ve mevcut sunucu durumunu g?rebilir; Kullan?c? sistem g?r?n?m?ne eri?emez. Salt okunur lisans ?zellik g?r?n?m?n? a?mad??? i?in bu modda normal gezinme de engellenir. Mevcut durum, i?, kontrol ve ba?latma API u?lar? `auto-update` ?zelli?ini ayr?ca sunucu taraf?nda denetlemez; bu uygulama ayr?nt?s? eri?im kap?s?n? a?ma yetkisi vermez.

**Canl? denetle** uzak GitHub manifestini okumak i?in Sahip veya Y?netici rol? ister ve on dakikada en fazla on istek kabul eder. Kontrol API ucu salt okunur lisans? ayr?ca reddetmez. Yaln?z durum ba?ar?yla d?nd?kten sonra `UPDATE_CHECK` denetim olay? yaz?l?r; manifest indirme veya ayr??t?rma hatas? sonu? ?retmez ve bu denetim olay?n? olu?turmaz. Normal ?zellik kap?s?n? do?rudan istekle a?maya ?al??may?n.

Sunucu MSI kurulumunda sunucu taraf?ndaki kesin yetki **Sahip** rol?d?r. Aray?zde bir d??me g?r?nse bile Y?netici sunucu kurulumunu ba?latmaya yetkili say?lmaz. Lisans salt okunursa Sahip i?in de kurulum ba?lang?c? reddedilir. Denet?i yaln?z g?r?nt?ler; paket kontrol? veya kurulum ba?latamaz.

## Burada Ne Yap?l?r

- Yerel sunucu s?r?m?n?, hedef s?r?m?, kart?n g?sterdi?i paket/URL ad?n?, boyutu, SHA-256 ?zetini ve do?rulama ad?mlar?n? inceleyin.
- **Do?rulama ad?mlar?** ile paketin neden **G?ncel**, **Haz?r** veya **??lem gerekli** oldu?unu okuyun.
- **Canl? denetle** ile yap?land?r?lm?? uzak g?ncelleme manifestini yeniden al?n ve imza/paket kan?t?n? do?rulay?n.
- Kan?t uygunsa Sahip rol?yle **Sunucu MSI kur** se?ene?ini kullan?n.
- Kurulum s?ras?nda y?zde, son kay?ttan bu yana ge?en s?re, hedef s?r?m, ad?mlar ve **Geli?mi? teknik log** ?zetini izleyin.
- Kurulum tamamlan?nca ?al??an s?r?m?n hedef s?r?mle e?le?mesini ve konsolun yeniden ba?lanmas?n? do?rulay?n.

Bu ekranda g?ncelleme i?ini iptal etme d??mesi veya genel **Yeniden dene** i?lemi yoktur. Engellenmi? i? korunur. K?k nedeni d?zeltip kan?t? yeniden do?rulad?ktan sonra kurulum d??mesini tekrar kullanmak, eski i?i devam ettirmek yerine yeni bir i? ba?lat?r.

## Bile?en ve S?r?m Y?zeyleri

Ekrandaki tek kurulum kart? **VaultPilot server** MSI hatt?d?r. Kart; **Artefakt**, **G?ncel s?r?m**, **Paket boyutu** ve varsa SHA-256 g?sterir. **Artefakt** metni bilinen `fileName` alan?ndan de?il `packageUrl` adresinin son b?l?m?nden t?retilir; URL yoksa sunucu dosya ad?n? biliyor olsa bile **Paket yolu bekleniyor** g?r?n?r. Normal sunucu durumunda ayr? bir manifest adresi sat?r? yoktur. Paket URL'si a??lm??sa **MSI indir** ba?lant?s? g?r?n?r.

Taray?c? eklentisi m??teri kurulum ve g?ncellemelerini Chrome Web Store ?zerinden al?r; bu ekran ayr? bir eklenti kurulum i?i olu?turmaz. Offline Share Decrypter, DC Agent ve ba?ka bile?enler g?m?l? **S?r?m notlar?** i?inde an?labilir, ancak burada ayr? kurulum kart? veya i? hatt? de?ildir.

**S?r?m notlar?** bu konsol paketine g?m?l? zaman ?izelgesidir; s?r?m, bile?en ve not say?lar?n? g?sterir. ?st ?ubuktaki en son GitHub s?r?m ?zeti ayr?, bilgilendirici bir sorgudur. GitHub yan?t? yokken ?st ?ubuktaki s?r?m ak??? yerel uygulama s?r?m?n? kullan?p **yay?nland?** diyebilir; bu yedek metin d?? yay?n kan?t? de?ildir. G?m?l? not, ?st ?ubuk ak???, en son s?r?m ?zeti veya **Canl? denetle** sonucu tek ba??na bir yay?n?n olu?turuldu?unu, yay?mland???n? ya da b?t?n dosyalar?n?n haz?r oldu?unu kan?tlamaz.

## Yerel Durum ve Canl? Denetim

Ekran ilk olarak sunucudaki yerel durumu okur:

- S?r?ml?, uygun bir MSI yoksa ?al??an s?r?m? **G?ncel** g?sterir ve kurulum ba?latmaz.
- Daha yeni, s?r?m? belirli yerel MSI bulundu?unda paket boyutu ve SHA-256 de?eri hesaplan?r; s?r?m amac? uygunsa paket **Haz?r** olabilir. Bu yaln?z yerel ?n denetimdir.
- Daha eski paket, s?r?m? belirlenemeyen paket veya ayn? s?r?m onar?m paketi otomatik kurulum i?in **??lem gerekli** durumuna al?n?r. Ayn? s?r?m onar?m? manuel MSI Repair ak???na aittir.

**Canl? denetle**, yap?land?r?lm?? HTTPS GitHub manifestini sunucudan okur. Ba?ar?l? denetim, imzal? manifestin do?ruland???n? ve sunucu MSI varl???n?n/uygunlu?unun de?erlendirildi?ini g?sterir. ?mza anahtar? eksik veya do?rulama ba?ar?s?zsa uzak paket adresleri a??lmaz ve indirme ad?m? engellenir. Yerel paket bulundu?una dair bilgi paneli g?r?nebilir; ancak uzak durum `BLOCKED` iken ekran ayr? bir yerel paket kart? veya indirme ba?lant?s? olu?turmaz.

Uzak ba?lant? veya en son s?r?m sorgusu ba?ar?s?z oldu?unda ekran yay?n olu?turmaz, manifesti de?i?tirmez ve yerel paketi otomatik olarak uzak paket saymaz. Yerel paket kendi s?r?m/SHA ?n denetimi ve kurulum i?i i?indeki Authenticode kontrol?yle ayr? de?erlendirilir.

## Paket ve ?mza Do?rulamas?

Uzak otomatik kurulumda s?ral? g?venlik s?n?r? ??yledir:

1. Manifest, yap?land?r?lm?? veya paketle gelen yay?n a??k anahtar?yla Ed25519 imzas? ?zerinden do?rulan?r.
2. Sunucu varl???, manifestteki izinli HTTPS adresi, dosya ad?, s?r?m ve beklenen boyutla e?le?tirilir.
3. ?ndirme sunucuda s?n?rl? boyutla yap?l?r ve hesaplanan SHA-256, manifestteki tam de?erle kar??la?t?r?l?r.
4. MSI Authenticode bilgisi Windows ?zerinde okunur. Manifest imzalayan sertifikan?n SHA-1 parmak izini sabitlemi?se MSI imzac?s? bununla e?le?melidir; sabitlenmemi? uzak pakette Windows imza durumu ge?erli olmal?d?r.
5. Bu denetimler ge?meden sessiz Windows Installer ad?m? ba?lat?lmaz.

Yerel haz?rlanm?? MSI'?n kart durumu s?r?m amac?n?, dosya varl???n?/boyutunu ve hesaplanan SHA-256 de?erini ?nceden denetler. Bu yerel `READY` de?erlendirmesi manifest Ed25519 imzas? do?rulamaz ve MSI Authenticode imzas?n? hen?z kontrol etmez; Authenticode, kurulum i?i ba?lad?ktan sonra do?rulan?r. ?retim ortam?nda imzas?z kurulum i?in belge veya ekran ?zerinden bir atlama yolu yoktur. Yerel **Haz?r**, yaln?z bu ?n ko?ullar?n ge?ti?ini g?sterir; kurulum veya imza do?rulamas? tamamland? anlam?na gelmez.

Kart SHA-256 de?erinin yaln?z ba?lang?? b?l?m?n? g?r?n?r metinde g?sterir; tam de?er ??e ayr?nt?s?nda bulunabilir. G?r?nen k?saltmay? tam e?le?me kan?t? saymay?n.

## Paket ve ?? Durumlar?

### Paket durumu

| Durum | Anlam? |
| --- | --- |
| **G?ncel** (`CURRENT`) | ?al??an s?r?m i?in kurulabilir yeni yerel/uzak MSI yoktur. |
| **Haz?r** (`READY`) | Uzak pakette imzal? manifest kan?t?, yerel pakette ise s?r?m ve SHA-256 ?n denetimi uygundur. Yerel Authenticode denetimi i? s?ras?nda yap?l?r. |
| **??lem gerekli** (`ACTION_REQUIRED`) | ?mza anahtar?, manifest, varl?k, s?r?m amac? veya ba?ka paket kan?t? eksik/uygunsuzdur. Engelli ad?m? okuyun. |

### G?ncelleme i?i durumu

| Durum | Anlam? |
| --- | --- |
| `QUEUED` | ?ema ve eski/kay?tl? i? uyumlulu?u i?in tan?n?r; g?ncel ba?latma ak??? bu durumu ?retmez. G?r?l?rse aktif kabul edilir. |
| `RUNNING` | ?ndirme, do?rulama, MSI veya yeniden ba?latma a?amas? ilerliyor. |
| `BLOCKED` | Bir g?venlik, paket, Windows Installer, UAC veya yeniden ba?lanma ad?m? i?i durdurdu. Bu ak??ta ayr? `FAILED` i? durumu yoktur. |
| `READY` | ?ema uyumlulu?u i?in tan?n?r; g?ncel ba?latma ak??? bu i? durumunu ?retmez ve kurulum tamamland? anlam?na gelmez. |
| `COMPLETED` | ?al??an VaultPilot s?r?m? hedef s?r?mle e?le?ecek ?ekilde i? tamamland?. |

G?ncel ba?latma yolu yeni i?i do?rudan `RUNNING`, `BLOCKED` veya `COMPLETED` olarak yazar. ?? ba?lang?c? iste?i kay?t olu?turulmadan hata verirse ekranda **G?ncelleme i?lemi ba?lat?lamad?** g?r?n?r; bu, kal?c? bir `FAILED` i? sat?r? de?ildir. Sunucu en fazla 12 g?ncelleme i?ini listeler; aktif i?ler ?nce, ard?ndan son g?ncellenen tamamlanm?? veya engellenmi? i?ler gelir.

## Ad?mlar ve Teknik Log

Do?rulama ve i? ad?mlar? `DONE`, `RUNNING`, `PENDING` veya `BLOCKED` olabilir. Sunucu MSI ak???nda g?r?lebilecek ad?mlar ?unlar? kapsar:

- kurulu s?r?m? okuma ve hedef s?r?m? kabul etme,
- yerel paketi se?me veya do?rulanm?? MSI'? sunucuya indirme,
- indirilen SHA-256 de?erini do?rulama,
- MSI Authenticode imzas?n? do?rulama ve durumunu kaydetme,
- sessiz Windows Installer ?al??t?rma,
- VaultPilotServer servisini yeniden ba?latma ve hedef s?r?m? bekleme.

Karttaki **Do?rulama ad?mlar?** paket durumuna veya se?ili i?in ad?mlar?na dayan?r. Aktif i? varsa ayr?ca **Geli?mi? teknik log** b?t?n i? ad?mlar?n? durum, etiket ve iste?e ba?l? ayr?nt?yla listeler. Bu b?l?m ham PowerShell, MSI veya Windows Event Log de?ildir. Yerel yollar?n sunucu yan?t?na s?zmas?n? azaltmak i?in baz? y?kleyici ayr?nt?lar? redakte edilir; yine de her sat?r? payla?madan ?nce inceleyin.

## Kurulum, UAC ve Servis Yeniden Ba?latma

Sunucu kurulumu sessiz `msiexec` ak???n? yeniden ba?latma istemlerini bast?rarak ?al??t?r?r, ard?ndan VaultPilotServer servisini ayr? bir yard?mc?yla yeniden ba?lat?r. Kurulum s?ras?nda taray?c? ba?lant?s? kesilebilir. Konsol, sa?l?k ve s?r?m sinyali geri geldi?inde hedef s?r?mle otomatik yeniden y?klenmeye ?al???r.

Y?kleyici yard?mc?s? y?netici yetkisi gerektirirse sunucu Windows UAC y?kseltmesi isteyebilir. Bu istem taray?c?da de?il Windows sunucu oturumunda g?r?l?r. Onay verilmezse veya y?kseltilmi? yard?mc? ba?lat?lamazsa i? yakla??k MSI a?amas?nda **BLOCKED** olur. Kurulumu yetkili bir Windows y?netici oturumu ve onayl? bak?m penceresi olmadan ba?latmay?n.

G?ncellemeler ekran? bak?m penceresi planlamaz, yedek olu?turmaz ve kullan?c? oturumlar?n? koordine etmez. Ba?latmadan ?nce onayl? yede?i, k?sa servis kesintisini, kullan?c? ileti?imini ve geri d?n?? yolunu i?letim prosed?r?n?zde haz?rlay?n.

## Engellenme ve Kurtarma

Kal?c? g?ncelleme i?leri sayfa yenilendi?inde veya servis geri geldi?inde yeniden okunur. Sunucu ?al??an `RUNNING` i?i y?kleyici yard?mc?s? g?nl??? ve ?al??an s?r?mle uzla?t?r?r:

- Hedef s?r?m zaten ?al???yorsa i? `COMPLETED` yap?labilir.
- MSI tamamlanm?? ancak servis hedef s?r?mle d?nmemi?se yeniden ba?latma ad?m? bekler; zaman a??m?nda `BLOCKED` olur.
- Y?kleyici yard?mc?s? ba?lang?? sinyali yazmazsa i? yakla??k `%76` d?zeyinde engellenebilir.
- Yard?mc? ba?lam?? ancak MSI tamamlanma/??k?? kodu gelmemi?se i? yakla??k `%82` d?zeyinde engellenebilir.
- MSI tamamland?ktan sonra hedef s?r?m zaman?nda do?rulanamazsa i? yakla??k `%96` d?zeyinde engellenebilir.

Y?zdenin birka? dakika ayn? kalmas? tek ba??na tak?lma kan?t? de?ildir. Son kay?ttan bu yana ge?en s?re k?sa ve yeni sinyal geliyorsa i?i bekleyin. Sayfa yenilendikten sonra kurtar?lan aktif i? kartta g?r?nebilir, ancak oturum i?i aktif i? sinyali yeniden kurulmad?ysa otomatik sorgulama kendili?inden devam etmeyebilir. Pencereye yeniden odaklan?n veya taray?c? sayfas?n? yenileyerek yeni i? anl?k g?r?nt?s?n? al?n; **Canl? denetle** paket kontrol?d?r, i? yenileme d??mesi de?ildir. Yeni i? ba?latmadan ?nce G?ncellemeler ve ??lemler ekranlar?nda aktif kay?t bulunmad???n? do?rulay?n.

?ptal denetimi yoktur. `BLOCKED` i?i veritaban?ndan d?zenlemeyin, paketi do?rulamas?z de?i?tirmeyin ve imza kontrol?n? atlamay?n. Kan?t? koruyun, k?k nedeni d?zeltin, **Canl? denetle** veya yerel kan?tla durumu yeniden do?rulay?n ve yaln?z sonra yeni bir kurulum i?i ba?lat?n.

## ?nerilen ?? Ak??lar?

### Uzak imzal? MSI kurulumunu do?rulama

1. Bak?m penceresi, yedek, geri d?n?? ve sunucu y?netici eri?imini haz?rlay?n.
2. **Canl? denetle** kullan?n; manifest imzas? ve paket ad?mlar?n?n engellenmedi?ini do?rulay?n.
3. Dosya ad?, hedef s?r?m, boyut, tam SHA-256 ve imzac? kan?t?n? ba??ms?z yay?n kan?t?yla kar??la?t?r?n.
4. Paket **Haz?r** ise Sahip rol?yle **Sunucu MSI kur** se?ene?ini kullan?n.
5. ?ndirme, SHA-256, Authenticode, MSI ve yeniden ba?latma ad?mlar?n? izleyin.
6. Konsol geri geldi?inde ?al??an s?r?m?, servis sa?l???n? ve terminal i? durumunu do?rulay?n.

### Engellenmi? i?i inceleme

1. `BLOCKED` i?te ilk engellenen ad?m? ve son kay?t zaman?n? belirleyin.
2. Manifest/imza/hash engeli ile Windows Installer/UAC/servis engelini birbirinden ay?r?n.
3. Paket veya g?ven ayar?n? de?i?tirmeden ?nce redakte kan?t? koruyun.
4. Gerekirse y?zde 76 bilgi bankas?n? ve Windows Installer/VaultPilot servis kan?t?n? kullan?n.
5. K?k neden d?zelmeden yeni i? ba?latmay?n; d?zeltme sonras? durumu yeniden denetleyin.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | ?ki iskelet sat?r? g?r?n?r; ge?ici bo?lu?u kesin paket durumu saymay?n. |
| G?ncelleme durumu okunamad? | Kasa/oturum, rol, otomatik g?ncelleme lisans? ve sunucu ba?lant?s?n? do?rulay?n. |
| G?ncel | Yeni otomatik MSI i?i yoktur; g?m?l? s?r?m notunu yay?n kan?t? saymay?n. |
| Haz?r | S?r?m, manifest, tam SHA-256, imzac? ve bak?m penceresini do?rulad?ktan sonra Sahip ba?latabilir. |
| ??lem gerekli | ?lk `BLOCKED` do?rulama ad?m?n? giderin; indirme veya kurulumu zorlamay?n. |
| Kontrol ?al???yor | ?kinci canl? denetim ba?latmay?n; sonu? veya uyar?y? bekleyin. |
| Kurulum s?r?yor | Y?zde ile birlikte son kay?ttan bu yana ge?en s?reyi izleyin; servis ba?lant? kesintisine haz?r olun. |
| UAC bekleniyor | Windows sunucu oturumunda onay? de?erlendirin; beklenmeyen istemi kabul etmeyin. |
| Y?zde 76/82 civar?nda sabit | Yeni kay?t geliyorsa bekleyin; zaman a??m? veya `BLOCKED` olu?ursa ilgili y?kleyici kan?t?n? inceleyin. |
| Y?zde 96 civar?nda sabit | MSI sonucu ile ?al??an servis s?r?m?n? kar??la?t?r?n; hedef s?r?m gelmeden tamamland? saymay?n. |
| Blocked | Engellenen ad?m? ve redakte ayr?nt?y? koruyun; otomatik yeniden deneme beklemeyin. |
| Completed | ?al??an s?r?m ve servis sa?l??? hedefle e?le?iyorsa tamamland? kabul edin. |
| Konsol ba?lant?s? kesildi | Beklenen bak?m penceresinde sa?l?k sinyalini bekleyin; ba?lant? gelince pencereye odaklan?n veya sayfay? yenileyin, hemen ikinci kurulum ba?latmay?n. |

## ??lemden ?nce

- Sahip rol?n?, otomatik g?ncelleme lisans ?zelli?ini ve lisans?n yaz?labilir oldu?unu do?rulay?n.
- Onayl? bak?m penceresi, g?ncel yedek, geri d?n?? y?ntemi ve Windows y?netici eri?imini haz?rlay?n.
- Yerel ve uzak kaynaklar? kar??t?rmay?n; karttaki `LOCAL` veya `GITHUB_RELEASE` kayna??n? ve hedef s?r?m? do?rulay?n.
- Uzak pakette manifest imzas?n?, izinli paket adresini, dosya ad?n?/boyutunu, tam SHA-256 de?erini ve Authenticode imzac?s?n? birlikte de?erlendirin; yerel `READY` durumunda Authenticode'un i? s?ras?nda do?rulanaca??n? unutmay?n.
- Aktif `QUEUED` veya `RUNNING` i? olmad???n? G?ncellemeler ve ??lemler ekranlar?nda kontrol edin.
- Canl? denetim, s?r?m notu veya en son s?r?m ?zetinin yay?n olu?turmad???n? ve kurulum ba?ar?s?n? kan?tlamad???n? unutmay?n.

## G?venli Kan?t

- Payla??labilir: genel kaynak t?r?, bile?en, s?r?m/etiket, herkese a??k paket ad? ve boyutu, beklenen/g?zlenen SHA-256 e?le?me durumu, Authenticode durumu veya imzac? ?zeti, ad?m durumu, geni? zaman aral??? ve redakte hata kategorisi.
- Gizli kalmal?: yerel indirme/haz?rlama yolu, sunucu ad? ve kullan?c? ad?, i? kimli?i, ?zel manifest veya destek ba?lant?s?, kopyalanm?? MSI, ham PowerShell/MSI/Windows olay g?nl?kleri, destek paketi, ortam de?erleri, lisans verisi ve imzalama ?zel anahtar?/sertifika dosyas?.
- Herkese a??k bir yay?n dosyas?n?n tam SHA-256 de?eri ve imzac? parmak izi payla??labilir kan?t olabilir; bunun ger?ekten herkese a??k varl??a ait oldu?unu do?rulamadan dahili paket kan?t?n? yay?mlamay?n.
- Ekran g?r?nt?s?nde paket URL'sinden t?retilen artefakt metnini, teknik ad?m ayr?nt?s?n? ve son kay?t zaman?n? ayr? ayr? inceleyip gerekli alanlar? maskeleyin; normal kartta manifest adresi bulundu?unu varsaymay?n.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Manifest imzas? do?rulanm?yorsa, SHA-256 veya boyut uyu?muyorsa, Authenticode imzac?s? beklenen kan?tla e?le?miyorsa, beklenmeyen UAC istemi ??k?yorsa, MSI geri al?n?yorsa, servis hedef s?r?mle d?nm?yorsa veya i? uzla?t?rma sonras? `BLOCKED` kal?yorsa kurulumu durdurun. Paket de?i?tirmeden veya yeni i? ba?latmadan; s?r?m, kaynak s?n?f?, ad?m ad?, geni? zaman aral???, genel hata kodu ve redakte imza/SHA-256 durumuyla ?zel destek kayd? a??n.

## Operat?r Notlar?

G?ncellemeler ekran? t?ketici taraftaki do?rulama ve kurulum y?zeyidir. GitHub s?r?m?, manifesti, MSI'? veya ba?ka bile?en varl???n? olu?turmaz, imzalamaz, y?klemez, etiketlemez ya da yay?mlamaz. G?m?l? s?r?m notlar? da d?? yay?n durumunun canl? kayna?? de?ildir.

## ?lgili

- [G?ncelleme Merkezi](update-center.md)
- [Yay?n dosyas? do?rulama](release-asset-verification.md)
- [??lemler ekran?](screen-executions.md)
- [Sunucu ayarlar? ekran?](screen-server-settings.md)
- [Update y?zde 76 civar?nda tak?l?yor KB](../../kb/tr/update-stuck-76.md)
