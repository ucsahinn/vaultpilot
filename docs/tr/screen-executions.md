# ??lemler Ekran?

?st ?ubuktaki `?`, ??lemler ekran?na ait bu rehberi a?ar. Bu ekran; g?ncelleme i?leri, AD ajan i?lemleri ve se?ili kal?c? denetim olaylar?n? tek bir zaman s?ral? g?r?n?mde birle?tirir. Bir g?revi ba?latma veya genel ama?l? yeniden deneme ekran? de?ildir.

## Eri?im, Rol ve Lisans S?n?r?

Sahip, Y?netici ve Denet?i sistem rolleri ??lemler ekran?n? a?abilir. Kullan?c? rol? sistem g?r?n?m?ne eri?emez. Ekran? kullanmak i?in kasa kilidinin a??lm?? ve sunucu oturumunun do?rulanm?? olmas? gerekir.

G?r?nt?leme ayr? bir lisans ?zelli?ine ba?l? de?ildir; salt okunur lisans mevcut kay?tlar? g?rmeyi tek ba??na engellemez. Yaln?z **Sahip**, uygun bir AD ajan i?leminde **??lemi durdur** se?ene?ini g?r?r. Durdurma sunucuda yazma say?ld??? i?in salt okunur lisans bu iste?i reddeder. **Kayna?? a?** ile gidilen G?ncelleme Merkezi veya Entegrasyonlar gibi ekranlarda ayr?ca rol ve ilgili lisans ?zelli?i denetlenebilir.

## Burada Ne Yap?l?r

- Y?klenen i?lemleri kategori ve durum grubuna g?re daralt?n.
- ??lem ?zetini, durumunu, ilerleme oran?n?, kayna??n?, hedefini, akt?r?n? ve son g?ncelleme zaman?n? okuyun.
- Varsa ad?mlar? ve s?n?rl? log ?zetini a?arak sorunun hangi a?amada oldu?unu belirleyin.
- **Yenile** ile anl?k g?r?n?m? tekrar al?n; ekran a??kken liste yakla??k 2,5 saniyede bir kendili?inden de yenilenir.
- **Kayna?? a?** ile G?ncelleme Merkezi, Entegrasyonlar veya Denetim Ge?mi?i ba?lam?na ge?in.
- Yaln?z bekleyen veya ajan taraf?ndan al?nm?? AD ajan i?lemini, Sahip rol?yle ve onay vererek durdurun.

Bu ekranda genel **Yeniden dene** d??mesi yoktur. G?ncelleme, Discovery, bak?m veya ba?ar?s?z AD i?lemini buradan yeniden ba?latmay?n; ?nce kayna?? ve kan?t? inceleyin, ard?ndan yaln?z ilgili kaynak ekran? b?yle bir i?lem sunuyorsa oradan yeni bir ?al??ma ba?lat?n.

## Veri Kaynaklar? ve Kapsam

Sunucu en fazla 80 kayd? son g?ncellenen ?nce olacak ?ekilde birle?tirir:

| Kaynak | Ekrandaki kaynak etiketi | Ne g?sterir | **Kayna?? a?** hedefi |
| --- | --- | --- | --- |
| G?ncelleme i?i | `Update job` | Sunucu veya taray?c? eklentisi g?ncellemesinin canl? durum, ad?m ve mesajlar?n? | G?ncelleme Merkezi |
| Dizin ajan i?lemi | `AD ajan i?lemi` | Bekleyen, ajan taraf?ndan al?nan veya tamamlanan AD eylemini | Entegrasyonlar |
| Denetim olay? | `Denetim olay?` | Payla??m, g?venlik, Discovery, kasa, entegrasyon ve sistem i?lemlerinin kal?c? kayd?n? | Denetim Ge?mi?i |

