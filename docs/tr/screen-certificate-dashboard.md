# Sertifika Paneli Ekran?

?st ?ubuktaki `?` simgesi Sertifika Paneli ekran?na ait bu rehberi a?ar. Panel, etkin kasadaki sertifika kay?tlar?n? ge?erlilik s?resi, durum, sertifika otoritesi, kaynak ve organizasyon k?r?l?mlar?yla ?zetler. Buradan sertifika materyali y?klenmez, sunucunun HTTPS sertifikas? de?i?tirilmez ve a? taramas? ba?lat?lmaz.

## Veri Kayna?? ve Eri?im

Panelin kayna??, oturum a?an kullan?c?n?n okuma yetkisi bulunan etkin kasadaki ?ifreli `CERTIFICATE` kay?tlar?d?r. Kay?tlar etkin kasa anahtar?yla taray?c?da ??z?ld?kten sonra say?lar ve grafikler bu g?r?n?r kay?tlar ?zerinden hesaplan?r. Ba?ka kasalardaki, Sunucu ayarlar?ndaki veya Discovery bulgular?ndaki sertifikalar bu toplama kendili?inden kat?lmaz.

Sahip, Y?netici ve Kullan?c? sistem rolleri, etkin kasada okuma yetkileri varsa bu envanteri g?rebilir. Denet?i rol? kasa s?rlar?n? okuyamad??? i?in Sertifika Panelindeki kay?t verisini kullanamaz. Panelde g?r?len **Sahip** alan? bir sertifika kayd?n?n sorumlu bilgisidir; VaultPilot sistem rol? olan **Sahip** ile kar??t?r?lmamal?d?r.

## Burada Ne Yap?l?r

- S?resi dolmu?, 30 g?nl?k yenileme aral???na girmi?, iptal edilmi? veya ge?erlilik tarihi eksik kay?tlar? ay?r?n.
- Sertifika otoritesi ve kalan g?n ili?kisini radarda inceleyip ilgili kayd?n yaln?z meta verisini a??n.
- Ge?erlilik, durum, kaynak, sertifika otoritesi veya organizasyon sat?r?ndan Sertifikalar ekran?na haz?r filtreyle ge?in.
- Uyar?n?n kasa envanterine mi, VaultPilot sunucusunun taray?c? HTTPS eri?imine mi, yoksa Discovery taramas?na m? ait oldu?unu belirleyin.
- Panel ara?lar?ndan veriyi yenileyin veya bile?en yerle?imini d?zenleyin. Yerle?im de?i?ikli?i yaln?z g?r?n?m? etkiler; sertifika kay?tlar?n? de?i?tirmez.

## Bile?enleri Nas?l Okumal?s?n?z

### Sertifika risk radar?

Radar?n sekt?rleri, etkin kasadaki kay?tlardan ??kar?lan sertifika otoritelerini; merkeze uzakl?k ise 90 g?ne kadar kalan s?reyi g?sterir. Renk bantlar? **0?15 g?n**, **16?30 g?n**, **31?60 g?n**, **60+ g?n** ve **Tarih yok** ayr?m?n? kullan?r. Kritik say?; 15 g?n veya daha az kalan kay?tlar?n yan?nda s?resi dolmu? ve iptal edilmi? kay?tlar? da kapsar.

Bir radar noktas?n? se?mek ayr?nt? penceresini a?ar. Burada kay?t say?s?, en yak?n biti?, durum, otorite ve imzalayan, konu, alan ad?, kay?t sorumlusu, ortam, kaynak, bi?im, kategori, i?e aktar?m tarihi ile k?salt?lm?? parmak izi ve seri numaras? g?r?l?r. Bu pencere kayd? de?i?tirmez ve sertifika de?erini g?stermez.

Ekrandaki **Canl? tarama** ifadesi, eldeki envanter noktalar?n?n g?rsel radar hareketidir. A? hedeflerine ba?lanmaz, TLS el s?k??mas? yapmaz ve Discovery ?al??t?rmaz.

### Sertifika ge?erlilik takvimi

Takvim yaln?z s?resi dolmam??, iptal edilmemi? ve ge?erlilik tarihi bulunan kay?tlar? sayar. G?r?nen s?tun etiketi ile kapsad??? ger?ek kalan s?re ??yledir:

| G?r?nen etiket | Ger?ek kalan s?re |
| --- | --- |
| 180+ g?n | 181 g?n ve ?zeri |
| 180 g?n | 91?180 g?n |
| 90 g?n | 61?90 g?n |
| 60 g?n | 31?60 g?n |
| 30 g?n | 16?30 g?n |
| 15 g?n | 8?15 g?n |
| 7 g?n | 2?7 g?n |
| 1 g?n | 1 g?n |
| Bug?n | 0 g?n |

