# Yeni Kay?t Ekran?

Genel ?st ?ubuktaki **Yeni kay?t ekle** denetimi Parola, API anahtar?, G?venli not, Sertifika ve Dosya se?eneklerini a?ar; se?ilen t?r? yerel Yeni kay?t d?zenleyicisinde g?sterir. D?zenleyicideki `?` bu k?lavuzu a?ar. Ba?ar?l? kaydetme, ?ifreli kayd? o anda aktif olan kasada olu?turur. D?zenleyicide otomatik kay?t, taslak saklama, ?ablon se?ici veya otomatik rotasyon i?lemi yoktur.

## Eri?im, Aktif Kasa ve Lisans S?n?r?

Genel se?ici ve yerel d?zenleyici Auditor rol?yle a??labilir; bu durum yazma yetkisi vermez. Kaydetmek i?in kilidi a??k bir aktif kasa ve bu kasan?n taray?c?da tutulan anahtar? gerekir. Oturum a?an ki?i sistem d?zeyinde Owner, Admin veya User olmal?; ayr?ca aktif kasada **Editor** ya da **Manager** yetkisine sahip olmal?d?r. Auditor, kasa **Viewer** rol? ve salt okunur lisans durumunda Kaydet denetimi devre d???d?r. ?stemci denetimi a??lmaya ?al???lsa bile sunucu oturumu, lisans?, kasay? ve rol? ba??ms?z olarak do?rular.

Yeni kay?t ekran?nda kasa se?ici yoktur. Kay?t, **?ifreli kayd? kaydet** se?ildi?i s?rada aktif olan kasaya yaz?l?r. Hassas bilgi girmeden ?nce aktif kasay? ba?ka bir ekrandan do?rulay?n. Elle olu?turulan Parola, API anahtar?, G?venli not, Sertifika ve Dosya kay?tlar? i?in yazmaya a??k lisans d???nda ayr? bir ?zellik lisans? aranmaz.

## Elle Olu?turulabilen Kay?t T?rleri

T?r ?eridinde be? se?enek bulunur:

| T?r | Kaydetmek i?in zorunlu | ?ste?e ba?l? ba?lam |
| --- | --- | --- |
| Parola | Ba?l?k ve Parola. | Kullan?c? ad?/e-posta, oturum a?ma adresi, not. |
| API anahtar? | Ba?l?k ve API anahtar? ya da token. | ?stemci/sahip/servis hesab?, konsol adresi, kapsam veya rotasyon notu. |
| G?venli not | Ba?l?k ile ?ifreli not veya ?ste?e ba?l? gizli de?er alanlar?ndan en az biri. | Sahip/ekip ve ilgili sistem bilgisi. |
| Sertifika | Ba?l?k ile sertifika veya ?zel anahtar materyali. | Sahip/servis, u? nokta, not, sona erme tarihi, Subject/CN ve sertifika yetkilisi s?n?f?. |
| Dosya | Ba?l?k ve yeni kay?t i?in se?ilmi? tek dosya. | Sahip/al?c?, ilgili sistem/talep ve dosya notu. |

`CREDENTIAL`, saklanabilen bir s?r t?r?d?r ancak elle se?im ?eridinde bilerek g?sterilmez. Yeni Active Directory kimlik bilgisi kay?tlar? ajan e?itlemesiyle olu?turulur. Elle kimlik bilgisi olu?turma giri?imi reddedilir ve form **Entegrasyonlar > Active Directory** b?l?m?ne y?nlendirir. Yeni kay?t ekran?n? RDP veya SSH kimlik bilgisi olu?turuyormu? gibi anlatmay?n.

Bu formda genel bir Sahip veya Etiketler denetimi yoktur. Hesap alan? t?re ?zg? ba?lamd?r; her durumda sahip alan? say?lmaz. Sertifika yetkilisi se?imi denetimli sertifika etiketleri ekler, di?er genel etiketler burada d?zenlenmez.

## Burada Ne Yap?l?r