Discovery taramas?n?n canl? i?i bu listeye ayr? bir Discovery ?al??ma kayd? olarak eklenmez. Politika kaydetme, tarama ba?latma, bulgu bast?rma, i?e aktar?m haz?rlama/tamamlama ve iyile?tirme tamamlama gibi se?ili Discovery olaylar? **Kaydedildi** durumunda denetim kayd? olarak g?r?n?r. Canl? ilerleme, iptal ve tamamlanm?? ?al??ma y?netimi i?in Discovery ekran?n? kullan?n.

Sunucu ayar? kaydetme, yeniden ba?latma ve bak?m temizli?i gibi izlenen bak?m olaylar? da **Sistem** kategorisinde kal?c? denetim kayd? olabilir. ??lem kay?tlar?n? yedekleyip temizleme veya geri y?kleme bu ekranda yap?lmaz; **Sunucu ayarlar? > Operasyonlar** kullan?l?r. Bak?m temizli?i tamamlanm?? g?ncelleme ve dizin i?lem kay?tlar?n? kald?rabilir, aktif i?lemleri korur ve kendi bak?m denetim kayd?n? ?retir.

## Filtreler

Kategori ve durum filtreleri sat?rlar? birlikte daralt?r. Ancak d??melerdeki say?lar kesi?imi g?stermez: kategori say?lar? se?ili durum filtresinden ba??ms?z, durum say?lar? da se?ili kategori filtresinden ba??ms?z olarak y?klenmi? anl?k g?r?n?m?n tamam?ndan hesaplan?r.

| Kategori | ??erik |
| --- | --- |
| **T?m?** | Y?klenen b?t?n kaynaklar. |
| **G?ncelleme** | Canl? g?ncelleme i?leri ile g?ncelleme denetim olaylar?. |
| **Dizin ajan?** | Canl? AD ajan i?lemleri ve bunlar?n se?ili denetim kay?tlar?. |
| **Payla??m** | Payla?ma ve payla??m? geri ?ekme denetim olaylar?. |
| **G?venlik** | Kullan?c?/oturum/2FA ve Discovery g?venlik olaylar?. |
| **Entegrasyon** | Dizin, entegrasyon ve eklenti denetim olaylar?. |
| **Kasa** | Silme, d??a/i?e aktarma ve tamamlanan Discovery i?e aktar?m? gibi kasa olaylar?. |
| **Sistem** | Bak?m, yeniden ba?latma, lisans ve di?er sistem denetim olaylar?. |

| Durum filtresi | Dahil etti?i sat?r durumlar? |
| --- | --- |
| **T?m durumlar** | B?t?n durumlar. |
| **Aktif** | **Bekliyor** ve **?al???yor**. |
| **Sorunlu** | **Ba?ar?s?z**, **Engellendi** ve **?nceleme**. |
| **Tamamlanan** | **Ba?ar?l?**, **Kaydedildi** ve **?ptal**. |

**?ptal** sat?rlar?n?n **Tamamlanan** filtresinde bulunmas?, ba?ar?l? olduklar? anlam?na gelmez; yaln?z art?k aktif olmad?klar?n? g?sterir. Filtrelenmi? g?r?n?mde sat?r yoksa **Bu filtrede i?lem kayd? yok** g?sterilir. Bu mesaj, ba?ka bir filtrede veya 80 kay?tl?k g?r?n?m s?n?r?n?n d???nda kay?t bulunmad???n? kan?tlamaz.

## Sat?r, Ad?m ve Log Ayr?nt?lar?

Her kartta i?lem ad?, ?zet, durum rozeti ve y?zde ilerleme bulunur. Meta sat?r? kaynak, hedef, akt?r ve **G?ncellendi** zaman?n? g?sterir. Kaynakta bulunmayan hedef veya akt?r `-` olarak g?r?n?r.

Kart, varsa ilk be? ad?m? g?sterir. Her ad?mda etiket, ayr?nt? veya genel durum kar??l??? ve y?zde bulunur. Ad?m durumlar? `PENDING`, `RUNNING`, `DONE`, `BLOCKED` veya `FAILED` olabilir. Daha fazla ad?m varsa bu ekranda g?sterilmez.

