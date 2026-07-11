# Payla??m Ekran?

?st ?ubuktaki `?`, Payla??m ekran?ndan bu rehberi a?ar. Bu ekran, aktif kasadaki se?ili kay?tlar? ba?ka bir VaultPilot kullan?c?s?n?n kendi kasas?na alabilece?i ?ifreli bir dahili paket olarak veya VaultPilot d???nda ?evrimd??? a??lacak parola korumal? bir dosya olarak haz?rlar.

D?? payla??m bar?nd?r?lan bir portal, herkese a??k ba?lant? veya merkezi PAM teslim hizmeti de?ildir. VaultPilot d?? paketi sunucuda saklamaz; al?c? hesab?, d?? paket ge?mi?i veya da??t?lm?? d?? paketi merkezi olarak geri alma i?lemi olu?turmaz.

## Eri?im, Roller ve Lisans

- Payla??m?n normal gezinmede g?r?nmesi i?in lisans?n `sharing` ?zelli?ini i?ermesi ve salt okunur olmamas? gerekir. Auditor gizli kay?t ?al??ma alanlar?n? kullanamaz.
- Kay?tlar? g?rmek ve paketlemek i?in aktif kasan?n kilidi a??k, kasa anahtar? taray?c?da kullan?labilir olmal?d?r.
- **Dahili paket g?ndermek** i?in sistem rol? Owner veya Admin, kaynak kasada Manager rol? ve yaz?labilir lisans gerekir.
- **D?? paket olu?turmak** i?in kaynak kasada Manager rol? ve yaz?labilir lisans gerekir. Sistem User, kasada Manager ise bu yerel ak??? kullanabilir.
- **Gelen paketi kendi kasana kaydetmek** i?in hedef aktif kasada Editor veya Manager rol? ve yaz?labilir lisans gerekir. Bu i?lem kaynak kasaya eri?im vermez.
- Dahili al?c?; ayn? organizasyonda, aktif, g?nderen d???nda, Auditor olmayan ve kullan?labilir a??k anahtar? bulunan bir kullan?c? olmal?d?r. Listede g?r?nen 2FA durumu bilgilendirmedir; al?c? se?im ko?ulu de?ildir.

Salt okunur veya ?zellik d??? durumda eski/a??k ekran durumunu yazma izni saymay?n. Normal ak??? yeniden a??n ve rol, kasa ile lisans durumunu do?rulay?n.

## ?? Ad?ml? Ak??

Ad?m g?stergesi **Se?**, **G?nder** ve **Sonu?** a?amalar?ndan olu?ur. Ad?mlar aras?nda geri d?nebilirsiniz; ancak ekranda g?r?nen se?im ?zeti son kontrold?r.

### 1. Kay?tlar? se?in

Parola, Active Directory kimlik bilgisi, API anahtar?, not, sertifika ve dosya kay?tlar? se?ilebilir. Arama; ba?l?k, kullan?c? ad?, URL, host, domain ve kay?t t?r? etiketinde ?al???r. **T?m?** veya t?r sekmeleriyle listeyi daraltabilir; tek kay?t, g?r?n?r kay?tlar?n t?m? ya da g?r?n?r t?r grubu se?ilebilir.

Filtre d???na ??kan se?ili kay?tlar se?ili kalabilir. **T?m?n? se?** yaln?z o an g?r?n?r kay?tlar? mevcut se?ime ekler. ?stteki **Se?imi temizle**, filtre arkas?nda kalanlar dahil b?t?n se?imi siler; **Grubu ??kar** ise yaln?z o grupta o anda g?r?n?r kay?tlar? kald?r?r. G?ndermeden ?nce toplam se?ili say?s?n? ve t?r ?zetini kontrol edin; gizli kalm?? bir kayd? fark etmeden pakete eklemeyin.

Dosya kay?tlar?n?n par?alar? yaln?z taray?c?da ??z?l?r ve payla??m anahtar?yla yeniden ?ifrelenir. Dosya bilgisi veya par?alardan biri eksikse paket olu?turulmaz.