- Zorunlu de?eri girmeden ?nce elle olu?turulabilen be? kay?t t?r?nden birini se?in.
- A??k bir ba?l?k yaz?n; yaln?z kayd? g?venle bulmak ve i?letmek i?in gereken ba?lam alanlar?n? doldurun.
- De?eri ?retin veya yap??t?r?n. Sunuluyorsa ve kurum ilkesi izin veriyorsa iste?e ba?l? s?z?nt? kontrol?n? ayr?ca ?al??t?r?n.
- Sertifika materyalini i?e aktar?n ya da belgelenen s?n?rlar i?inde tek dosya se?in.
- **?ifreli kayd? kaydet** se?ene?ine basmadan ?nce aktif kasay? ve yazma yetkisini yeniden kontrol edin.
- Mevcut formu silip se?ili t?r?n listesine d?nmek i?in geri okunu kullan?n.

## T?r De?i?ikli?i ve Ortak Taslak Alanlar?

Be? elle kay?t t?r? aras?nda ge?i? yapmak etiketleri ve ?zel denetimleri de?i?tirir; ayr? ve ba??ms?z yeni bir taslak ba?latmaz. Ba?l?k, hesap, gizli de?er, adres, not, sertifika bilgileri, dosya bilgisi veya se?imi, kategori, kaynak ve etiketler ortak form durumunda kalabilir; yaln?z kimlik bilgisine ?zg? ba?lant? alanlar? ??kar?l?r. Bu nedenle sertifika, dosya veya s?n?fland?rma verisi ba?ka bir t?rde gizlenebilir, yeniden g?r?nebilir ya da sonraki kaydetmeyi etkileyebilir.

Materyal girmeden ?nce genel se?iciden do?ru t?r? a??n. Sertifika i?e aktard?ktan, dosya se?tikten veya sertifika yetkilisi s?n?f? belirledikten sonra t?r de?i?tiyse en g?venli yol formu s?f?rlamak ya da geri d?nmek, do?ru t?r? yeniden a?mak ve g?ncel materyali yeniden girmek veya se?mektir. T?r? bilerek de?i?tirdiyseniz Kaydet ?ncesinde hem g?r?nen alanlar? hem daha ?nce girilmi? gizli veriyi yeniden kontrol edin. Form g?nderilene kadar hi?bir alan kaydedilmez; otomatik kay?t veya kay?tl? taslak listesi yoktur.

## De?er ?retme, G?? ve S?z?nt? Kontrol?

Parola ?retici, Dosya d???ndaki b?t?n elle kay?t t?rlerinde kullan?labilir. K???k harfler se?im havuzunda her zaman bulunur; B?y?k harf, Rakam ve Sembol se?enekleri kendi k?melerini bu havuza ekler. Birle?ik havuzdan rastgele se?im, k???k harf dahil herhangi bir k?meden en az bir karakter gelece?ini garanti etmez. G?r?nen uzunluk ayar? 12?64 karakter aral???ndad?r; varsay?lan de?er 24't?r ve ?? se?enek de a??kt?r. ?retim taray?c?n?n kriptografik rastgeleli?ini kullan?r, mevcut gizli de?er alan?n?n ?zerine yazar ve kayd? kendili?inden kaydetmez.

**K?sa / Haz?r / G??l?** g?stergesi yaln?z uzunlu?a g?re bilgi verir: 16 karakterden az, 16?23 veya 24 ve ?zeri. ?lke karar?, entropi kan?t?, s?z?nt? sonucu ya da kaydetme ko?ulu de?ildir.

S?z?nt? d??mesi g?sterildi?inde kontrol ancak operat?r d??meye bast?ktan sonra ?al???r. Taray?c? de?erin SHA-1 ?zetini al?r ve HIBP Pwned Passwords aral?k servisine yaln?z ilk be? ?zet karakterini g?nderir; tam de?er g?nderilmez. Formdaki sonu? mevcut alan?n ?zetiyle ba?l? tutulmaz: kontrol sonras?nda de?er ?retmek, yap??t?rmak veya d?zenlemek eski sonucu ekranda b?rakabilir; bu sonu?, Dosya d???ndaki ba?ar?l? kay?ttan sonra kayd?n taray?c?daki yerel s?z?nt? durumuna aktar?labilir. ?nce son de?eri belirleyin, ard?ndan Kaydet'e basmadan hemen ?nce s?z?nt? kontrol?n? yeniden ?al??t?r?n. Kontrol hatas? kayd? kaydetmez veya de?i?tirmez; ekrandaki eski sonucun g?ncel de?erle e?le?ti?ini de kan?tlamaz.

## Sertifika ??leme

