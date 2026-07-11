# Rotasyon Ekran?

?st ?ubuktaki `?` simgesi Rotasyon ekran?na ait bu rehberi a?ar. Bu ekran; credential envanteri, denetim kay?tlar? ve Active Directory ajan i?lemlerinden ?retilen salt okunur bir ?nceliklendirme y?zeyidir. Rotasyon planlamaz, yeni parola ?retmez, hesab? de?i?tirmez ve gizli de?eri kendili?inden yenilemez.

## Veri Kayna??, Eri?im ve Lisans S?n?r?

Rotasyon SLA yaln?zca aktif kasadaki ?ifresi taray?c?da ??z?lebilen `CREDENTIAL` kay?tlar?n? kullan?r. `PASSWORD`, `API_KEY` veya ba?ka kasalardaki kay?tlar? eklemez. Metrikler, oturumdaki kullan?c?n?n okuyabildi?i kay?t k?mesinden taray?c?da hesaplan?r.

Sahip, Y?netici ve Kullan?c? aktif kasay? okuyabildi?inde credential metriklerini g?rebilir. Bu envanter metrikleri i?in entegrasyon ?zelli?i gerekmez. Denet?i ekran? a??p denetim kayd?na dayal? bilgileri okuyabilir; ancak kasa s?rlar?n? okuyamad??? i?in credential say?lar? ve SLA sat?rlar? bu rolde kullan?lamaz. **Y?r?tmeler** ayr?nt?s?na Sahip, Y?netici veya Denet?i ge?ebilir. Credential envanterini ayr?nt? ba?lant?s?ndan a?mak i?in mevcut lisansta entegrasyon ?zelli?i de gerekir.

Active Directory sa?lay?c? ve ajan i?lemi verileri Sahip rol?ne ?zel u?lardan gelir; ancak Rotasyon g?r?n?m? bu sa?lay?c? ve i?lem sorgular?n? etkinle?tirmez. Dizin i?lemi say?lar? yaln?z Sahip oturumu bu sorgular? etkinle?tiren ba?ka bir g?r?n?mde veriyi daha ?nce y?klediyse g?r?nebilir; Rotasyon ekran?na d?n?ld???nde tutulan sorgu verisi g?ncelli?ini yitirmi? olabilir.

Dashboard'un ayr? bir lisans kap?s? yoktur. Salt okunur lisans, g?r?n?m? ve taray?c?ya ?zg? yerle?im de?i?ikliklerini a??k tutar; hedef ekranlardaki credential yazmalar?n? engeller. Tablodaki **Sahip**, kay?tta tutulan sorumlu bilgisidir; VaultPilot Sahip sistem rol? olmak zorunda de?ildir.

## Burada Ne Yap?l?r

- Credential envanterini dizin parola i?lemleri ve e?le?en denetim kay?tlar?yla kar??la?t?r?n.
- 61?90 g?nl?k inceleme adaylar?n?, 90 g?n? a?an kay?tlar? ve okunabilir ya? kayna?? olmayan kay?tlar? ay?r?n.
- Desteklenen ak?? kartlar?ndan haz?rlanm?? credential durumu veya y?r?tme filtrelerine ge?in.
- ?retilen, mevcut veya eski parolalar? g?stermeden olay kan?t?n? inceleyin.
- G?r?nen tarih aral???n? etkin filtre saymadan toplam? en y?ksek alt? site grubunu kar??la?t?r?n.
- **Dashboard ara?lar?** ?zerinden eri?ilebilen kaynak sorgular?n? yenileyin veya widget yerle?imini d?zenleyin; yaln?z Yenile kullanmak dizin i?lemi verisinin g?ncel oldu?unu garanti etmez.

## Widgetlar Nas?l Okunur

### Parola rotasyon ak???

Bu kartlar tek bir huninin a?amalar? de?il, ili?kili sinyallerdir. Farkl? veri k?meleri kulland?klar? i?in say?lar?n birbirini tamamlamas? beklenmemelidir:

| Kart | G?ncel hesap | T?klama davran??? |
| --- | --- | --- |
| Toplam | En fazla alt? e?le?en denetim sat?r? ile y?klenmi? b?t?n dizin parola i?lemlerinin toplam?. | Yaln?z g?sterim. |
| Y?netilen | Dizin bilgisi, AD e?itleme kayna?? veya yenilenmi? kaynak bilgisi bulunan credential kay?tlar?. | Credential ekran?n? **Y?netilen** filtresiyle a?ar. |
| Y?netilmeyen | Y?netilen s?n?f?na girmeyen credential kay?tlar?. | Credential ekran?n? **Y?netilmeyen** filtresiyle a?ar. |
| G?ncellenen | `SUCCEEDED` durumundaki `RESET_TEMP_PASSWORD` veya `REQUIRE_PASSWORD_CHANGE` i?lemleri. | Y?r?tmeler ekran?n? **Dizin / Tamamland?** filtresiyle a?ar. |
| S?resi dolan | Riski s?resi dolmu? olan ya da durumu iptal edilmi? veya kapat?lm?? credential kay?tlar?. | Credential ekran?n? **S?resi dolan / pasif** filtresiyle a?ar. |
| Bekleyen | Parola d??? i?ler dahil, `PENDING` veya `LEASED` durumundaki b?t?n y?klenmi? dizin i?lemleri. | Y?r?tmeler ekran?n? **Dizin / Aktif** filtresiyle a?ar. |
| Hata | `FAILED` veya `STALE_REVIEW_REQUIRED` durumundaki dizin parola i?lemleri. | Y?r?tmeler ekran?n? **Dizin / Ba?ar?s?z** filtresiyle a?ar. |

E?le?en denetim eylemleri `PASSWORD_CHANGE`, `USER_PASSWORD_SET` ve `DIRECTORY_AGENT_ACTION` kodlar?d?r. **Toplam**, denetim sat?rlar?n? i?lem sat?rlar?yla birle?tirdi?i i?in ayn? operasyonun birden fazla kan?t? olabilir; bu say? benzersiz credential say?s? de?ildir.

### Rotasyon SLA

Okunabilir her `CREDENTIAL` kayd? sabit bir parola ya?? aral???na atan?r:

| G?r?nen aral?k | Hesap |
| --- | --- |
| 0?30 g?n | 30 g?n veya daha az. |
| 31?60 g?n | 30 g?nden b?y?k, 60 g?nden k???k veya e?it. |
| 61?90 g?n | 60 g?nden b?y?k, 90 g?nden k???k veya e?it; dashboard'un yakla?an inceleme aral???. |
| 90+ g?n | 90 g?nden b?y?k; gecikmi? aral?k. |
| Tarih yok | Okunabilir kaynak zaman damgas? yok. |

Ya? i?in s?ras?yla dizindeki `passwordLastSetAt`, kayd?n `importedAt` ve kayd?n `updatedAt` de?eri kullan?l?r; bulunan ilk de?er hesab? belirler. Hesap, tan?ml? sonraki rotasyon tarihine veya kuruma ?zel SLA'ya dayanmaz. Gelecekteki tarih s?f?r g?ne sabitlenir; okunamayan tarih **Tarih yok** grubuna gider.

Tabloda en fazla be? kay?t g?sterilir; ?nce hesaplanan ya?? en b?y?k olanlar, e?itlikte ba?l??a g?re s?ralan?r. Tarihi olmayan sat?rlar tarihli sat?rlar?n arkas?na d??er. Kullan?c? ad? bo?sa **Kullan?c?** s?tununda `-` g?r?n?r. **Sahip** s?ras?yla kay?t sahibi, dizin hesab? ve kullan?c? ad?ndan ??z?l?r; ??? de bo?sa h?cre bo? kal?r. ?ubuklar ve sat?rlar t?klanamaz.

### Parola rotasyonlar?

- **Denetim olay?**, ekrana sa?lanan e?le?en denetim sat?rlar?n?n en fazla alt?s?n? sayar; ?m?r boyu toplam de?ildir.
- **AD aksiyonu**, ba?ar?l? dizin parola i?lemlerini y?klenmi? b?t?n dizin parola i?lemlerine oranlar; ba?ar?s?z ve yeniden inceleme isteyen i?lemler dikkat gerektirir.
- **Bekleyen i?lem**, `PENDING` veya `LEASED` durumundaki b?t?n y?klenmi? dizin i?lemlerini sayar. Sahip, Y?netici ve Denet?i i?in say? s?f?rdan b?y?kse **Dizin / Aktif**, s?f?rsa **Dizin / T?m?** filtresini a?ar. Kullan?c? rol?nde kapal?d?r.