### 2. S?re ve kullan?m hakk?n? belirleyin

Ge?erlilik s?resi 1 saat ile 720 saat (30 g?n), kullan?m hakk? 1 ile 25 aras?ndad?r. Aray?z 1 saat, 24 saat, 3 g?n, 7 g?n ve 30 g?n k?sayollar? sunar.

- Dahili pakette s?re, kullan?m sayac? ve durum sunucuda uygulan?r.
- D?? pakette s?re do?rulanm?? manifestten ve al?c? cihaz?n?n saatinden kontrol edilir.
- D?? paketin kullan?m hakk?, manifest hash'iyle o taray?c? profilinin `localStorage` alan?nda tutulan yerel saya?t?r. Ba?ka taray?c?/profil veya temizlenmi? taray?c? depolamas? yeni bir saya?la ba?lar. Bu de?er organizasyon genelinde limit, denetim veya geri alma s?n?r? de?ildir.
- D?? ??zme i?lemi ba?ar?l? oldu?unda bir yerel hak, i?erik g?sterilmeden ?nce t?ketilir. Sonraki dosya indirme hatas? bu hakk? geri vermez.

### 3. G?nderim y?ntemini se?in

Ayn? se?im ve politika, a?a??daki dahili veya d?? ak??lardan yaln?z biriyle tamamlan?r. Bu iki yolun saklama, kullan?m ve geri alma s?n?rlar? farkl?d?r.

## Dahili Payla??m

**Dahili al?c?** b?l?m?nde hedef VaultPilot kullan?c?s?n? se?ip **Se?ili kay?tlar? g?nder** i?lemini ba?lat?n. Taray?c? yeni bir AES-GCM paket anahtar? ?retir, se?ili kay?tlar? bu anahtarla ?ifreler ve anahtar? al?c?n?n kay?tl? a??k anahtar?yla sarar. Sunucu d?z metin kay?t veya paket anahtar? yerine ?ifreli paket, sar?lm?? anahtar, se?im hash'leri ve politika meta verisini saklar.

Dosya i?eren dahili paket ?ok ad?ml?d?r:

1. Paket kayd? ?nce `PENDING` ve `packageReady=false` olarak olu?turulur.
2. Dosya par?alar? taray?c?da yeniden ?ifrelenip sunucuya tek tek y?klenir.
3. Say? ve byte toplam? e?le?ince paket haz?r olarak i?aretlenir.

Al?c? yaln?z haz?r, `PENDING`, s?resi ge?memi? ve kullan?m hakk? kalm?? paketleri **Gelen payla??mlar** alt?nda g?r?r. **Kendi kasama kaydet**, paketi al?c?n?n ?zel anahtar?yla taray?c?da a?ar; her kayd? ve dosya par?as?n? o anda aktif olan yaz?labilir hedef kasan?n anahtar?yla yeniden ?ifreleyerek yeni kay?tlar olu?turur. T?m yaz?mlar bittikten sonra sunucudaki kullan?m say?s? art?r?l?r. Limit hen?z dolmad?ysa paket `PENDING` kalabilir ve yeniden kullan?labilir; dolunca `ACCEPTED` olur.

Bu bir kaynak kasaya ?yelik veya canl? senkronizasyon de?ildir. Sonradan de?i?en kaynak kay?tlar kopyaya aktar?lmaz.

Active Directory kimlik bilgisi se?im listesinde g?r?n?r; ancak mevcut kabul ak??? yeni kayd? olu?tururken zorunlu dizin sa?lay?c?s?/DN kaynak alanlar?n? iletmez. Bu t?r bir kay?t hedef kasaya al?n?rken sunucu taraf?ndan reddedilebilir. Ba?ar?l? oldu?u do?rulanmadan Active Directory kayd?n? dahili payla??m teslimat? olarak planlamay?n.