Sertifika materyali **Sertifika veya ?zel anahtar** alan?na yap??t?r?labilir ya da dosyadan i?e aktar?labilir. Dosya se?ici PEM, CRT, CER, DER, P7B/P7C, PFX/P12/PKCS12, P8/P8E/PK8 ve KEY bi?imlerini sunar. Se?ilen sertifika dosyas? en fazla 10 MB olabilir.

??e aktarma s?ras?nda taray?c? SHA-256 ?zetini hesaplar ve dosyan?n ?zg?n baytlar?n? ?ifreli kay?t y?k?n?n i?ine koyar. Metin bi?imleri ??z?mlenir; bulundu?unda basit `Subject`, `Issuer`, `Serial` ve sona erme etiketleri okunur. ?kili bi?imler base64 materyali olarak sar?l?r. Bu i?lem envantere i?e aktarmad?r; sertifika zinciri veya ?zel anahtar i?in tam do?rulama de?ildir. **Sertifika dosyas? ?ifreli kay?t alan?na al?nd?.** bildirimi, materyalin mevcut formda bulundu?u anlam?na gelir; Kaydet ba?ar?l? olana kadar kay?t kal?c? de?ildir.

Sona erme tarihi ve Subject/CN formda d?zeltilebilir. DigiCert, GoDaddy, GlobalSign, Let's Encrypt, Microsoft CA veya Self-signed se?mek yaln?z kayd?n sertifika kategorisini ve s?n?fland?rma etiketlerini de?i?tirir. ?lgili sertifika yetkilisine ba?lanmaz; hesab? do?rulamaz; sertifika sipari? etmez, yenilemez, yeniden d?zenlemez, iptal etmez veya da??tmaz.

## Dosya ??leme ve S?n?rlar

Yeni Dosya kayd? i?in tek dosya se?ilmelidir. Se?im form t?r?n? Dosya olarak de?i?tirir, Ba?l?k h?l? bo?sa dosya ad?n? ba?l?k olarak doldurur, gizli de?er alan?n? temizler ve boyut ile par?a say?s?n? g?sterir. Parola ?retici ve gizli de?er d?zenleyicisi Dosya t?r?nde bulunmaz.

Dosya boyutu ve depolama tavan?, aktif kasada kullan?c? ba??na 1 GB'dir. Dosyalar en fazla 2 MB'lik par?alara ayr?l?r ve en ?ok 512 par?a olabilir. Kaydet s?ras?nda taray?c? ?nce b?t?n dosyan?n SHA-256 ?zetini hesaplar, ?ifreli Dosya kayd?n? olu?turur, o kayd?n varsa mevcut par?alar?n? temizler; ard?ndan her par?ay? aktif kasa anahtar?yla ?ifreleyip y?kler. Sunucu kota uygulamak i?in ?ifreli par?alarla birlikte boyut ve par?a konumu bilgisini saklar; d?z metin dosya baytlar?n? almaz.

Dosya kayd?n?n olu?turulmas? ve par?alar?n y?klenmesi ayr? i?lemlerdir. Kay?t olu?turulduktan veya baz? par?alar kabul edildikten sonra y?kleme ba?ar?s?z olursa otomatik i?lem geri alma yoktur. Yeniden denemeden ya da kayd? de?i?tirmeden ?nce Dosyalar ekran?n? yenileyip kay?t ile par?alar?n kullan?labilirli?ini do?rulay?n. Hata bildiriminin hi? kay?t veya k?smi y?kleme kalmad???n? kan?tlad???n? varsaymay?n.

## Taray?c? ?ifrelemesi, Kaydetme ve Denetim Sonucu

Dosya d???ndaki kay?tlar i?in taray?c? form y?k?n?n tamam?n? serile?tirir ve sunucuyu ?a??rmadan ?nce aktif kasa anahtar?yla AES-GCM kullanarak ?ifreler. Sunucu ?ifreli zarf?, kay?t t?r?n?, kasa kimli?ini, oturum rol?n?, lisans kipini ve kasa yazma yetkisini do?rular; d?z metin ba?l?k, hesap, de?er, adres, not veya sertifika materyalini almaz.

Taray?c?n?n yerle?ik zorunlu alan do?rulamas?; g?nderme i?leyicisinden, taray?c? ?ifrelemesinden ve sunucu iste?inden ?nce ?al???r. Bu do?rulama ge?erse g?nderme i?leyicisi a?a??daki ko?ullar? s?rayla kontrol eder:

