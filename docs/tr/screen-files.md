# Dosyalar Ekran?

?st ?ubuktaki `?` bu rehberi **Dosyalar** ekran?ndan a?ar. Bu ekran, etkin kasadaki `FILE` t?r? kay?tlar? y?netir; genel ama?l? bir belge ar?ivi, a? payla??m? veya bulut depolama istemcisi de?ildir.

## Eri?im ve Lisans S?n?r?

Dosyalar ekran?, Denet?i d???ndaki sistem rollerine yaln?zca kendilerine atanm?? ve taray?c? oturumunda kilidi a??lm?? kasalar i?in g?r?n?r. **G?r?nt?leyici**, **D?zenleyici** ve **Y?netici** kasa rolleri dosya kay?tlar?n? listeleyebilir ve indirebilir. Denet?i rol?n?n gizli kay?tlara veya kasa anahtar?na eri?imi yoktur.

Yeni dosya olu?turma, dosya de?i?tirme, kopya olu?turma, kay?t bilgilerini d?zenleme ve silme i?in yaz?labilir lisans ile etkin kasada **D?zenleyici** veya **Y?netici** rol? gerekir. G?r?nt?leyici rol? ve salt okunur lisans bu yazma i?lemlerini kapat?r; mevcut bir dosyay? indirme yolunu kapatmaz. Dosyalar ekran?n?n ayr? bir lisans mod?l? yoktur. **Toplu payla?** ile a??lan payla??m ak???nda ise lisans?n **Payla??m** yetene?i ve Payla??m ekran?n?n daha dar rol ko?ullar? ayr?ca uygulan?r.

## Burada Ne Yap?l?r

- **Dosyalarda ara** ile etkin kasan?n dosya kay?tlar?nda aray?n.
- **Ak?ll? filtre ekle** ile i?e aktar?lan, uyar? ta??yan, kategori, etiket veya ?r?n bilgisi e?le?en kay?tlar? birlikte s?z?n.
- **T?m?** h?zl? filtresine d?n?n; **Kart** veya **Tablo** g?r?n?m?n? se?in ve **Yenile** ile kasa listesini yeniden al?n.
- Yazma yetkiniz varsa **Yeni dosya** ile ?ifreli dosya kayd? olu?turun.
- Sat?rda dosya ad?, boyut, par?a say?s?, k?salt?lm?? SHA-256 ?zeti ve son g?ncelleme zaman?n? inceleyin.
- **Dosyay? indir** ile par?alar? taray?c?da ??z?p dosyay? indirin.
- **VirusTotal SHA-256 aramas?** ile yaln?z dosya ?zetini VirusTotal ?zerinde aray?n.
- **Di?er i?lemler** i?inden **Kopyas?n? olu?tur**, **Kayd? d?zenle** veya **Kayd? sil** i?lemini ba?lat?n.
- Sat?rlar? se?ip **Toplu i?lemler** men?s?nden dosya kay?tlar?na uygulanabilen i?lemleri y?r?t?n.

## Dosya Boyutu, Par?alar ve ?ifreleme S?n?r?

Se?ilen tek dosya 1 GB'? a?amaz. Sunucu ayr?ca ge?erli kullan?c?n?n etkin kasaya yazd??? ?ifreli dosya par?alar?n?n toplam?n? kullan?c? ve kasa ba??na 1 GB ile s?n?rlar; bu nedenle 1 GB'tan k???k bir dosya da kullan?labilir alan yetersizse reddedilebilir. Dosyalar ekran? tam olarak ne kadar alan kald???n? g?stermez; s?n?r, par?alar yaz?l?rken sunucu taraf?ndan uygulan?r.

VaultPilot dosyay? 2 MB'l?k en fazla 512 par?a halinde i?ler. Kaydetme s?ras?nda SHA-256 ?zeti taray?c?da hesaplan?r; dosya her par?a i?in etkin kasa anahtar?yla taray?c?da ?ifrelenir. Sunucu ?ifreli par?alar?, par?a s?ras?n? ve kota i?in gereken boyut bilgisini saklar. Dosya i?eri?ini ayr? bir bulut nesne deposuna y?klemez ve sunucu taraf?nda d?z metin dosya olarak tutmaz.