**Loglar** b?l?m? varsa ilk alt? kay?t g?r?n?r. Her kay?tta seviye (**Bilgi**, **Ba?ar?l?**, **Uyar?**, **Hata**), mesaj, zaman ve varsa teknik ayr?nt? yer al?r. Log b?l?m? **?al???yor**, **Ba?ar?s?z** ve **Engellendi** sat?rlar?nda varsay?lan olarak a??kt?r; di?er durumlarda elle a??l?r. Bu ?zet tam sunucu logu veya teslim/?al??t?rma makbuzu de?ildir.

Kart, i?lem kimli?ini, ba?lang?? zaman?n? veya tamamlanma zaman?n? ayr? alan olarak g?stermez. Destek kan?t?nda g?r?nmeyen bir i?lem kimli?i bulundu?unu varsaymay?n; kimli?i ancak g?venilir ?zel kaynak kan?t?nda ger?ekten mevcutsa kullan?n.

## Durumlar?n Anlam?

| G?r?nen durum | Kaynak durumu ve yorum |
| --- | --- |
| **Bekliyor** | Kuyru?a al?nm?? veya haz?r g?ncelleme i?i ya da bekleyen AD ajan i?lemi. Hen?z ajan/i??i taraf?ndan y?r?t?l?yor saymay?n. |
| **?al???yor** | G?ncelleme ?al???yor veya AD ajan? i?lemi y?r?tmek ?zere teslim alm??. ?lerleme y?zdesi tek ba??na canl?l?k kan?t? de?ildir; g?ncellenme zaman?n? da izleyin. |
| **Ba?ar?l?** | G?ncelleme tamamlanm?? ya da AD ajan i?lemi ba?ar?yla sonu?lanm??. Kaynak ekran?ndaki sonucu ayr?ca do?rulay?n. |
| **Ba?ar?s?z** | AD ajan i?lemi hata ile sonu?lanm??. Mesaj? ve redakte log ayr?nt?s?n? koruyun; bu ekranda yeniden deneme yoktur. |
| **Engellendi** | G?ncelleme i?i ilerleyememi?. Ad?m ve log ayr?nt?s?n? inceleyip G?ncelleme Merkezine ge?in. |
| **?ptal** | AD ajan i?lemi Sahip taraf?ndan durdurulmu?. Tamamlanm?? i?lem ve denetim kan?t? silinmez. |
| **?nceleme** | Dizin ajan?ndaki `STALE_REVIEW_REQUIRED` durumu. Ba?ar? veya s?radan kuyruk beklemesi saymay?n; ajan sa?l???n? ve hedef i?lemi inceleyin. |
| **Kaydedildi** | ?zlenen bir denetim olay? kal?c? olarak yaz?lm??. Bu, ili?kili d?? i?lemin ba?ar?l? teslim edildi?ini veya tamamland???n? tek ba??na kan?tlamaz. |

## Yenileme, Durdurma ve Yeniden Deneme

**Yenile**, yeni bir i?lem ba?latmadan yaln?z liste sorgusunu tekrarlar. Sorgu s?rerken d??me devre d??? kal?r ve **Yenileniyor** olarak i?aretlenir. Yetkili ve kilidi a??k oturumda ??lemler g?r?n?m? a??kken otomatik sorgu yakla??k 2,5 saniyede bir ?al???r.

**??lemi durdur** yaln?z kayna?? `AD ajan i?lemi` olan **Bekliyor** veya **?al???yor** sat?r?nda ve yaln?z Sahip i?in g?sterilir. Onaydan sonra bekleyen ya da ajan taraf?ndan al?nm?? eylem `CANCELLED` durumuna ge?irilir. Tamamlanm?? i?lemler ile denetim kay?tlar? silinmez. G?ncelleme i?leri ve denetim olay? sat?rlar? ??lemler ekran?ndan durdurulamaz.