Ba?l?ktaki ilk say? bu aral?klara girebilen kay?tlar?, ikinci say? etkin kasadaki toplam sertifika kayd?n? g?sterir. S?resi dolmu? ve tarihi olmayan kay?tlar burada de?il, durum bile?eninde izlenir.

### Sertifika durumlar?

Durum bile?eni t?m sertifika kay?tlar?n? be? s?n?fa ay?r?r:

| Durum | Hesaplama |
| --- | --- |
| Ge?erli | 30 g?nden fazla s?resi kalan kay?t. |
| Yenileme aral???nda | Bug?n dahil 30 g?n veya daha az s?resi kalan kay?t. |
| S?resi doldu | Biti? tarihi ge?mi? kay?t. |
| ?ptal / pasif | Kay?t durumu iptal veya pasif olarak i?aretlenmi? kay?t; biti? tarihinden ?nce de?erlendirilir. |
| Tarih yok | Okunabilir bir biti? tarihi bulunmayan kay?t. |

Durum hesab?nda **?ptal / pasif** ?nceliklidir. Bu nedenle iptal edilmi? bir kay?t, biti? tarihi ge?mi? veya eksik olsa bile **S?resi doldu** ya da **Tarih yok** yerine **?ptal / pasif** alt?nda say?l?r.

**Dikkat** say?s?, ge?erli d???ndaki d?rt s?n?f?n toplam?d?r. Toplam sertifika d??mesi Sertifikalar ekran?ndaki t?m sertifikalar? a?ar; belirli bir durum sat?r? yaln?z o durumla filtrelenmi? listeyi a?ar. **Dikkat** halkas? da t?klanabilir, ancak dikkat say?s? s?f?rdan b?y?k oldu?unda her zaman **Yenileme aral???nda** filtresine gider. Dikkat yaln?z s?resi dolmu?, iptal/pasif veya tarihi eksik kay?tlardan geliyorsa sonu? bo? olabilir. Kesin inceleme i?in adland?r?lm?? durum sat?r?n? se?in. Dikkat say?s? s?f?rsa halka **Ge?erli** filtresini a?ar.

### Sertifika da??l?m?

Da??l?m alan? kay?tlar? ?? y?nden gruplar:

- **Kaynak:** Manuel, ??e aktar?lan, AD sync ve Di?er. **Di?er** yaln?z ?zet grubudur; ayr? bir kaynak filtresi yoktur.
- **CA:** Kay?t meta verisinden s?n?fland?r?lan sertifika otoritesi.
- **Organizasyon:** Kay?tlardan ??kar?lan ilk d?rt organizasyon grubu.

**Manuel**, **??e aktar?lan** ve **AD sync** kaynak sat?rlar? ile CA ve organizasyon sat?rlar? Sertifikalar ekran?n? ilgili filtreyle a?ar. **Di?er** kaynak sat?r? ayr? bir kaynak de?erine ba?l? de?ildir; se?ildi?inde g?venilir bir ?Di?er kaynak? ayr?nt?s? a?maz ve organizasyon filtresine d??ebilir. Di?er kaynaklar? incelemek i?in Sertifikalar ekran?n? do?rudan a??p kay?tlar?n kaynak alan?n? g?zden ge?irin. ?stteki ?zet g?rseli gruptaki ilk dolu b?l?m? a?ar; Kaynak grubunda ilk b?l?m **Di?er** ise ayn? s?n?rlama ge?erlidir.

## Filtreler ve Ayr?nt?ya ?nme

- Ge?erlilik takvimindeki dolu bir s?tun, o s?re aral???n? **Sertifikalar** ekran?nda ak?ll? filtre olarak a?ar.
- Durum sat?rlar? **Ge?erli**, **Yenileme aral???nda**, **S?resi doldu**, **?ptal / pasif** veya **Tarih yok** filtresine gider.
- Manuel, ??e aktar?lan ve AD sync kaynak sat?rlar? ile CA ve organizasyon sat?rlar? ayn? de?erle filtrelenmi? sertifika envanterine gider. **Di?er** kaynak sat?r? bu garantinin d???ndad?r.
- Radar noktas? Sertifika Panelinden ayr?lmadan meta veri penceresi a?ar; kay?t d?zenleyicisini a?maz.
- Bir filtre beklenenden az sonu? g?steriyorsa etkin kasay? kontrol edin. Panel ve ayr?nt? listesi yaln?z se?ili kasan?n okunabilir kay?tlar?n? kullan?r.