Dosya sat?r?ndaki par?a say?s? ve boyut, kay?t meta verisidir. K?salt?lm?? SHA-256 de?eri dosyan?n kimli?ini do?rulamaya yard?mc? olur; gizli dosya i?eri?inin g?venli bi?imde payla??labilece?i anlam?na gelmez.

## Yeni Dosya Olu?turma

1. Yaz?labilir ve do?ru kasan?n etkin oldu?unu do?rulay?n.
2. **Yeni dosya** d??mesini se?in.
3. Zorunlu **Ba?l?k** alan?n? doldurun.
4. ?ste?e ba?l? olarak **Sahip veya teslim alan**, **?lgili sistem veya talep kayd?** ve **Dosya notu** alanlar?n? doldurun.
5. **Dosya se?** ile tek dosyay? se?in. Ekran dosya ad?n?, boyutu ve hesaplanacak par?a say?s?n? g?sterir; ba?l?k bo?sa dosya ad?n? ba?l?k olarak kullan?r.
6. **?ifreli kayd? kaydet** ile i?lemi ba?lat?n. ?lerleme alan? ?nce ?ifreli kay?t verisinin kayd?n?, ard?ndan dosya par?alar?n?n ?ifrelenip y?klendi?ini g?sterir.
7. ??lem tamamlan?nca Dosyalar listesinde dosya ad?n?, boyutu, par?a say?s?n? ve SHA-256 ?zetini do?rulay?n.

Dosya se?imi zorunludur. 1 GB s?n?r? a??l?rsa se?im temizlenir. Kasa kilitli, rol yetersiz, lisans salt okunur veya kullan?c?/kasa kotas? doluysa kay?t tamamlanmaz.

## D?zenleme, De?i?tirme, Kopyalama ve Silme

**Kayd? d?zenle**, mevcut ba?l?k, sahip, ilgili sistem ve not bilgilerini a?ar. Dosyay? de?i?tirmek zorunlu de?ildir. **Dosyay? de?i?tir** ile yeni bir dosya se?erseniz kay?t meta verisi yeniden ?ifrelenir, eski par?alar temizlenir ve yeni dosya 2 MB'l?k par?alar halinde y?klenir. Kaydetme s?ras?nda sayfadan ayr?lmay?n.

**Kopyas?n? olu?tur** bir pano i?lemi de?ildir. VaultPilot kaynak par?alar? etkin kasa anahtar?yla taray?c?da ??zer, yeni kay?t i?in yeniden ?ifreler ve ayn? kasada ayr? bir dosya kayd? olu?turur. Kaynak par?alar eksikse kopya olu?turulmaz; eksik haz?rlanm?? yeni kopya kayd? temizlenmeye ?al???l?r.

**Kayd? sil**, onaydan sonra dosya kayd?n? ve ona ba?l? ?ifreli par?alar? sunucu kasas?ndan kal?c? olarak kald?r?r. ??lem geri al?namaz. Toplu silme de ayr? onay ister; i?lem k?smen ba?ar?s?z olursa listedeki kalan kay?tlar? yenileyip yeniden de?erlendirin.

## ?ndirme, G?sterme, Kopyalama ve Denetim Davran???

Dosya sat?r?nda **Gizli de?eri g?ster** veya **Gizli de?eri kopyala** i?lemi yoktur. Dosya i?eri?i sat?rda ya da panoda a??lmaz. **Dosyay? indir**, sunucudan ?ifreli par?alar? s?ras?yla al?r, beklenen par?a say?s?n? do?rular, par?alar? etkin kasa anahtar?yla taray?c?da ??zer ve taray?c?n?n indirme ak???na verir. ?ndirme i?in kasan?n kilidi a??k olmal?d?r.

Sunucu, dosya par?a listesini ba?ar?yla d?nd?rd???nde; aray?z beklenen par?a say?s?n? do?rulamadan, par?alar? ??zmeden veya taray?c? indirmesini ba?latmadan ?nce `EXPORT` denetim olay?n? yazar. Bu nedenle par?alar eksik oldu?unda, taray?c?da ??zme veya indirme ba?ar?s?z oldu?unda ya da **Kopyas?n? olu?tur** ?n kontrol? kaynak par?alar? listeledikten sonra durdu?unda da `EXPORT` g?r?lebilir. Payla??m haz?rl??? da kaynak par?a listesini ald??? i?in paket daha sonra ba?ar?s?z olsa bile ayn? olay olu?abilir.