1. Aktif kasa ve taray?c?daki kasa anahtar? bulunmal?d?r.
2. Lisans ve aktif kasa rol? yazmaya izin vermelidir.
3. Yeni Active Directory kimlik bilgisi bu ekrandan olu?turulamaz.
4. Her t?r i?in Ba?l?k zorunludur.
5. Parola, API anahtar? ve Sertifika i?in gizli de?er bo? b?rak?lamaz.
6. G?venli not i?in not i?eri?i veya iste?e ba?l? gizli de?er bulunmal?d?r.
7. Yeni Dosya i?in se?ilmi? ya da formda kalm?? dosya bilgisi bulunmal?; yeni se?ilen dosya 1 GB s?n?r?n? a?mamal?d?r.

Bu taray?c? kontrolleri operat?re geri bildirim sa?lar; yetkilendirme s?n?r? de?ildir. ??leyici y?k? ?ifreledikten sonra sunucu oturumu, ?ifreli zarf?, kay?t t?r?n?, kasa kimli?ini, lisans kipini ve kasa yazma rol?n? ba??ms?z olarak do?rular. Eri?imi korumak i?in yerel Kaydet d??mesine veya yerel zorunlu alanlara g?venmez.

Sertifika i?e aktarma, ?ifreleme, kaydetme veya dosya y?kleme s?rerken g?nderme denetimi devre d??? kal?r ve ilerleme g?sterilir. Aktif kaydetme veya y?kleme i?lemi i?in form i?inde iptal d??mesi yoktur.

Ba?ar?l? olu?turmadan sonra Parola, API anahtar? ve G?venli not `CREATE`; Sertifika ve Dosya ise `IMPORT` denetim olay? yazar. Dosya par?alar?n? haz?rlama, kayd?n mevcut par?a k?mesini temizledi?i i?in ayr?ca `EDIT` denetim olay? ?retir. Form s?f?rlan?r, ilgili kay?t listesi a??l?r, s?r ve denetim sorgular? yenilenir. Ba?ar? bildirimi sunucuda ?ifreli saklamay? do?rular; kimlik bilgisinin s?nand???n?, sertifikan?n da??t?ld???n? veya dosyan?n ba?ar?yla a??ld???n? g?stermez.

## ?ptal ve Hata Davran???

- Geri oku yerel formu s?f?rlar ve kaydedilmemi? de?i?iklik onay? g?stermeden se?ili t?r?n listesine d?ner. Gezinme, ba?lam?? sertifika okuma, kaydetme veya y?kleme i?ini durdurmaz. Gezinmeyi iptal y?ntemi olarak kullanmay?n; tamamlanma ya da hatay? bekleyip listeyi ve Denetim G?nl???n? uzla?t?r?n.
- Yeni kay?t i?in ayr? ?ptal d??mesi yoktur. **D?zenlemeyi iptal et** yaln?z mevcut ve d?zenlenebilir bir kay?tta g?r?n?r; se?ildi?inde d?zenleme kipini kapat?r ve kay?t listesine d?nmek yerine Yeni kay?t ekran?nda bo? bir Parola tasla?? b?rak?r.
- S?n?r? a?an Dosya reddedildi?inde o anki se?ici temizlenir ancak ?nceki dosya bilgisi ortak formda kalabilir. S?n?r? a?an veya okunamayan sertifika dosya giri?ini temizler ancak ?nceki sertifika materyali, bilgileri veya s?n?fland?rma etiketleri kalabilir. Bu hatalardan sonra formu s?f?rlay?n ya da Yeni kay?ttan ??k?p yeniden a??n; do?ru t?r? ve g?ncel dosyay? yeniden se?ip Kaydet ?ncesinde ?zeti do?rulay?n.
- ?o?u do?rulama ve kaydetme hatas?nda form, operat?r?n d?zeltme yapabilmesi i?in bellekte kal?r. Sayfay? yenileme, kilitleme, gezinme s?f?rlamas? veya geri okunun tasla?? saklayaca??n? d???nmeyin.
- Ba?ar?s?z kaydetme ekranda hata ve canl? uygulama bildirimi ?retir. Yan?t?n tamam?n? veya form i?eri?ini herkese a??k deste?e yap??t?rmay?n.
- Dosya y?kleme kay?t olu?turulduktan sonra ba?ar?s?z olabilir; yeniden denemeye karar vermeden ?nce Dosyalar ve Denetim G?nl??? ekranlar?n? kontrol edin.