### Gelen ve giden listeleri

- **Gelen payla??mlar** ge?mi? de?ildir; yaln?z al?nabilir durumdaki haz?r paketleri g?sterir. Kabul edilmi?, geri al?nm??, s?resi dolmu?, hakk? bitmi? veya h?l? haz?rlanmakta olan paketler burada g?r?nmez.
- **Son g?nderilenler** yaln?z en yeni alt? dahili paketi g?sterir. Sunucu, kullan?c?ya ait en yeni 100 gelen/giden paketi d?nd?r?r; daha eski paketler bu ekran?n g?r?n?r ge?mi?i de?ildir.
- Durumlar **Haz?rlan?yor**, **Bekliyor**, **Kullan?ld?**, **S?resi doldu** ve **Geri al?nd?** olabilir.
- Mevcut aray?z, **Geri al** d??mesini yaln?z g?nderenin kendi `PENDING`, s?resi ge?memi? ve hakk? kalm?? paketi i?in g?sterir. Bu ko?ul yaln?z d??menin g?r?n?rl???n? belirler; sunucudaki geri alma yolu ?u anda oturum a?m?? g?nderene ait her paketi durumuna, s?resine veya kalan hakk?na bakmadan kabul eder. Geri alma paketi `REVOKED` durumuna ge?irir ve sonraki a??l??lar? engeller; al?c?n?n daha ?nce kendi kasas?na kaydetti?i kopyalar? veya kaynak kay?tlar? silmez.

## D?? Parola Paketi

**D?? paket olu?tur**, taray?c?da 28 karakterlik g??l? bir payla??m parolas? ?retir. Se?ili y?k AES-256-GCM ile ?ifrelenir; parola anahtar? PBKDF2-SHA-256 ile t?retilir ve s?re, kullan?m hakk?, kapsam ile dosya bilgileri do?rulanm?? manifeste ba?lan?r.

- Dosyas?z yeni paket `.json`, dosyal? paket `.pmshare` olarak indirilir.
- Paket ve parola yaln?z canl? sonu? durumunda g?r?n?r; d?? paket sunucu ge?mi?ine veya **Son g?nderilenler** listesine eklenmez.
- **Paketi kopyala** veya **Paketi indir** ile korumal? dosyay? al?n. **??zme arac?n? indir**, `vaultpilot-share-decrypter.zip` dosyas?n? verir.
- Do?rudan teslimatta paket, payla??m parolas? ve ??zme arac?n? onayl? ayr? kanallarla ula?t?r?n. En az?ndan paket ile parolay? hi?bir zaman ayn? kanalda g?ndermeyin.
- **Tamamla** veya **Yeni payla??m** canl? paket, parola ve se?im durumunu temizler. Paketi g?venli konuma almadan tamamlamay?n; ekran kilidini tek ba??na payla??m materyali temizli?i saymay?n. Ak??tan vazge?iyorsan?z sayfay? tamamen yenileyin.

D?? paket da??t?ld?ktan sonra VaultPilot'ta geri alma i?lemi yoktur. Yeni paket ?retmek eskisini ge?ersiz k?lmaz. Paket veya parola yanl?? ki?iye gittiyse paketi s?re sonuna kadar a??labilir kabul edin ve i?indeki s?rlar? kendi sahiplik prosed?rleriyle de?i?tirin ya da iptal edin.

### SMTP ile g?nderim

Sonu? ekran?ndaki SMTP i?lemi, yap?land?r?lm?? VaultPilot SMTP hizmeti ?zerinden tek al?c?ya paket dosyas?n?, ??zme arac? ZIP'ini ve k?sa y?nergeyi g?nderir. Payla??m parolas? e-postaya eklenmez. ?stemci `confirmPassphraseSeparate: true` de?erini sabit g?nderir; aray?z parolan?n ayr? kanaldan iletilmesi gerekti?ini a??klar ancak onay kutusu veya ayr?ca bir operat?r onay? sunmaz. Bu istek alan?, parolan?n ger?ekte hangi kanaldan g?nderildi?ini kan?tlamaz.