Bu ekranda yeniden deneme yoktur. **Kayna?? a?**, i?lemi tekrar ?al??t?rmaz; yaln?z ilgili ?al??ma alan?na gider. ?zellikle **Kaydedildi** durumundaki Discovery veya bak?m kayd? canl? bir i?i iptal etme ya da yeniden ba?latma denetimi de?ildir.

## ?nerilen ?? Ak??lar?

### Sorunlu bir i?lemi inceleme

1. **Sorunlu** filtresini a??n ve ilgili kategoriyi se?in.
2. Durumun **Ba?ar?s?z**, **Engellendi** veya **?nceleme** oldu?unu ay?r?n.
3. Son g?ncelleme zaman?n?, ilerlemeyi, ad?mlar? ve ilk alt? log sat?r?n? inceleyin.
4. Akt?r, hedef, Dizin DN'si, host, dosya yolu ve hata ayr?nt?s?n? payla?madan ?nce redakte edin.
5. **Kayna?? a?** ile do?ru ?al??ma alan?na ge?in; kaynak ekranda yeni eylem ba?latmadan ?nce ayn? i?in h?l? aktif olmad???n? do?rulay?n.

### Aktif bir AD ajan i?lemini durdurma

1. **Dizin ajan?** ve **Aktif** filtrelerini se?in.
2. Hedefi, akt?r?, son g?ncelleme zaman?n? ve ajan sa?l???n? do?rulay?n.
3. ??lemin ger?ekten **Bekliyor** veya **?al???yor** oldu?unu ve yanl?? hedef se?ilmedi?ini kontrol edin.
4. Sahip rol?yle **??lemi durdur** se?ene?ini kullan?p onay? okuyun.
5. Liste yenilendi?inde **?ptal** durumunu ve ilgili denetim kan?t?n? do?rulay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | Be? sat?rl?k iskelet g?r?n?r; varsay?lan bo? g?r?n?m? kesin sonu? saymay?n. |
| Filtrede kay?t yok | Kategoriyi veya durum filtresini geni?letin; 80 kay?t s?n?r?n? ve kaynak ekran?n? ayr?ca kontrol edin. |
| Yenileniyor | Ayn? anda ikinci yenileme ba?latmay?n; mevcut sorgunun bitmesini bekleyin. |
| Liste yenilenemedi | Ekranda ayr? hata kart? olmayabilir. Oturum/kasa kilidi, rol ve sunucu ba?lant?s?n? do?rulay?p tekrar yenileyin; bo? g?r?n?m? kay?t yok kan?t? saymay?n. |
| Bekliyor | ??in kuyru?a al?nd???n? g?sterir; kaynak ekran?nda yinelenen ikinci i? ba?latmay?n. |
| ?al???yor | Son g?ncelleme zaman? ilerliyorsa bekleyin; sabitse kaynak ekran? ve servis/ajan sa?l???n? inceleyin. |
| Ba?ar?s?z | Redakte hata kan?t?n? koruyun; buradan yeniden deneyemezsiniz. |
| Engellendi | Engellenen ad?m? ve log ayr?nt?s?n? okuyup G?ncelleme Merkezine ge?in. |
| ?nceleme | Dizin ajan? eylemini ba?ar? saymay?n; ajan/ba?lant? ve hedef durumunu inceleyin. |
| Ba?ar?l? | Kaynak ekran?ndaki hedef sonucu do?rulay?n; y?zde 100 tek ba??na d?? etki kan?t? de?ildir. |
| Kaydedildi | Kal?c? denetim kayd? vard?r; ili?kili i?in canl? veya ba?ar?l? oldu?unu buradan ??karmay?n. |
| ?ptal | Eylem aktif de?ildir; kay?t **Tamamlanan** filtresinde kal?r ve denetim kan?t? korunur. |
| Durdurma g?r?nm?yor | Sat?r AD ajan i?lemi de?ildir, art?k aktif de?ildir veya rol Sahip de?ildir. Salt okunur lisansta d??me g?r?nebilir ancak sunucu iste?i reddeder; kontrol? a?maya ?al??may?n. |