## ?nerilen ?? Ak??lar?

### Parola, API anahtar? veya G?venli not olu?turma

1. Aktif kasay? ve Editor ya da Manager rol?n? do?rulay?n.
2. Kesin kay?t t?r?n? se?ip Ba?l?k girin.
3. Zorunlu de?eri ekleyin; G?venli not i?in not i?eri?i, gizli de?er veya ikisini birden kullan?n.
4. Yaln?z gerekli hesap, adres ve i?letim ba?lam?n? ekleyin.
5. ?sterseniz de?er ?retin. Son de?eri belirledikten sonra Kaydet'e basmadan hemen ?nce s?z?nt? kontrol?n? ?al??t?r?n; bu i?lemlerin hi?biri otomatik kaydetmez.
6. **?ifreli kayd? kaydet** se?ene?ine bas?n, tamamlanmas?n? bekleyin ve beklenen liste ile denetim olay?n? do?rulay?n.

### Sertifika kayd? i?e aktarma

1. Sertifika t?r?n? se?ip hassas olmayan bir ba?l?k girin.
2. Onayl? materyali yap??t?r?n veya 10 MB'yi a?mayan destekli bir dosya se?in.
3. SHA-256, bi?im, sona erme tarihi, Subject/CN ve sertifika yetkilisi s?n?f?n? inceleyin. ??e aktar?ld? bildirimi, do?ruland? veya kaydedildi anlam?na gelmez.
4. Kaydedin ve `IMPORT` denetim olay?n? do?rulay?n.
5. Envanter incelemesi i?in Sertifikalar ekran?n?, VaultPilot HTTPS paketi i?in Sunucu ayarlar?n? kullan?n; bu ekran da??t?m yapmaz.

### Dosya saklama

1. Kullan?c? ve kasa ba??na kullan?labilir kotay? do?rulay?n; 1 GB'yi a?mayan bir dosya se?in.
2. Otomatik ?nerilen ba?l???, dosya ad?n?, boyutu, par?a say?s?n? ve hedef kasay? inceleyin.
3. Kaydedin; ?zet alma, ?ifreleme ve y?kleme tamamlan?rken sayfay? a??k tutun.
4. Y?klemeyi tamamlanm?? saymadan ?nce Dosyalar ekran?n? a??n ve kayd?n geri al?nabildi?ini do?rulay?n.
5. Hata olu?tuysa yeniden denemeden ?nce Dosyalar ve Denetim G?nl???nde olu?turulmu? kay?t veya k?smi par?a durumu bulunup bulunmad???n? inceleyin.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Yeni taslak | T?r? se?ip zorunlu alanlar? tamamlay?n; hen?z hi?bir ?ey kal?c? de?ildir. |
| Kilidi a??k aktif kasa yok | Materyal girmeden veya kaydetmeden ?nce hedef kasay? se?ip kilidini a??n. |
| Viewer / Auditor | Se?ici veya d?zenleyici a??labilir ancak Kaydet devre d???d?r ve sunucu yazmay? korur. Editor veya Manager kasa yetkisine sahip bir Owner, Admin ya da User hesab? kullan?n. |
| Salt okunur lisans | G?r?nt?leme s?rebilir ancak Kaydet kapal? kal?r. |
| T?r de?i?tirildi | Sertifika, dosya veya etiket i?lemi sonras?nda s?f?rlay?p yeniden a?may? tercih edin; aksi durumda ortak ve gizli verinin tamam?n? yeniden kontrol edin. |
| Ba?l?k veya de?er eksik | Se?ili t?r?n kesin zorunlu alanlar?n? tamamlay?n. |
| Sertifika i?e aktar?l?yor | Taray?c?n?n okuma ve ?zet alma i?lemini bekleyin; hen?z kaydedilmi? kay?t de?ildir. |
| Sertifika b?y?k / okunam?yor | ?nceki materyal veya bilgiler kalabilir. S?f?rlay?p yeniden a??n; ard?ndan 10 MB s?n?r?ndaki onayl? dosyay? se?in veya do?rulanm?? metni yap??t?r?n. |
| Dosya se?ilmedi | Yeni Dosya kayd?n? kaydetmeden ?nce tek dosya se?in. |
| Dosya b?y?k / kota a??ld? | ?nceki dosya bilgisi kalabilir. S?f?rlay?p yeniden a??n; ard?ndan aktif kasadaki kullan?c? toplam?n? 1 GB i?inde tutan dosyay? se?in. |
| ?ifreleniyor / y?kleniyor | Sayfay? a??k tutun; devam eden i?lem i?in iptal denetimi yoktur ve gezinme i?i durdurmaz. |
| Kaydetme ba?ar?l? | Hedef listeyi ve `CREATE` ya da `IMPORT` denetim kan?t?n? do?rulay?n. |
| Kaydetme ba?ar?s?z | Gizli ayr?nt?lar? koruyun, formu d?zeltin ve Dosya kayd? veya k?smi par?alar?n olu?up olu?mad???n? kontrol edin. |