SMTP kullan?ld???nda d?? paket teslimat i?in VaultPilot sunucusuna ge?ici olarak g?nderilir ve yap?land?r?lm?? SMTP hizmetinden ge?er; bu nedenle ?paket sunucuya hi? gitmez? ifadesi do?ru de?ildir. Buna ra?men VaultPilot paketi bar?nd?r?lan d?? payla??m kayd? olarak saklamaz.

## Boyut ve ?stek S?n?rlar?

| Yol | Uygulanan s?n?r |
| --- | --- |
| Dahili paket | En fazla 250 kay?t, toplam 512 dosya par?as? ve 1 GiB d?z metin dosya boyutu. |
| Dahili dosya par?as? | Her par?a en fazla 2 MiB; par?a y?kleme iste?i en fazla 8 MiB. |
| Dahili paket olu?turma iste?i | En fazla 1,5 MB istek g?vdesi. B?y?k ?ifreli kay?t y?kleri dosya olmasa da bu s?n?ra tak?labilir. |
| D?? paket do?rudan indirme | Se?ili dosyalar?n toplam? en fazla 1 GiB; mevcut 2 MiB dosya par?alar? kullan?l?r. Dahili 250 kay?t/512 toplam par?a ?emas? yerel indirmeye uygulanmaz. |
| SMTP ile d?? paket | Paket i?eri?i en fazla 12 MiB olabilir; SMTP meta verisindeki kay?t say?s? 250 ile s?n?rl?d?r. Daha b?y?k yerel paket SMTP ile g?nderilemez; onayl? manuel teslimat kullan?n. |

## ??lem B?t?nl??? D???ndaki ve K?smi Durumlar

Payla??m?n t?m ad?mlar? tek bir atomik i?lem i?inde y?r?t?lmez:

- **Dahili olu?turma yar?m kal?rsa:** Paket kayd? ve baz? ?ifreli dosya par?alar? ger?ekten olu?turulmu? olabilir. G?nderen listesinde **Haz?rlan?yor** g?r?n?rken al?c? listesinde g?r?nmez. Yeniden deneme eski paketi s?rd?rmez, yeni paket olu?turur. ?nce mevcut giden paketi ve Denetim G?nl???n? uzla?t?r?n; gerekiyorsa yar?m paketi geri al?n.
- **Gelen paket yar?m al?n?rsa:** Kay?tlar ve dosya par?alar? hedef kasaya tek tek yaz?l?r, kullan?m say?s? en son g?ncellenir. Hata baz? yeni kay?tlar? veya eksik dosyay? kasada b?rakabilir; paket h?l? `PENDING` ve hakk? kullan?lmam?? g?r?nebilir. K?rlemesine yeniden deneme kopya kay?tlar olu?turabilir. Hedef kasay?, gelen/giden durumu ve denetimi kar??la?t?r?n.
- **E?zamanl? kabul:** Kullan?m sayac? ile hedef kasaya yap?lan yaz?mlar ayn? i?lem b?t?nl??? i?inde de?ildir. ?ift t?klama veya iki oturum ayn? paketi e?zamanl? a?arsa limit g?ncellenmeden birden fazla kopya olu?abilir. Tek operat?r ve tek oturumla ilerleyin.
- **D?? olu?turma ve denetim ayr?l?r:** Taray?c? paket ile parolay? olu?turup sonu? alan?na koyduktan sonra genel `SHARE` denetim olay? yaz?l?r. Denetim yaz?m? ba?ar?s?zsa aray?z olu?turma hatas? g?sterebilir ama paket ve parola h?l? bellekte bulunabilir. Sonu? alan?n? ve denetimi kontrol etmeden yeniden ?retmeyin.
- **SMTP denetimi iki a?amal?d?r:** Kal?c? g?nderim-niyeti olay? SMTP'den ?nce yaz?l?r; bu yaz?m ba?ar?s?zsa e-posta g?nderilmez. SMTP kabul?nden sonraki teslimat kan?t? en iyi ?aba ile yaz?l?r ve ba?ar?s?z olsa bile e-posta g?nderilmi? olabilir. Niyet olay? tek ba??na teslimat kan?t? de?ildir; teslimat denetimi eksik diye ayn? paketi hemen tekrar g?ndermeyin.