**VirusTotal SHA-256 aramas?** dosyay? y?klemez; `https://www.virustotal.com/gui/file/{sha256}` adresini yeni sekmede a?ar ve `VIEW` denetim olay? yazmay? dener. Bu i?lem SHA-256 ?zetini ???nc? taraf bir hizmete ta??r; kurum politikas? izin vermiyorsa kullanmay?n.

Yeni dosya kayd? normalde iki denetim kan?t? ?retir: kay?t olu?turma `IMPORT`, par?a y?klemeden ?nce mevcut par?a k?mesini temizleme `EDIT`. Dosya de?i?tirme, kay?t g?ncellemesi i?in bir `EDIT` ve eski par?alar? temizleme i?in ikinci bir `EDIT` ?retebilir. Silme `DELETE` olarak kaydedilir. Kopya ?n kontrol?nde kaynak par?alar?n listelenmesi `EXPORT`; yeni kopya kayd?n?n ve par?alar?n?n yaz?lmas? ise `IMPORT` ile `EDIT` ?retir. Dosya ad?n? veya ekrandaki meta veriyi i?letim sistemi yoluyla kopyalamak i?in ayr? bir VaultPilot denetim olay? yoktur.

## Payla??m ve Toplu ??lemler

Yaz?labilir kasada **T?m?n? se?**, yaln?z ge?erli arama ve filtrede g?r?nen dosya kay?tlar?n? se?er. G?r?n?r kay?tlar?n t?m? se?ildi?inde d??me **Se?imi temizle** olur ve se?imi kald?r?r. G?r?nt?leyici veya salt okunur modda dosya kay?tlar? toplu g?r?n?r se?im k?mesinden ??kar?ld??? i?in bu d??me devre d???d?r; sat?r onay kutular? yine g?r?n?r ve dosyalar tek tek se?ilebilir. Bu modda se?imi kald?rmak i?in sat?r kutular?n? tek tek temizleyin.

Dosya ekran?nda kullan?labilen toplu men? ?unlar? i?erebilir:

- **Se?ilenleri d??a aktar** hassas onaydan sonra kay?t verilerini JSON dosyas?na yazar ve her kay?t i?in `EXPORT` olay? olu?turur. Dosya kayd? i?in bu ??kt? ba?l?k, not ve dosya meta verisini ta??r; ?ifreli dosya par?alar?n?n veya indirilebilir dosya i?eri?inin yerine ge?mez.
- **Kategori ata**, **Etiket ata**, **Ar?ivle**, **Pasifle?tir / iptal et**, **Toplu not ekle**, **Se?iliyi d?zenle** ve **Onayla ve kald?r** yaz?labilir kasa ister.
- **Denetim raporuna ekle** CSV'ye yaln?z genel kay?t alanlar?n? yazar: ba?l?k, t?r, kaynak, durum, risk, sahip, kategori, etiketler, g?ncelleme zaman? ve dosya kay?tlar?nda bo? kalan dizin alanlar?. Dosya ad?, boyut, par?a say?s?, SHA-256 ?zeti ve dosya i?eri?i rapora eklenmez.
- **G?venlik kontrol? ba?lat** dosya i?in antivir?s veya zararl? yaz?l?m taramas? de?ildir; dosya kayd?nda kopyalanabilir gizli de?er bulunmad??? i?in ikili dosya i?eri?ini taramaz.
- **Excel'den i?eri aktar** genel kay?t ?ablonu ak???d?r; birden ?ok ikili dosyay? y?kleyen dosya aktar?m arac? de?ildir. ?ifreli ek olu?turmak i?in **Yeni dosya** ak???n? kullan?n.
- **Toplu payla?**, se?ili kay?tlar? **Payla??m** ekran?na ta??r. Burada al?c?, s?re ve kullan?m s?n?r? ayr?ca do?rulanmadan paket g?nderilmez.

Dahili payla??m i?in etkin kasada **Y?netici** rol?, kullan?c? y?netimi yetkisi ve yaz?labilir lisans gerekir. Dahili pakette se?ili dosyalar?n toplam? 1 GB'? ve toplam par?a say?s? 512'yi a?amaz. D?? payla??m paketi i?in etkin kasada **Y?netici** rol? ve yaz?labilir lisans gerekir; d?? pakette ayr?ca toplam par?a tavan? yoktur, ancak paket toplam? 1 GB ve her kaynak dosya en fazla 1 GB/512 par?a s?n?r?nda kal?r. Her iki y?ntemde de dosya par?alar? taray?c?da a??l?r ve payla??m anahtar?yla yeniden ?ifrelenir; bu i?lem orijinal kasa kayd?n? herkese a??k yapmaz.