Zaman ?izelgesi en fazla alt? denetim sat?r?yla d?nen ilk d?rt dizin parola i?lemini birle?tirir, zamana g?re s?ralar ve en fazla yedi kay?t g?sterir. Sat?rlar yaln?z g?sterim i?indir ve parola de?eri g?stermez.

### Site bazl? rotasyon

Toplam? en y?ksekten d????e, e?itlikte site ad?na g?re s?ralanm?? en fazla alt? site sat?r? g?sterilir. Widget ?u kaynaklar? birle?tirir:

- Dizin bilgisi ve AD e?itleme kayna?? olmayan credential kay?tlar? **Y?netilmeyen** b?l?m?ne yaz?l?r; alan ad?, kayd?n sunucu ad? veya **Yerel** alt?nda gruplan?r.
- Dizin parola i?lemleri sa?lay?c?n?n site ad?, alan ad?, sa?lay?c? ad? veya hedefiyle gruplan?r ve **G?ncellenen**, **Bekleyen** ya da **Hata** b?l?m?ne eklenir.
- Ayn? s?n?rl? denetim sat?rlar? denetim hedefine g?re gruplan?r. `PASSWORD_CHANGE` ve `USER_PASSWORD_SET`, **G?ncellenen** b?l?m?ne eklenir; `DIRECTORY_AGENT_ACTION` renkli b?l?me eklenmeden toplam? b?y?tebilir.

G?r?nen 45 g?nl?k aral?k mevcut s?r?mde yaln?z ba?l?k bilgisidir; site hesab?n? filtrelemez. Bu nedenle renkli b?l?m toplamlar? sat?r toplam?ndan k???k olabilir. Grafik eksiksiz 45 g?nl?k uyumluluk raporu de?ildir ve site sat?rlar? t?klanamaz.

## Filtreler, Ayr?nt?ya Ge?i? ve Yerle?im

Rotasyon ekran?n?n kendi tarih, sahip, ya?, site veya durum filtresi yoktur. Desteklenen kart ekrandan ??kar ve **Credential** ya da **Y?r?tmeler** ekran?nda haz?r filtre uygular. SLA ?ubuk ve sat?rlar?, zaman ?izelgesi ve site sat?rlar? yaln?z g?sterim i?indir.

Credential ayr?nt?lar? **Y?netilen**, **Y?netilmeyen** veya **S?resi dolan / pasif** filtresini uygulamadan ?nce protokol, risk, kaynak, arama ve ak?ll? filtre durumunu temizler. Y?r?tme ayr?nt?lar? Dizin kategorisiyle Tamamland?, Aktif veya Ba?ar?s?z durumunu haz?rlar. Normal rol ve lisans korumalar? ge?erlidir; t?klamak bir i?lemin ?al??t???n? kan?tlamaz.

**Dashboard ara?lar?** bu rehberi a?ar, veriyi yeniler veya yerle?im d?zenleme moduna ge?er. D?zenleme modunda s?r?kle-b?rak ya da ok tu?lar?yla s?ralama, gizleme ve geri alma, kaydetme, vazge?me ve varsay?lan yerle?ime d?nme bulunur. Yerle?im bu taray?c?da tutulur ve yaln?z g?r?n?m? de?i?tirir. D?rt widget da gizlenirse **Kategori widgetlar?n? geri getir** se?ene?ini kullan?n.

## Veri G?ncelli?i ve S?n?rlar

**Yenile**, oturumun eri?ebildi?i kasa, denetim, tan?lama, y?r?tme, dizin sa?lay?c?, lisans, kullan?c?, eklenti, g?ncelleme ve payla??m sorgular?n? ge?ersiz k?lar; dizin i?lemi sorgusunu ge?ersiz k?lmaz. Rotasyon g?r?n?m? ne dizin sa?lay?c? ne de dizin i?lemi sorgusunu etkinle?tirir. Bu nedenle bu ekrandaki Yenile, AD i?lemi say?lar?n?n g?ncel oldu?unu garanti etmez. G?ncel dizin kan?t? gerekiyorsa Sahip, bu sorgular? etkinle?tiren bir g?r?n?m? a??p y?klemenin tamamlanmas?n? beklemeli ve sonra Rotasyon ekran?na d?nmelidir.