## Denetim ve Kan?t

- Dahili paket olu?turma `SHARE`; dosya finalizasyonu ayr?nt?l? ikinci `SHARE`; ba?ar?l? kabul `IMPORT`; geri alma `SHARE_REVOKE` ?retir. Hedef kasada olu?an kay?tlar kendi `CREATE`/`IMPORT` izlerini de b?rakabilir.
- Yerel d?? paket olu?turma yaln?z genel `SHARE` olay? yazmay? dener; sunucuda d?? paket sat?r? olu?turmaz.
- SMTP niyet ve teslimat olaylar?; manifest ?zeti, kay?t/kullan?m say?s?, boyut, s?re, kabul say?s? ve mesaj kimli?i gibi gizli alanlar? ??kar?lm?? meta veriler ta??r. Paket i?eri?i, parola, al?c? adresi ve dosya ad? denetim meta verisine yaz?lmaz.
- Denetim olay?n?n bulunmamas? i?lemin hi? ger?ekle?medi?ini; niyet olay?n?n bulunmas? da e-postan?n teslim edildi?ini tek ba??na kan?tlamaz.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Kay?tlar veya paket listesi y?kleniyor | Panel ?zel iskelet g?stermeyebilir. On saniyelik yenilemeyi ve genel sorgu durumunu bekleyin. |
| Payla??lacak kay?t yok | Aktif kasay?, kilit durumunu, arama ve t?r filtresini do?rulay?n. |
| Payla??labilir dahili kullan?c? yok | Kendi hesab?n?z, kapal? kullan?c?lar, Auditor ve ge?erli a??k anahtar? olmayan kullan?c?lar listelenmez. Kullan?c? durumunu ?zel olarak do?rulay?n. |
| Gelen/giden listesi bo? | ?zel sorgu hata kart? yoktur; istek hatas? bo? dizi gibi g?r?nebilir. Bo?lu?u ba?ar? kan?t? saymadan oturumu ve a? iste?ini do?rulay?n. |
| Haz?rlan?yor | Dahili paket kayd? vard?r fakat dosya par?alar? tamamlanmam??t?r. Yeni paket olu?turmadan ?nce uzla?t?r?n veya geri al?n. |
| Bekliyor | Dahili paket haz?rd?r ve al?c? i?in en az bir kullan?m hakk? kalm??t?r. |
| Kullan?ld? / S?resi doldu / Geri al?nd? | Paket yeni kabul i?in kullan?lamaz. Daha ?nce al?nm?? hedef kasa kopyalar? etkilenmez. |
| Gelen payla??m a??lamad? | Hedef kasada k?smi kay?t veya par?a bulunabilece?ini varsay?n; yeniden denemeden ?nce kasay? inceleyin. |
| D?? paket olu?turma hatas? | Sonu? alan?nda paket/parola kalm?? olabilir. Yeni paket ?retmeden ?nce canl? durumu ve denetimi kontrol edin. |
| SMTP hatas? veya belirsiz sonu? | Niyet, UI kabul sonucu, mesaj kimli?i ve ?zel SMTP kan?t?n? uzla?t?r?n; k?r yeniden g?nderim yapmay?n. |
| Decrypter hatas? | Yanl?? parola, de?i?tirilmi? manifest, s?re, yerel hak, taray?c? depolamas? ve s?r?m hatalar?n? ay?r?n; ??z?lm?? i?erik ekran g?r?nt?s? istemeyin. |

## ??lemden ?nce