## Envanter, HTTPS ve Discovery Ayr?m?

| Y?zey | Veri kayna?? | Ne anlat?r | ??lem yeri |
| --- | --- | --- | --- |
| Sertifika Paneli | Etkin kasadaki sertifika kay?tlar? | Kay?tl? ge?erlilik, durum, otorite, kaynak ve organizasyon meta verisi | Sertifikalar ekran? |
| Taray?c? HTTPS eri?imi | VaultPilot sunucusunun etkin HTTPS yap?land?rmas? | Taray?c?n?n ba?land??? sunucu sertifikas?, g?ven zinciri ve genel sunucu ad? | Sunucu ayarlar? ve Public host/HTTPS rehberi |
| Discovery | Yetkilendirilmi?, onayl? ?zel hedeflere yap?lan s?n?rl? aktif TLS ba?lant?s? | S?re, hen?z ge?erli olmama, kendinden imzal? sertifika, hostname uyumsuzlu?u ve yinelenen parmak izi bulgular? | Discovery ekran? |

Bir kasa kayd?n?n konusu ile alan ad? farkl? g?r?n?yor diye Sertifika Paneli tek ba??na **hostname uyumsuzlu?u** karar? vermez. Bu karar, beklenen hedef ad? ile sunulan SAN/CN bilgisini kar??la?t?ran Discovery bulgusundan veya taray?c?n?n ba?land??? ger?ek HTTPS u? noktas?ndan gelmelidir.

## ?nerilen ?? Ak??lar?

### S?resi dolmu? veya yenileme aral???ndaki kayd? inceleme

1. **Sertifika durumlar?** i?inden **S?resi doldu** veya **Yenileme aral???nda** sat?r?n? se?in.
2. Sertifikalar ekran?ndaki filtreli kay?tlar?n biti? tarihini, ortam?n?, sorumlusunu ve kullan?m ba?lam?n? do?rulay?n.
3. Yenileme onay sahibini ve hedef tarihi kurum i?i de?i?iklik kayd?nda belirleyin.
4. Yeni materyali bu panelden y?klemeyin. Envanter kayd? i?in Sertifikalar ekran?n?, sunucu HTTPS paketi i?in Sunucu ayarlar?n? kullan?n.
5. De?i?iklikten sonra paneli yenileyip durum ve s?re aral???n?n beklendi?i gibi g?ncellendi?ini do?rulay?n.

S?resi dolmu? kay?t takvimde g?r?nmez; **S?resi doldu** durum sat?r?nda kal?r. Takvim s?tununun bo? olmas?, s?resi dolmu? kay?t olmad??? anlam?na gelmez.

### Hostname uyumsuzlu?unu ele alma

1. Uyar?n?n adres ?ubu?undaki VaultPilot HTTPS ba?lant?s?ndan m?, Discovery bulgusundan m? geldi?ini belirleyin.
2. Taray?c? uyar?s?ysa kullan?lan URL ile Sunucu ayarlar?ndaki genel sunucu ad?n? ve etkin sertifika kayna??n? kar??la?t?r?n.
3. Discovery bulgusuysa beklenen hedefi, ba?lant? noktas?n? ve hassas ayr?nt?lar? ??kar?lm?? SAN/CN ?zetini ?zel kay?tta do?rulay?n.
4. Yaln?z envanter kayd?nda ad farkl?l??? g?r?yorsan?z bunu do?rulanm?? hostname uyumsuzlu?u diye raporlamay?n; ger?ek u? nokta kan?t? isteyin.
5. ?zel anahtar, sertifika parolas? veya PFX/P12 paketi olmadan ??z?lemeyecek bir durumda ?zel destek kanal?na ge?in.

### Ge?erlilik tarihi eksik kayd? d?zeltme