## ?nerilen ?? Ak??lar?

### Yeni ?ifreli dosya ekleme

1. Do?ru kasay? ve D?zenleyici/Y?netici rol?n? do?rulay?n.
2. Dosyan?n boyutunu, sahibini ve saklama gerek?esini kontrol edin. Ekran tam kalan alan? g?stermedi?i i?in 1 GB kullan?c?/kasa s?n?r?nda pay b?rak?n.
3. **Yeni dosya** ile kayd? haz?rlay?n ve kaydetme ilerlemesi bitene kadar bekleyin.
4. Listede ad, boyut, par?a say?s? ve SHA-256 de?erini do?rulay?n.
5. Denetim Kayd?'nda normal dosya olu?turma ak???n?n `IMPORT` ve par?a temizleme `EDIT` olaylar?n? kontrol edin.

### Dosyay? g?venli indirme

1. Dosya ad?n?, boyutunu ve k?salt?lm?? SHA-256 de?erini beklenen kay?tla e?le?tirin.
2. **Dosyay? indir** se?ene?ini kullan?n.
3. Par?a eksikli?i uyar?s? yoksa indirilen dosyay? kurumun onayl? konumuna ta??y?n.
4. Gerekirse yerel SHA-256 de?erini kay?tla kar??la?t?r?n ve `EXPORT` denetim olay?n? do?rulay?n. Bu olay par?alar?n listelendi?ini kan?tlar; taray?c? indirmesinin tamamland???n? tek ba??na kan?tlamaz.

### Dosyay? de?i?tirme

1. **Kayd? d?zenle** ile do?ru kayd? a??n.
2. **Dosyay? de?i?tir** ile yeni dosyay? se?ip boyut, par?a say?s? ve ad? kontrol edin.
3. ?ifreli g?ncellemeyi kaydedin; i?lem bitmeden sekmeyi kapatmay?n.
4. ?ndirme testi ve Denetim Kayd?'ndaki iki olas? `EDIT` olay?yla yeni par?alar? do?rulay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Dosyalar y?kleniyor | ?skelet sat?rlar bitene kadar olu?turma, toplu i?lem veya indirme ba?latmay?n. |
| Bu kasada kay?t yok | Yazma yetkiniz varsa **Yeni dosya** kullan?n; dosyan?n bu kasaya ait oldu?undan emin olun. |
| Arama veya filtre sonucu yok | Arama ifadesini de?i?tirin, etkin ak?ll? filtreleri temizleyin veya **T?m?** se?ene?ine d?n?n. |
| G?r?nt?leyici / salt okunur | ?ndirme kullan?labilir; olu?turma, de?i?tirme, kopya, d?zenleme, silme ve payla??m olu?turma kapal?d?r. **T?m?n? se?** devre d???d?r; sat?r kutular? tek tek kullan?labilir. |
| Dosya se?ilmedi | Yeni kay?tta **Dosya se?** ile tek dosya se?meden kaydetmeyin. |
| 1 GB s?n?r? veya kota a??ld? | Dosya boyutunu veya kullan?c?/kasa kullan?m?n? azalt?n. Ekran tam kalan alan? g?stermez; s?n?r? sunucu uygular. |
| Dosya ?ifrelenip y?kleniyor | ?lerleme tamamlanana kadar sayfay? yenilemeyin veya sekmeyi kapatmay?n. |
| Dosya par?alar? eksik | Kasay? yenileyin; sorun s?rerse kayd? d?zenleyip dosyay? yeniden ekleyin. Eksik kayd? payla?may?n veya kopyalamay?n. |
| Dosya indirilemedi | Kasan?n a??k oldu?unu, eri?im rol?n? ve par?a b?t?nl???n? kontrol edip bir kez yenileyin. |
| Toplu i?lemde kay?t se?ilmedi | ?nce g?r?n?r dosya kay?tlar?ndan en az birini se?in. |
| Payla??m dosya eklerini haz?rl?yor | Par?alar tamamlanmadan paketi indirmeyin, kopyalamay?n veya al?c?ya g?ndermeyin. |