Her sorgu yine rol, lisans, aktif kasa ve u? eri?imi kurallar?na uyar. Tek bir anl?k g?r?nt? zaman? veya son g?ncelleme alan? yoktur; sorgular tamamland?k?a de?erler de?i?ebilir.

Ekran credential'?n h?l? kullan?mda oldu?unu, hedefin yeni parolay? kabul etti?ini veya geri d?n???n ?al??t???n? kan?tlamaz. `SUCCEEDED` ajan i?lemi durumudur; denetim sat?r? yaln?z olay?n kayda ge?ti?ini g?sterir. ?kisi de hedefte u?tan uca giri? testi de?ildir.

## ?nerilen ?? Ak??lar?

### Yakla?an, gecikmi? ve tarihi eksik kay?tlar? inceleme

1. **61?90 g?n**, **90+ g?n** ve **Tarih yok** say?lar?n? ayr? de?erlendirin.
2. Be? sat?rl?k en eski kay?tlar tablosunu yaln?z ba?lang?? noktas? olarak kullan?n.
3. Credential ekran?nda sahip, hesap, hedef, kaynak, ger?ek son de?i?im kan?t?, ba??ml?l?klar ve geri d?n??? do?rulay?n.
4. Kurumun onayl? de?i?iklik s?recini kullan?n; dashboard rotasyon planlamaz veya ?al??t?rmaz.
5. Yetkili de?i?iklik ba?ka y?zeyde tamamland?ktan sonra yenileyip kaynak tarih ve kan?t?n de?i?ti?ini do?rulay?n.

### Ba?ar?s?z veya bekleyen dizin i?ini inceleme

1. **Hata**, **Bekleyen** veya **Bekleyen i?lem** se?ene?ini kullan?n.
2. Y?r?tmeler ekran?nda kategori, durum, sa?lay?c?, hedef, zaman ve g?venli hata s?n?f?n? do?rulay?n.
3. Y?r?tme ile denetim kan?t?n? kar??la?t?r?n; ?ift kan?t? ayr? credential olarak saymay?n.
4. Yeniden deneme, iptal veya yeni i?i yaln?z yetkili operasyon ekran?ndan ba?lat?n.

### Eksik sahip veya tarih bilgisini d?zeltme

1. **Tarih yok**, `-` veya bo? sahip h?cresini sa?l?kl? durum de?il, eksik kan?t say?n.
2. Credential kayd?n? a??p eksik ya? kayna??n? veya sahip alan?n? belirleyin.
3. Kasa yaz?labilir ve yetki uygunsa onayl? kay?t bilgisini d?zeltin; notlara gizli de?er koymay?n.
4. Yenileyip beklenen ya? aral???n? ve sorumlu ki?iyi do?rulay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Yenileniyor | Bekleyin; kaynak sorgular ayr? zamanlarda tamamlanabilir. |
| Credential kayd? yok | Aktif kasay? ve kasa okuma iznini do?rulay?n. Bu metrikler i?in entegrasyon ?zelli?i gerekmez; parola ve API anahtar? kay?tlar? SLA'y? doldurmaz. |
| 61?90 g?n | Yakla?an inceleme aday? say?n; kurumun ger?ek politikas?n? ayr?ca do?rulay?n. |
| 90+ g?n | Gecikmi? inceleme aday? say?n; sahip, ba??ml?l?k ve geri d?n?? olmadan rotasyon yapmay?n. |
| Tarih yok | `passwordLastSetAt`, i?e aktar?m ve g?ncelleme zaman?n? do?rulay?n. Sonraki rotasyon tarihi alan? yoktur. |
| Sahip eksik | ?? atamadan ?nce kay?t sahibi, dizin hesab? veya kullan?c? ad? bilgisini tamamlay?n. |
| Ba?ar?s?z / yeniden inceleme | Ba?ar?s?z y?r?tmeleri a??p g?venli hata ba?lam?n? inceleyin. |
| Bekleyen | Aktif dizin y?r?tmelerini a??p parola i?lemlerini di?er kuyruk i?lerinden ay?r?n. |
| ??lem kayd? yok | Y?klenmi? e?le?en kan?t yoktur; credential'lar?n g?ncel oldu?unu kan?tlamaz. |
| Site verisi yok | Credential envanterini do?rulay?n. Rotasyon g?r?n?m? sorgular? etkinle?tirmedi?i i?in Sahip rol?ne ?zel dizin i?lemi verisi yok veya g?ncelli?ini yitirmi? olabilir. Bu canl? tarama de?ildir. |
| Widgetlar gizli | D?zenleme modunda tek tek widgetlar? veya kategoriyi geri al?n. |
| Denet?i | Denetim kayd?na dayal? bilgi g?r?nebilir; credential envanteri ve SLA sat?rlar? kullan?lamaz. |
| Salt okunur lisans | G?r?n?m ve taray?c?ya ?zg? yerle?im a??kt?r; credential yazmalar? engellenir. |