1. **Tarih yok** durum sat?r?n? se?in.
2. Kayd?n yaln?z meta veri tutmak ?zere olu?turulmu? bir sertifika kayd? m?, yoksa eksik meta verili bir sertifika i?e aktar?m? m? oldu?unu do?rulay?n.
3. Yetkili ve yaz?labilir durumda kayd? Sertifikalar ekran?ndan d?zeltin veya onayl? kaynaktan yeniden i?e aktar?n.
4. Paneli yenileyip kayd?n do?ru s?re aral???na ve duruma ge?ti?ini kontrol edin.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Yenileniyor | Panelin yenilenmesi tamamlanana kadar ikinci bir yenileme ba?latmay?n. |
| Sertifika kayd? yok | Etkin kasay? ve kasa okuma yetkisini do?rulay?n; ba?ka y?zeylerdeki sertifikalar?n burada g?r?nmesi beklenmez. |
| Ge?erli kay?tlar | 60+ g?n band?n? sakin izleyin; sorumlu ve ortam meta verisinin g?ncel kald???n? do?rulay?n. |
| Yenileme aral??? | 30 g?n ve alt?ndaki kay?tlar i?in onay sahibi ve hedef tarih belirleyin. |
| S?resi dolmu? | ?lgili kullan?m? do?rulay?n; yenileme veya kontroll? kullan?m d??? b?rakma karar? verin. |
| ?ptal / pasif | Kayd?n bilerek pasifle?tirildi?ini ve art?k etkin kullan?m kan?t? olmad???n? do?rulay?n. |
| Tarih yok | Meta veriyi do?rulamadan kayd? sa?l?kl? kabul etmeyin. |
| Salt okunur lisans | Grafik, meta veri penceresi ve filtreli liste kullan?labilir; kay?t ekleme, d?zenleme, iptal etme ve silme kapal?d?r. |

## ??lemden ?nce

- Do?ru kasan?n se?ili ve kilidinin a??k oldu?unu do?rulay?n.
- Envanter kayd?, taray?c? HTTPS sertifikas? ve Discovery bulgusu aras?ndaki i?lem s?n?r?n? belirleyin.
- Biti? tarihi, otorite, konu, ortam, kay?t sorumlusu ve kullan?m ba?lam?n? birlikte kontrol edin.
- Sertifika kayd?n? de?i?tirmek i?in kasada D?zenleyici veya Y?netici yetkisi ve yaz?labilir lisans gerekti?ini unutmay?n.
- Sunucu HTTPS de?i?ikli?i ?ncesinde onayl? bak?m penceresi, geri d?n?? yolu ve yeni paketin kullan?labilir oldu?unu do?rulay?n.

## G?venli Kan?t

- Payla??labilir: kay?t say?s?, durum s?n?f?, geni? s?re aral??? ve onayl? genel CA s?n?f?.
- Gizli kalmal?: alan ad?, konu/SAN ?zeti, organizasyon, ortam, kay?t sorumlusu, dosya ad?, imzalayan ile k?salt?lm?? parmak izi ve seri numaras?. Bunlar? yaln?z ?zel destek veya kurum i?i kay?tta kullan?n; i? sunucu adlar?n? ve m??teri kimli?ini maskeleyin.
- Asla payla?may?n: ?zel anahtar, sertifika parolas?, kay?t i?indeki gizli de?er, `.pfx`, `.p12`, `.pkcs12`, parola korumal? paket veya ?zel anahtar i?eren PEM/KEY i?eri?i.
- Tam sertifika ve zincir ?zel anahtar i?ermese bile i? alan adlar?n? ve kurum topolojisini a???a ??karabilir; a??k kanala koymadan ?nce kurum onay? ve tam redaksiyon uygulay?n.
- Ekran g?r?nt?s?nde m??teri ad?, i? alan ad?, e-posta, dosya yolu, parmak izi ve seri numaras?n? yaln?z k?rpmay?n; tamamen maskeleyin.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Uyar?n?n hangi y?zeye ait oldu?u belirlenemiyorsa, yenilenen sertifika yanl?? alan ad?n? g?steriyorsa, g?ven zinciri bilinmiyorsa, ?zel anahtar?n d??ar? ??km?? olabilece?inden ??pheleniyorsan?z veya de?i?iklik i?in gerekli paket ve parola do?rulanam?yorsa i?lem yapmay? b?rak?n. Gizli materyali eklemeden; y?zeyi, genel hata s?n?f?n?, redakte hedefi, s?re aral???n? ve uygulanan son g?venli ad?m? i?eren ?zel destek kayd? a??n.

## Operat?r Notlar?

Sertifika Paneli bir envanter ve ?nceliklendirme ekran?d?r. Buradaki renkler, kay?t meta verisine g?re risk s?ralar; ger?ek u? nokta g?venini, Windows sertifika deposunu veya taray?c? zincir do?rulamas?n? kan?tlamaz.

## ?lgili

- [Sertifikalar ekran?](screen-certificates.md)
- [Discovery ekran?](screen-discovery.md)
- [Sunucu ayarlar?](screen-server-settings.md)
- [Public host ve HTTPS](public-host-https-certificate.md)
- [HTTPS sertifika uyar?s?](../../kb/tr/certificate-warning.md)