## ??lemden ?nce

- Aktif kasay? do?rulay?n; bu ekranda kasa se?ici yoktur.
- Yazmaya a??k lisans? ve o kasadaki Editor ya da Manager eri?imini do?rulay?n.
- Yeni RDP/SSH kimlik bilgisi kay?tlar? i?in Yeni kay?t yerine Active Directory e?itlemesini kullan?n.
- Hassas materyal girmeden ?nce t?r? se?in. Sertifika, dosya veya etiket i?leminden sonra t?r de?i?tiyse s?f?rlay?p yeniden a??n; aksi durumda gizli ortak durumu yeniden kontrol edin.
- Sertifika ve dosyalarda kaynak yetkisini, s?n?fland?rmay?, saklama s?resini, boyutu ve hedefi do?rulay?n.
- ?retme, s?z?nt? kontrol?, sertifika i?e aktarma ve sertifika yetkilisi se?iminin hi?bir ?eyi kaydetmedi?ini veya da??tmad???n? unutmay?n. Son de?er de?i?ikli?inden sonra, Kaydet'e basmadan hemen ?nce s?z?nt? kontrol?n? yeniden ?al??t?r?n.

## G?venli Kan?t

- Payla??labilir: se?ili elle kay?t t?r?, genel do?rulama durumu, boyut aral???, par?a say?s?, genel denetim eylemi ve yer tutuculu alan haritas?.
- Gizli kalmal?: ba?l?k, hesap, adres, not, sahip/ekip ba?lam?, sertifika konusu/yay?nc?s?/seri numaras?/?zeti, dosya ad?, kesin boyut ve i? sistem ya da talep bilgisi.
- Asla payla?may?n: parolalar, API anahtarlar?, tokenlar, sertifika veya ?zel anahtar materyali, PFX/P12 i?eri?i ya da parolas?, dosya i?eri?i, ?ifreli y?kler, kasa anahtarlar? veya formun tam ekran g?r?nt?s?.
- Ger?ek bir de?er herkese a??k kan?ta girdiyse a???a ??km?? kabul edin; ilgili sistem ?zerinden d?nd?r?n veya iptal edin.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Aktif kasa belirsizse, yazma eri?imi beklenmedikse, sertifika veya dosyan?n kayna?? bilinmiyorsa, ?zel anahtar?n a???a ??kt???ndan ??pheleniliyorsa, y?kleme k?smen ilerledikten sonra ba?ar?s?z oluyorsa, kota durumu aray?zle ?eli?iyorsa ya da denetim ve liste sonu?lar? uyu?muyorsa durun. Gizli materyal eklemeden kay?t t?r?n?, genel boyutu, genel hata kodunu, yakla??k zaman aral???n? ve son g?venli ad?m? i?eren ?zel destek kayd? a??n.

## Operat?r Notlar?

Yeni kay?t, istemci taraf?nda ?ifreleme yapan bir formdur; i? ak??? motoru de?ildir. Otomatik kaydetmez, sayfa yenilemeleri aras?nda taslak tutmaz, kimlik bilgilerini s?namaz, Active Directory kay?tlar?n? elle olu?turmaz, sertifika g?venini do?rulamaz, sertifika da??tmaz, dosya taramaz veya d?? sistemlerde rotasyon yapmaz.

## ?lgili

- [Parolalar ekran?](screen-passwords.md)
- [API anahtarlar? ekran?](screen-api-keys.md)
- [G?venli notlar ekran?](screen-secure-notes.md)
- [Sertifikalar ekran?](screen-certificates.md)
- [Dosyalar ekran?](screen-files.md)
- [Active Directory kay?tlar? ekran?](screen-active-directory-records.md)
- [Denetim G?nl??? ekran?](screen-audit-log.md)