## ??lemden ?nce

- Aktif kasay? ve rol? do?rulay?n. Dizin i?lemi kan?t? ?nemliyse say?lara g?venmeden ?nce Sahip rol?yle bu sorgular? etkinle?tiren bir g?r?n?mden veriyi yenileyin.
- Widgetlar? tek uzla?t?r?lm?? toplam veya ard???k ak?? de?il, farkl? kan?t k?meleri olarak okuyun.
- Yakla?an veya gecikmi? aral??? kullanmadan ?nce ger?ek kaynak tarihini do?rulay?n.
- Sahip, hedef, ba??ml?l?k, bak?m penceresi, geri d?n?? ve kurtarma yolunu do?rulay?n.
- ??lem kan?t? i?in Y?r?tmeler ve Denetim Ge?mi?ini; envanter i?in credential kayd?n? kullan?n.
- Karta t?klaman?n rotasyon, yeniden deneme, onay veya zamanlama yapmad???n? unutmay?n.

## G?venli Kan?t

- Payla??labilir: toplu ya? aral???, genel i?lem durumu, redakte site s?n?f?, genel hata s?n?f? ve geni? zaman aral???.
- Gizli kalmal?: ba?l?k, kullan?c? ad?, sahip, dizin hesab?, alan ad?, host, sa?lay?c?, site, denetim hedefi, i?lem kimli?i, kesin zaman ve m??teri ba??ml?l?klar?.
- Asla payla?may?n: mevcut, eski, ge?ici veya ?retilen parola; eri?im anahtar?; kurtarma kodu; kimlik bilgisi i?eren komut ??kt?s? ya da gizli de?er g?steren ekran g?r?nt?s?.
- M??teriyi veya hesab? belirleyebilecek az ?yeli site etiketlerini ve kesin say?lar? maskeleyin. Yaln?z k?rpmak yeterli de?ildir.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Sahip bilinmiyorsa, ya? kaynaklar? ?eli?iyorsa, gelecekteki veya bozuk tarih ?nceli?i de?i?tiriyorsa, i?lem ve denetim kan?t? uyu?muyorsa, ?retilen parola a???a ??km?? olabilir, hedef g?venle s?nanam?yor veya geri d?n?? bilinmiyorsa durun. Gizli de?er eklemeden; geni? ya? aral???, redakte i?lem durumu, genel hata s?n?f?, geni? zaman aral??? ve son g?venli ad?mla ?zel destek kayd? a??n.

## Operat?r Notlar?

Rotasyon, izleme ve ilgili ekrana ge?i? dashboard'udur. Ya? aral?klar? taray?c?da hesaplanan sabit s?n?flard?r; yap?land?r?labilir SLA motoru veya sonraki rotasyon zamanlay?c?s? de?ildir. Kartlar parola yenilemez, dizin i?lemi olu?turmaz, hedefte giri? do?rulamaz ve uyumluluk belgesi ?retmez.

## ?lgili

- [Active Directory kay?tlar? ekran?](screen-active-directory-records.md)
- [Y?r?tmeler ekran?](screen-executions.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
- [Entegrasyonlar ekran?](screen-integrations.md)
- [Operat?r runbook](operator-runbook.md)