- Do?ru aktif kasay?, sistem ve kasa rol?n?, `sharing` ?zelli?ini ve yaz?labilir lisans? do?rulay?n.
- Toplam se?ili say?s?n?, t?r ?zetini ve filtre arkas?nda kalan se?imleri inceleyin.
- Dosya toplam?, par?a say?s?, paket boyutu, ge?erlilik ve kullan?m hakk?n? teslim y?ntemine g?re kontrol edin.
- Dahili al?c?n?n aktif kimli?ini ve a??k anahtar?n? ?zel kanaldan do?rulay?n; hedef kasay? al?c? a?ar.
- D?? pakette merkezi geri alma olmad???n? ve kullan?m hakk?n?n yaln?z yerel saya? oldu?unu i?in sorumlusuna a??klay?n.
- Paket, parola ve ??zme arac? i?in onayl? teslim kanallar?n? ?nceden belirleyin; SMTP kullan?yorsan?z parolay? e-postaya koymay?n.
- Yar?m kalm?? giden paket veya hedef kasa yaz?m? varsa yeniden denemeden ?nce paket listesi, hedef kasa ve Denetim G?nl???n? uzla?t?r?n.

## G?venli Kan?t

- Payla??labilir: dahili/d?? yol, genel paket durumu, yakla??k zaman, kay?t ve par?a say?s?, toplam boyut s?n?f?, s?re/kullan?m politikas?, redakte hata kategorisi, k?salt?lm?? paket/manifest kimli?i, SMTP niyet veya kabul durumu.
- Gizli kalmal?: paket JSON/PMShare i?eri?i, payla??m parolas?, ??z?lm?? i?erik, kay?t ba?l?klar? ve kullan?c? adlar?, dosya adlar?/par?alar?, al?c? ad? ve e-posta adresi, tam paket kimli?i/manifest ?zeti, sar?lm?? anahtar, ?ifreli kay?t i?eri?i, kasa ad?/kimli?i, ?zel SMTP mesaj? ve tam ekran g?r?nt?s?.
- Asla parola ile paketi ayn? kan?ta eklemeyin. Paket veya parola herkese a??k kanala girdiyse d?? paketi geri al?nabilir saymay?n; i?erdi?i s?rlar? de?i?tirin ya da iptal edin.

## Ne Zaman Durmal?

Se?im kapsam? belirsizse, hedef kullan?c?/anahtar do?rulanam?yorsa, dosya par?alar? eksikse, Active Directory kimlik bilgisi dahili kabuldeyse, mevcut paket **Haz?rlan?yor** durumundaysa, hedef kasada k?smi kabul ??phesi varsa, d?? paket sonucu denetimle ?eli?iyorsa, SMTP sonucu belirsizse veya paket/parola ayn? kanala girdiyse durun. Yeni paket ya da ikinci kabul ?retmeden ?nce redakte kimlikler, zaman, durum ve denetim kan?t?yla ?zel inceleme yap?n.

## Operat?r Notlar?

Dahili payla??m, sunucuda s?n?rl? ve geri al?nabilir bir ?ifreli teslim kuyru?udur; kabul edildi?inde al?c? kasas?nda ba??ms?z kopyalar ?retir. D?? payla??m ise ?evrimd??? dosya teslimidir; da??t?mdan sonra kontrol manifest s?resi, al?c? cihaz?n?n saati, yerel saya? ve s?r rotasyonu disiplinine dayan?r. Bu iki g?ven modelini ayn? ?aktif payla??m? olarak de?erlendirmeyin.

## ?lgili

- [Payla??m ve ?evrimd??? ??zme arac?](sharing-and-offline-decrypter.md)
- [D?? payla??m paketi a??lam?yor](../../kb/tr/external-share-fails.md)
- [Denetim G?nl??? ekran?](screen-audit-log.md)
- [??lemler ekran?](screen-executions.md)
- [G?venli destek kan?t?](support-evidence-pack.md)