## ??lemden ?nce

- Do?ru sunucu profili, kasa ve dosya kayd?nda oldu?unuzu do?rulay?n.
- Olu?turma/de?i?tirme i?in etkin kasa rol?n?n D?zenleyici veya Y?netici ve lisans?n yaz?labilir oldu?unu kontrol edin.
- Dosya sahibini, saklama ve imha beklentisini, ilgili talep kayd?n? ve dosya ad?n? do?rulay?n.
- Boyutun 1 GB'? a?mad???n? kontrol edin. Tam kalan alan ekranda g?sterilmedi?inden kullan?c?/kasa s?n?r?nda g?venli pay b?rak?n; son karar? sunucu verir.
- Log, veritaban? d?k?m?, ?zel anahtar, sertifika paketi veya ekran g?r?nt?s?n? dosya kasas?na koymadan ?nce veri s?n?fland?rma ve saklama politikas?n? uygulay?n.
- ?ndirme hedefinin, payla??m al?c?s?n?n ve VirusTotal gibi ???nc? taraf ?zet aramas?n?n kurum politikas?na uygun oldu?unu do?rulay?n.
- De?i?tirme veya silme ?ncesi geri d?n?? i?in gerekli onayl? yede?in bulundu?unu do?rulay?n.

## G?venli Kan?t

- Payla??labilir: ekran durumu, genel hata s?n?f?, yuvarlanm?? boyut aral???, par?a say?s?, rol/lisans modu ve gizli bilgi i?ermeyen i?lem zaman?.
- Gizli kalmal?: dosya i?eri?i, tam dosya ad?, tam SHA-256 ?zeti, kay?t kimli?i, sahip/al?c?, i? sistem veya talep kayd? adresi, kasa ad?, not, m??teri ba?lam? ve indirilen yerel yol.
- `IMPORT`, `EDIT`, `EXPORT`, `VIEW` veya `DELETE` olay?n? kan?t olarak g?nderirken kullan?c?y?, hedef kimli?ini, zaman ili?kisini ve b?t?nl?k ?zetini uygun ?ekilde maskeleyin.
- Ham g?nl?k kay?tlar?n?, veritaban? d?k?mlerini, ?zel anahtarlar?, imzalama materyalini, kurulum paketlerini, yay?n ar?ivlerini veya redakte edilmemi? ekran g?r?nt?lerini herkese a??k destek kanal?na y?klemeyin.
- Dosya ?zeti ???nc? taraf aramas?na g?nderildiyse bunu kan?t paketinde belirtin; dosyan?n kendisinin g?nderildi?ini varsaymay?n.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Beklenen dosya ad?, boyutu veya SHA-256 ?zeti de?i?tiyse; par?a say?s? eksik kal?yorsa; ?ifreleme/y?kleme ilerlemesi tamamlanm?yorsa; silinen kay?t geri g?r?n?yorsa; kullan?c?/kasa s?n?r? beklenmedik bi?imde doluysa; denetim olay? olu?muyorsa; yanl?? dosya indirildi, kopyaland? veya payla??ma eklendiyse i?lemi durdurun. Dosya i?eri?ini eklemeden; ekran durumu, redakte kay?t kimli?i, genel boyut, par?a say?s?, son g?venli ad?m, zaman ve hata metniyle ?zel destek kayd? a??n.

## Operat?r Notlar?

Dosyalar ekran? dosya i?eri?ini otomatik olarak s?n?fland?rmaz, zararl? yaz?l?m taramas? yapmaz veya saklama s?resi dolunca kendili?inden silmez. **VirusTotal SHA-256 aramas?** yaln?z harici bir ?zet sorgusudur. Veri sahibi, saklama politikas?, g?venli indirme hedefi ve gerekti?inde kal?c? silme operat?r sorumlulu?undad?r.

## ?lgili

- [Yeni kay?t ekran?](screen-new-item.md)
- [Payla??m ekran?](screen-sharing.md)
- [Denetim Kayd? ekran?](screen-audit-log.md)
- [Yedekleme ve geri y?kleme](backups-and-restore.md)
- [Herkese a??k depo s?n?r?](public-repository-boundary.md)
- [Destek kan?t paketi](support-evidence-pack.md)