## ??lemden ?nce

- Oturum rol?n? ve lisans?n yaz?labilir durumunu kontrol edin; g?r?nt?leme ile durdurma yetkisini birbirine kar??t?rmay?n.
- Kategori ile durum filtresini not edin; filtrelenmi? bo? g?r?n?m? tam ge?mi? olarak yorumlamay?n.
- Son g?ncelleme zaman?n?n de?i?ip de?i?medi?ini ve ayn? kaynakta mevcut aktif i? olup olmad???n? kontrol edin.
- Durdurma ?ncesinde hedef ve akt?r?n do?ru oldu?unu do?rulay?n; ajan taraf?ndan al?nm?? AD eyleminin etkisi ba?lam?? olabilir.
- G?ncelleme, Discovery ve bak?m kay?tlar?nda **Kaydedildi** ile ger?ek i? sonucu aras?ndaki fark? koruyun.
- ??lem kayd? bak?m temizli?i veya geri y?kleme kapsam?ndaysa ?nce ?zel kan?t? ve onayl? yedek ak???n? tamamlay?n.

## G?venli Kan?t

- Payla??labilir: kaynak ve kategori s?n?f?, g?r?nen durum, yakla??k ilerleme y?zdesi, geni? zaman aral???, redakte i?lem/ad?m ad?, log seviyesi ve genel hata kategorisi.
- Gizli kalmal?: akt?r/kullan?c? ad?, ger?ek hedef etiketi ve Dizin DN'si, host/domain, yerel yol, dosya/paket ad? ve konumu, tam log mesaj?/ayr?nt?s?, tam denetim karma de?eri, yedek dosya ad?/?zet de?eri ve makineye ?zg? iz.
- Ekran g?r?nt?s?nde kart ba?l???n?n g?venli oldu?unu varsaymay?n; ?zet, hedef, akt?r, ad?m ayr?nt?s? ve log sat?rlar?n? ayr? ayr? inceleyip maskeleyin.
- Destek i?in m?mk?nse kategori, durum, geni? zaman aral??? ve redakte hata kodunu payla??n. Ham logu veya Dizin hedefini yaln?z onayl? ?zel kanalda ve gerekli en dar kapsamla iletin.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

?al??an sat?r?n g?ncellenme zaman? ilerlemiyorsa, ayn? i?lem tekrar tekrar olu?uyorsa, **?nceleme** durumunun nedeni belirsizse, g?ncelleme **Engellendi** kal?yorsa, durdurulan AD eylemi hedefte etkisini s?rd?r?yorsa veya liste kaynak ekran?yla ?eli?iyorsa yeni g?rev ba?latmay? b?rak?n. Redakte kaynak, kategori, durum, geni? zaman aral???, son g?r?nen ad?m ve genel hata koduyla ?zel destek kayd? a??n.

## Operat?r Notlar?

??lemler, farkl? ya?am d?ng?lerini tek g?r?n?mde toplar; her sat?r ayn? t?rden bir ?al??ma de?ildir. **Kaydedildi** denetim olay?, **Ba?ar?l?** i? sonucu ve **?ptal** terminal durumu birbirinin yerine kullan?lamaz. Kartta g?sterilen ad?m ve log say?s? s?n?rl?d?r; g?r?nmeyen ayr?nt?y? yok saymay?n veya tahmin etmeyin.

## ?lgili

- [Operasyon runbook](operator-runbook.md)
- [G?ncelleme Merkezi](update-center.md)
- [Discovery ekran?](screen-discovery.md)
- [Entegrasyonlar ekran?](screen-integrations.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
- [Sunucu ayarlar? ekran?](screen-server-settings.md)
